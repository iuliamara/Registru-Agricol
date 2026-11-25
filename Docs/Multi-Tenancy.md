# Multi-tenancy implementation

[Documentation index](README.md) · [Database](Database.md) · [Architecture](Architecture.md)

The backend uses **schema-per-tenant within one PostgreSQL database and one configured datasource**, combined with shared global tables and tenant ID columns on selected records. This conclusion follows the connection provider, entity mappings, migrations, authentication filter, and public-service controllers rather than the `multiTenancy` configuration label alone.

## Tenant, institution, and UAT

| Concept | Definition and persistence |
| --- | --- |
| Tenant | Organization/workspace in `public.tenants`: string ID, display name, schema name, creation time, activity/deletion flags |
| Tenant schema | Normally `uat_<tenantId>`; contains operational agricultural records, local UAT copies, applications, and audits |
| Public UAT | Global `public.uats` entry with numeric ID, SIRUTA code, name, county, type, activity, and nullable tenant ID |
| Local UAT | Schema-relative `uats` entry; copied when assigned and referenced by local household records |
| Institutional user | `public.users` with role, tenant ID, optional UAT ID, and activity; not a separate per-tenant account table |
| Citizen account | `public.cetateni`; global account without a tenant claim; applications may span institution tenants |

A tenant can manage more than one UAT. The word “institution” in the interfaces mostly describes the tenant organization and its users; the source does not define an additional independent public-institution domain object.

## Provisioning and lifecycle

`TenantController` is restricted to SUPER_ADMIN. `POST /api/tenants` accepts `tenantId` and `name`. `TenantService.createTenant` checks null arguments and duplicate registry ID, constructs `uat_<id>`, executes schema creation through JDBC, then configures Flyway for `classpath:db/tenant`.

The registry row is saved **after** provisioning succeeds. A caught provisioning/migration error triggers a best-effort `DROP SCHEMA IF EXISTS ... CASCADE` cleanup and then a runtime error. Schema operations and registry persistence are not one transaction with guaranteed compensation in every failure path. The runtime connection provider validates tenant ID syntax; provisioning concatenates its own DDL and does not reuse that validator. This documentation does not imply a complete provisioning security boundary.

Tenant migrations use `outOfOrder(true)`, `validateOnMigrate(false)`, and `repair()` before `migrate()`. Those choices explain how this project accepts evolved tenant migrations; they are not a recommended universal migration policy. Global Flyway is configured separately with validation enabled, out-of-order disabled, and clean disabled.

`DatabaseSeeder` invokes `migrateAllTenants()` on startup. Initial public migrations supply demo tenants/UATs; the runner then provisions/migrates their schemas and populates demo accounts/agricultural data. It has no `@Profile` restriction. `POST /api/tenants/migrate-all` exposes explicit super-admin migration. Failures for one tenant are logged and the migration loop continues.

Tenant update currently changes the **name only**. The UI delete action displays a manual-database-intervention message; no tenant delete controller exists. `isActive` and soft-delete fields exist but are not a complete exposed activation/deactivation/deprovisioning lifecycle. Do not infer login denial or access revocation from the existence of an activity column.

Sources: [tenant service](../src/backend/src/main/java/com/multitenant/service/TenantService.java), [tenant controller](../src/backend/src/main/java/com/multitenant/controller/TenantController.java), [startup seeder](../src/backend/src/main/java/com/multitenant/config/DatabaseSeeder.java).

## Institutional tenant resolution

```mermaid
sequenceDiagram
    participant F as Institutions Portal
    participant J as JWT filter
    participant T as TenantFilter / TenantContext
    participant H as Hibernate resolver/provider
    participant P as PostgreSQL
    F->>J: Request + jwt cookie (or Bearer fallback)
    J->>J: Verify signature/expiry; construct role/tenant principal
    J->>T: Continue filter chain
    T->>T: Set thread-local tenant from institutional principal
    T->>H: Authorized controller/service repository call
    H->>P: SET search_path TO "uat_id", public
    P-->>H: Tenant-relative query result
    H->>P: Reset search_path to public on release
    T->>T: Clear thread-local in finally
```

