# Shared backend implementation

[Documentation index](README.md) · [API catalog](Reference/API.md) · [Domain/DTO reference](Reference/Domain.md) · [Multi-tenancy](Multi-Tenancy.md)

The shared backend is the Java 21 Maven project in [`src/backend`](../src/backend), based on Spring Boot 3.3.0. Both independent Angular applications call it through relative `/api` URLs. Its package structure separates controllers, services, repositories, models, DTOs/payloads, security, tenant configuration, aspects, converters, and domain events.

## Layers and application-specific responsibilities

| Layer | Project-specific implementation |
| --- | --- |
| HTTP controllers | Citizen and institutional auth; public application/UAT/status endpoints; administrative applications; tenant/user/UAT management; agricultural domain CRUD; maps proxy; report/download endpoints |
| Services | Resolve related records, assign tenant metadata, apply domain calculations, control transactions, issue documents, publish messages, coordinate cross-schema transfers |
| Repositories | Spring Data JPA CRUD/pagination, filtered JPQL, statistical DTO projections, hash lookups, explicit JDBC/JdbcTemplate for selected global/domain operations |
| Models | `core` global administration/accounts, `persoana` inheritance, `registru` household/land/agricultural records, `animal` lifecycle records, `audit` revisions/access logs |
| DTOs/payloads | Flattened read responses, create/update inputs, report projections, auth/tenant payloads, history differences |
| Infrastructure | JWT and tenant filters, Hibernate schema routing, Flyway, Jackson/ModelMapper configuration, Kafka/WebSocket setup, scheduled expiry, file/email/PDF/signature services |

The citizen-facing backend is concentrated in `CetateanAuthController`, `CerereController`, `AtestatController`, public UAT/identity-verification controllers, and the public branch of `CererePdfController`. Institutional controllers operate on the same tenant application records and on agricultural/administrative domains. They share `CerereService`, document/PDF services, repositories, authentication utilities, and messaging infrastructure.

This is not a uniform DTO-only architecture: several endpoints accept or return entities (animals, parcels, contracts, UATs), while other modules use DTOs. `UserDTO` explicitly avoids password serialization; `PersoanaDTO` combines fields from concrete person types. [Complete controller inputs and method rules](Reference/API.md).

## Mapping and serialization

`ModelMapperConfig` uses strict matching with explicit mappings/converters, including `TipCerere` string/enum conversion and person/household-related DTO handling. Services also map manually when subtype/lazy-reference behavior needs control. `CerereService` explicitly sets the application enum in addition to automatic mapping; invalid enum strings are caught rather than returned through a dedicated type-validation response.

Jackson configuration supports Java time and Hibernate-related serialization concerns. Global date serialization disables numeric timestamp output. Several Angular consumers still normalize array-form dates for compatibility. Lazy loading is not kept open for HTTP views (`open-in-view=false`), so DTO assembly and explicit `Hibernate.initialize`/unproxy work occur inside service transactions where needed.

The [domain reference](Reference/Domain.md) lists entity/DTO/payload fields with source links. A field annotation is not proof that validation executes: the controller must invoke validation, and service/database constraints may differ.

## Authentication and authorization

### Institutional authentication

`POST /api/auth/signin` passes username/password to Spring's authentication manager. `UserDetailsServiceImpl` reads `public.users`; BCrypt validates passwords, and `UserDetailsImpl.isEnabled()` reflects account activity during login. The JWT contains subject, user ID, tenant ID, UAT ID, role, `type=USER`, issue time, and expiry; configured expiry is 86,400,000 ms.

### Citizen authentication

`POST /api/public/cetatean/register` validates a signup payload, checks duplicate email and identifier hash, hashes the password, and saves `public.cetateni`. Login directly compares the submitted password with the stored hash and issues `type=CETATEAN` plus citizen ID/email. The citizen principal is reconstructed as a minimal `Cetatean`; profile operations reload its full database record. Citizen account status/deletion handling is not the institutional `UserDetails` login flow.

### Cookies, principals, and HTTP rules

`JwtAuthenticationFilter` chooses between `jwt` and `jwt_cetatean` cookies by URL prefix with fallback to the other available cookie, then to Bearer authentication. Institutional tokens produce a role authority; citizen tokens produce an empty-authority citizen principal. Invalid-token exceptions are swallowed and the chain continues without successful authentication.

Both cookies use HttpOnly, SameSite=Lax, path `/`, 24-hour age, and `secure(false)`. Authentication is stateless, with CSRF and CORS processing disabled in current `SecurityConfig`. `/api/auth/**`, `/api/public/**`, `/api/ws/**`, and `/error` are permitted at the HTTP layer; remaining requests require authentication. Method-level and controller-local checks then further restrict operations.

Most tenant domain controllers allow SUPER_ADMIN, ADMIN, and USER and require non-public context through `@TenantRequired`. Catalog mutations restrict to admins. `UserSecurity` compares target-user tenant or permits super-admin; the user controller applies additional create/list/edit/delete rules. UAT mutation and assignment rules differ from domain CRUD. Public profile/history/status/PDF operations implement manual principal checks. Certificate and Nominatim proxy controllers do not share all the stricter domain annotations.