1. `JwtUtils` signs institutional JWTs containing `userId`, `tenantId`, `uatId`, `role`, and `type=USER`.
2. `JwtAuthenticationFilter` prefers the institutional cookie for non-public URLs and the citizen cookie for `/api/public/`; if no cookie is selected, it accepts a Bearer header. Cookie fallback permits either cookie when the preferred type is absent.
3. The filter reconstructs an institutional principal from claims. It does not select a schema from an arbitrary `X-Tenant-ID` header.
4. `TenantFilter` chooses its default `public`, then overrides it from a nonblank institutional principal tenant. Citizen principals remain in public.
5. `TenantIdentifierResolver` returns the context value, or `public` if unset, and requests validation of existing sessions.
6. `JpaConfig` registers the custom resolver/provider through Hibernate property customization.
7. `MultiTenantConnectionProviderImpl` acquires a datasource connection and sets a quoted schema plus public fallback; release resets to public and closes the connection.

The provider allows tenant IDs matching `^[a-zA-Z0-9_-]{1,32}$`, maps `public` specially, and otherwise derives the schema by prefix. It does not query `Tenant.schemaName` on each request. Registry/schema-name consistency therefore matters; a custom stored schema name does not independently change runtime routing.

`TenantContext` is a `ThreadLocal<String>`. It is not automatically propagated to Kafka listener threads, scheduled threads, or an async executor. Current scheduler/transfer/public-controller paths set context explicitly where needed. Reusing a context across an already-open Hibernate session is not a general way to switch schemas.

Sources: [tenant configuration package](../src/backend/src/main/java/com/multitenant/config/tenant), [JWT filter](../src/backend/src/main/java/com/multitenant/security/JwtAuthenticationFilter.java), [JWT claims](../src/backend/src/main/java/com/multitenant/security/JwtUtils.java).

## Repositories and isolation model

Tenant entities usually omit an explicit `schema` in `@Table`, so their generated SQL resolves relative table names through the selected connection search path. Most repositories consequently use ordinary Spring Data methods or JPQL without a `WHERE tenant_id` clause on every query. Schema selection is the primary separation mechanism.

Core `Tenant`, `User`, `PublicUat`, and `Cetatean` entities explicitly map to `public`. Global lookup and crotal registry operations likewise use public data. Selected operational models still carry tenant metadata (persons, animals/events, identity documents, access logs). Those columns supplement context and business behavior; the system does not use a single shared operational table set with universal discriminator filtering.

The `public` search-path fallback allows shared references to be resolved. It also means missing/incorrect context is not equivalent to a separate database credential boundary. Most domain controllers have `@TenantRequired`; the aspect rejects the literal `public` context with 400. The aspect does not itself validate tenant existence, activity, or null context, and it is not present on every controller.

## Public applications and citizen aggregation

Citizen tokens contain no institution tenant. `CerereController` and public verification/status operations first resolve a numeric `PublicUat` ID, then set its `tenantId` in context around tenant calls. The selected county/locality therefore determines application storage; the static citizen UAT list alone does not provision a tenant.

`getMyCereri()` requires a citizen principal, collects distinct nonblank tenants from global UAT assignments, and queries each for `userId`. `AtestatController` follows similar enumeration for document/status details. These operations intentionally cross schemas on behalf of a global citizen identity. They are synchronous loops, not a federated index or demonstrated scalable query engine.

The public submission/tracking/by-CNP endpoints are permitted without account login. `/my-cereri`, profile, and attestation status check identity in controller code. The accepted-PDF controller scans numeric IDs across schemas, which can select a colliding record before ownership checking. These details qualify the otherwise useful schema-isolation design.

## UAT assignment and within-tenant filtering