JWT requests reconstruct institutional activity as true without a fresh database lookup. Role/activity/tenant changes are not immediately reflected in already-issued tokens. No refresh-token table, token blacklist, MFA, external identity provider, or destination-specific WebSocket authorization was found. These details prevent treating the repository as a completed production security model.

## Tenant resolution and transactions

Institutional tenant claims pass through `TenantFilter` into `TenantContext`. `JpaConfig`, `TenantIdentifierResolver`, and `MultiTenantConnectionProviderImpl` select `uat_<id>, public` on the connection, then reset and close it. Public citizen controllers select context from a global UAT; global entity mappings remain explicitly in `public`. [Full resolution, lifecycle, and isolation explanation](Multi-Tenancy.md).

Ordinary domain services use Spring `@Transactional` / read-only transactions, with repository calls participating in that context. Important exceptions and transaction interactions include:

- Cross-tenant animal transfer uses programmatic separate transactions after selecting each schema, with attempted compensation if insertion fails.
- `CarteFunciaraEventListener` listens AFTER_COMMIT and runs REQUIRES_NEW, so land creation can persist even if its later land-book work fails.
- `GdprAuditService` saves logs in REQUIRES_NEW to decouple audit persistence from the main operation.
- Application notifications, synchronous email, Kafka sends, remote signing, and file writes do not become atomic with database transactions. No outbox pattern is implemented.
- Scheduled contract processing explicitly sets tenant context before transactional service calls and restores it afterward.

## Citizen applications and issuance

Application DTOs contain applicant/contact/address, encrypted identifier/search hash through the entity, optional cadastral/land-book information, application type, status/code, account user ID, UAT ID, and creation time.

Creation resolves the chosen UAT tenant, maps data, assigns `PENDING`, generates `cerere-<8 UUID characters>`, saves, sends a tenant topic message, and attempts email when an address exists. The server does not require authentication for submission; it links the citizen principal when present. Personal history enumerates distinct tenants from public UAT assignments and finds applications by citizen ID.

ADMIN/USER can set `PENDING`, `ACCEPTED`, or `DECLINED`; the implementation does not enforce a one-way state machine or rejection explanation. First transition into acceptance can resolve/create a physical person and issue an attestation or booklet. Attestations use generated numbers, hardcoded series `CJ`, and 60-month validity; booklet issuance requires an existing attestation but accepted status can still be saved without one. These are source behaviors, not verified legally complete issuance procedures.

The PDF controller accepts both public/admin URL prefixes. It requires an accepted application and either its owner or recognized admin authority. Templates are chosen for attestation, booklet, role certificate, or generic application. It scans schemas for a citizen application by numeric ID, so schema-local ID collision is a documented limitation. Public code tracking returns the application DTO, and public by-CNP lookup is a separate exposed API.

Source: [application service](../src/backend/src/main/java/com/multitenant/service/CerereService.java), [application controllers](Reference/API.md#cererecontroller), [PDF controller](../src/backend/src/main/java/com/multitenant/controller/CererePdfController.java).

## Agricultural domain operations

| Domain | Service behavior |
| --- | --- |
| Persons | Set tenant metadata, resolve memberships/relations, assign child document references, prevent concrete type changes, search clear names/hash identifiers |
| Households | Resolve local UAT, filter by UAT/type/activity/search, assign head, create/edit dated member events with optional document |
| Land and parcels | Resolve parent records; create land/initial parcel; store coordinates/GeoJSON; publish land-book events; expose parcel Envers differences |
| Animal individuals | Resolve owner/household, enforce active tag conflict checks, coordinate public tag registry, retain lifecycle event records |
| Group counts | Positive headcounts and dated snapshots; latest-per-household/species queries rather than destructive headcount updates |
| Animal events/transfers | Origin/terminal/date rules; destination validation and explicit cross-schema transfer steps |
| Parcel resources | CRUD for annual crops, trees, vines, pasture/hayfield, forest, water; parent checks on many nested updates/deletes |
| Protected cultivation | One active cycle per parcel; date-based cycle association for treatments/fertilization/harvests; restricted environment observations |
| Chemical evidence | PPP dose/pause/justification; biological release fields; fertilizer nutrient/unit calculations, winter override, organic-input threshold |
| Contracts | Resolve parcel/persons, operating user/date, expire status by date, emit approaching-expiry alerts, coordinate SignNow |

[Institutional functional guide](Applications/Public-Institutions-Portal.md) provides forms, workflows, screenshots, and business terminology. Historical requirements for CNP checksums, mandatory household head, strict land-area totals, spatial overlaps, and contract-date overlaps must not be promoted into service guarantees absent from the source.

## Succession processing

`NotificareSuccesiuneServiceImpl.save` rejects null payload/missing deceased-person ID and non-physical persons. In one service transaction it marks the physical person deceased, applies supplied death date/certificate, ensures the person's blind index when needed, and saves notice metadata. The notice entity copies the hash and timestamps itself. The operator comes from the security context rather than trusting a submitted operator name.

The schema-relative table has a foreign key to `persons`, notice hash, notary name, official correspondence number/date, stage, observations, operator, and registration time. V53 creates it. Search hashes the supplied full CNP and matches the stored notice hash. PATCH requires a nonblank stage but does not enforce an enum transition graph. Kafka emission is attempted and consumed into a general topic. No external notary delivery, heir distribution, title transfer, or succession-document generation is implemented.

## Identifier protection and audit

`AesCryptoConverter` uses AES/CBC/PKCS5Padding with a random 16-byte IV, a SHA-256-derived key, and Base64 encoding of IV+ciphertext. It applies to selected identifiers such as person CNP/CUI, citizen CNP, and application CNP/CUI. On decryption failure it returns the stored value unchanged for legacy compatibility; this can expose opaque/corrupt values through the application rather than rejecting them. It is not authenticated encryption or blanket encryption of all personal fields/files.

`CryptoUtils` hashes `value + configuredSalt` with SHA-256 to supply deterministic exact-match indexes. Changing the configured salt breaks existing hash lookup unless data is reindexed. Encryption-key changes likewise require data migration; no automated rotation procedure is provided. SQL migration backfills and JPA conversion are distinct paths and must be assessed together for an existing database.

Envers `@Audited` and schema-local `revinfo`/`*_aud` tables retain selected entity revisions, with username through `CustomRevisionListener`. `ParcelaService` reads parcel revisions and generates field differences. Coverage follows entity annotations; it is not a complete history of every table.

`@GdprAudited` wraps selected controller methods. The aspect records time, username, HTTP-derived action, entity label, returned/argument IDs, endpoint, and tenant. Logging runs even when an annotated operation fails, but audit-save failures are logged without replacing the original response. This is access traceability, not independent GDPR-compliance certification or an immutable externally secured audit ledger. Current debug output can include identifiers or HTTP request data; a blanket “no personal data in logs” claim is inaccurate.

Sources: [AES converter](../src/backend/src/main/java/com/multitenant/converter/AesCryptoConverter.java), [hash utility](../src/backend/src/main/java/com/multitenant/util/CryptoUtils.java), [audit aspect](../src/backend/src/main/java/com/multitenant/aspect/GdprAuditAspect.java), [revision models](../src/backend/src/main/java/com/multitenant/model/audit).

## Validation, errors, and response formats

Bean Validation appears on selected entities/DTOs and is invoked on controller parameters annotated `@Valid`. Services additionally perform parent/existence/null/date/domain checks, while SQL constraints supply foreign keys, required fields, indexes, and some uniqueness rules. Validation coverage is inconsistent: not every create/update uses DTO validation or the full historical business rules.

`GlobalExceptionHandler` translates `DataIntegrityViolationException` to 400 with a `message`, recognizing older person CNP/CUI constraint names, and `MethodArgumentNotValidException` to a field→message map. It does not provide a uniform handler for every `IllegalArgumentException`, missing-reference `RuntimeException`, remote-service failure, or filesystem error. `ResponseStatusException` is used for selected 400/404/409 cases. `server.error.include-message=always` and database-cause output can expose technical detail.

Responses therefore include entities/DTOs, Spring `Page` objects (`content`, `totalElements`, etc.), plain arrays, text messages, message maps, validation maps, PDF/XLSX bytes, file resources, and empty responses. No universal success/error envelope or generated OpenAPI specification is present.

## Notifications and integrations

`EmailService` renders `templates/email/email-confirmare-cerere.html` and sends synchronously with JavaMail. The application path catches failures. The every-minute contract scheduler publishes expiry alerts through Kafka; the succession producer publishes notice events. `NotificationKafkaConsumer` bridges these to the Spring WebSocket simple broker. Application statuses publish directly to that broker. There is no persisted inbox or atomic outbox; general succession messages are not tenant-partitioned in the broker destination.

`SignNowClient` is an actively called remote integration for contract invitations/status/downloads. Nominatim proxy and direct frontend requests supply address/locality searches; Leaflet/OSM supplies maps. Spatial libraries declared in Maven are not evidence of active spatial SQL: current geometry fields are JSONB and frontend code performs coordinate conversion.

Reports use JPQL constructor projections and Apache POI for `.xlsx`; PDFs use Thymeleaf/OpenHTMLtoPDF and OpenPDF for contracts. Document uploads use local filesystem paths and MIME/size checks. No object store or external archival service is configured.

## Configuration and testing pointers

[Development](Development.md) covers datasource, JWT, crypto, mail, signing, proxy/storage/ports and startup seed behavior. [Testing](Testing.md) distinguishes implemented test infrastructure from execution status. [Source inventory](Reference/Source-Inventory.md) links every audited source unit and frontend route; [migration catalog](Reference/Migrations.md) records both Flyway sets.