Global UAT creation/edit/delete is SUPER_ADMIN-only. Tenant assignment/removal is ADMIN-only. The assignment service rejects an already claimed UAT, copies its data into the active tenant's local `uats`, and records the tenant ID on `public.uats`. Removing clears the global assignment and deletes the local record according to repository semantics.

The institutional active-UAT selector stores a SIRUTA code and sends it only on operations supporting that filter. It does not reissue authentication. `uatId` in the JWT is not a universal enforced record scope. Tenant users may access their schema's other UAT data through APIs not constrained to a UAT.

The super-admin tenant detail UI calls missing `/api/tenants/{id}/uats/{code}` endpoints. The working tenant UAT endpoints under `/api/uats/tenant` omit SUPER_ADMIN from their method roles. [Integration status](Implementation-Status.md) records both facts.

## Super-admin tenant impersonation

`POST /api/auth/impersonate` permits SUPER_ADMIN and issues a replacement institutional cookie with the requested tenant ID, preserving the same identity, authority, and UAT claim. Frontend subjects update visible tenant context. Choosing `public` is the intended stop action.

The controller does not verify that the requested tenant exists or is active. Super-admin context selection does not transform the role into ADMIN and cannot grant permissions omitted from endpoint expressions. The sidebar stop method calls the cold HTTP observable without subscribing, so that particular UI path does not execute the request. These are current behavior limits rather than a reason to describe super-admin access as unrestricted.

## Deliberate cross-tenant operations

| Operation | Context and transaction handling |
| --- | --- |
| Animal destination lookup | Authorized institutional endpoint accepts target tenant, temporarily selects it, returns household/person DTOs, restores original context |
| Individual animal transfer | Validates destination, uses separate transactions for source/destination, copies history, updates global crotal registry, attempts compensation after insertion failure |
| Citizen application history/status | Enumerates UAT-associated tenant IDs and filters records by citizen identity or identifier hash |
| Contract scheduler | Enumerates registry tenants, sets each context before service transactions, restores original context in `finally` |
| Migrate-all | Uses each registry schema name to configure Flyway independently |

Cross-tenant animal destination lookup is available to ordinary institutional operational roles. It intentionally exposes destination data, so the system should not be described as prohibiting every cross-tenant read. Transfer compensation is a best-effort multi-step recovery mechanism, not an atomic transaction across schemas.

## Isolation limits

| Boundary | What the implementation establishes | Remaining limit |
| --- | --- | --- |
| Operational SQL | Schema-relative Hibernate sessions with reset on release | Shared datasource credential; correct context/session lifetime is essential |
| Global users | Tenant-filtered listing and target-user helper | Global table intentionally shared; JWT active state is not reloaded per request |
| Public UAT routing | Explicit chosen-UAT → tenant lookup | Submission/tracking are public; no full citizen/tenant eligibility rule |
| WebSockets | Topic names include tenant/user/code on application flows | Handshake public; wildcard origins; no subscription authorization; succession topic global |
| Household documents | Schema-scoped metadata; randomized filenames | Path is household ID without tenant partition |
| Signed contracts | Schema-scoped contract metadata | Filename is `contract-<id>-semnat.pdf` under one shared directory, allowing tenant-local ID collisions |
| Tenant lifecycle | Registry activity/deletion metadata and provisioning methods | No complete deactivation, revocation, archival, or automatic schema teardown workflow |

## Errors and verification

Invalid provider identifiers produce `SQLException`; missing public context for annotated actions produces 400; duplicate tenants/UAT assignments produce 409; missing references use 404 or runtime errors depending on the service. Unknown/empty public UAT tenant assignments are not comprehensively validated by every public controller, and PostgreSQL schema selection does not itself confirm all required tables exist.

Tests include provisioning/service mocks and an integration test for Envers separation across two schemas. They do not establish isolation for every endpoint, file, public lookup, or topic. [Testing coverage and execution constraints](Testing.md).
