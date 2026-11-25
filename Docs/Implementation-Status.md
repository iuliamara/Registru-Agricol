# Implementation status and historical boundaries

[Documentation index](README.md) · [Audit method](Audit.md) · [Historical originals](Historical/README.md)

This register describes the current working-tree source inspected on 25 November 2026. A functioning code path is not a claim of successful deployment, complete legal coverage, security certification, or production readiness. The current repository is authoritative; recovery material supplies historical context only.

## Status vocabulary

| Label | Meaning |
| --- | --- |
| Integrated source | Frontend binding, backend endpoint/service, and relevant persistence exist; practical caveats may remain |
| Partial integration | Significant code exists but a mismatch, incomplete workflow, or missing enforcement affects the advertised behavior |
| Backend only | Endpoint/service/persistence exists without a corresponding complete frontend workflow |
| Frontend only / placeholder | An action or screen exists without the matching completed backend behavior |
| Demonstration | Seeded/sample/hardcoded UI data or values; not live operational evidence |
| Historical specification | Preserved design/requirements/branch descriptions; not accepted as current implementation evidence |
| Future possibility | Described as an optional next step, not an implemented or committed roadmap item |

## Citizens Portal

| Feature | Status | Evidence / limitation |
| --- | --- | --- |
| Independent citizen application | Integrated source | Own Angular 21 entry point, routes, build, package, Dockerfile, proxy/Nginx |
| Register/login/logout/session/profile | Integrated source | Citizen account/controller/service; no activation/MFA/reset flow |
| Physical/legal registration | Partial integration | Legal-entity HTML identifier range conflicts with unconditional 13-character submit check |
| Landing dashboard | Demonstration/static content | Service explanation cards; no personal statistics query |
| Eleven service cards/shared form | Integrated source | Bundled catalog, profile prefill, JSON submission; no service-specific eligibility engine |
| UAT/institution choice | Partial integration | Static locality data needs matching assigned public UAT IDs; no separate institution entity/directory |
| Application submission | Integrated source | UAT-based tenant selection, PENDING/code/email/topic; backend also permits anonymous submission |
| Attachments | Historical specification | No citizen file input or application-attachment API association |
| Personal history/filter/pagination | Integrated source | Principal check; tenant enumeration by global UAT associations; userId filtering |
| Public tracking | Integrated source | Code + global UAT; returns DTO without account login |
| Accepted PDFs | Partial integration | Owner/status checks and templates exist; local-ID schema scan can select a colliding application |
| Attestation/booklet cards | Partial integration | Global flags plus cross-schema detail/status queries; flags alone do not establish current validity |
| Live application updates | Integrated source | STOMP user/code topics and UI toast/history update; subscriptions not privately authorized |
| Profile contract notifications | Integrated source, ephemeral UI | Kafka→CNP topic; component memory only, no persisted notification inbox |
| Email confirmation | Integrated source | Synchronous JavaMail/Thymeleaf; credentials/delivery not tested here |
| Citizen agricultural declarations/household data editor | Historical specification | No current citizen module implements the proposed annual self-service declarations |

Sources: [citizen guide](Applications/Citizens-Portal.md), [citizen route table](../src/portal-cetateni/src/app/app.routes.ts), [application controller](../src/backend/src/main/java/com/multitenant/controller/CerereController.java).

## Public Institutions Portal

| Feature | Status | Evidence / limitation |
| --- | --- | --- |
| Independent institutional application | Integrated source | Own Angular 18 workspace; dashboards are sections in it |
| Role-specific navigation/login redirects | Integrated source | SUPER_ADMIN/ADMIN/USER; source routes lack guards |
| Tenant/global dashboards | Partial integration + demo values | API counts exist; UAT count fallback, last-login placeholders, hardcoded error fallback users, export TODO |
| People, identity docs, relationships | Integrated source | Single-table inheritance, collections, search/hash lookup, type-change rejection; no verified full CNP/CUI checksum validation |
| Household CRUD/membership/head/history | Integrated source | Many-to-many links, optional head, editable events/documents; historical mandatory adult-head/closure constraints not fully enforced |
| Land/parcel and cadastral references | Integrated source | Parent hierarchy, CRUD, coordinate/JSONB geometry, land-book update/events; not official title synchronization |
| Crops/trees/vines/pastures/forestry/water | Integrated source | Parcel forms/services/API; validation varies; historical area-balancing targets not universal guarantees |
| Production cycles and harvests | Integrated source | Single active cycle, date association, harvest aggregation and forms |
| Environmental observations | Backend only | `FactoriMediuController/Service`; no dedicated institutional frontend entry service/workflow found |
| Buildings, machinery, household files | Integrated source | Embedded management; files have MIME/service-size/path checks and storage limitations |
| Individual/group livestock | Integrated source | Ear tags, events, snapshot history; equal-date latest snapshots may contribute twice |
| Cross-tenant transfer | Integrated source | Destination reads and explicit transfer transactions/compensation; no distributed atomicity guarantee |
| Veterinary treatment | Integrated source as event | `TRATAMENT_VETERINAR` with date/details; no separate normalized treatment catalog |
| Plant treatment/fertilization | Integrated source | PPP/catalog/activity/PDF rules; code thresholds are not legal certification |
| Contracts CRUD/signing | Integrated source | Parcel/person/date/rent records and SignNow actions; external transaction not tested |
| Contract overlap/date consistency | Historical specification / partial validation | Current service does not implement the earlier branch's complete overlap rule |
| Expiry scheduler/alerts | Integrated source | Every minute; repeated alerts possible; historic midnight description outdated |
| Succession records/search/stage | Integrated source | V53/person death/hash/correspondence; no heirs, adjudication, estate transfer, or actual notarial delivery |
| Citizen applications/decisions/PDF | Partial integration | ADMIN/USER decision path; SUPER_ADMIN omitted; PDF admin branch excludes ordinary ROLE_USER |
| Strict application lifecycle / rejection message | Historical specification | Source accepts supplied status enum; no reason/deadline/assignment workflow |
| Reports and Excel exports | Integrated source | Actual POI `.xlsx`; year only affects selected datasets; vegetal card can double-count area |
| GIS | Integrated source | Leaflet/OSM, custom conversion, JSONB; no current Google Maps/Leaflet Draw/spatial-overlap engine |
| Global UAT CRUD / tenant UAT assignment | Integrated source | Roles differ; active UAT is a filter, not a universal authorization boundary |
| Tenant detail UAT assignment buttons | Frontend only / mismatched API | Calls `/api/tenants/{id}/uats/{code}`; no matching controller mapping |
| Tenant create/list/rename/migrate | Integrated source | Schema provision and Flyway; no full activation/deactivation lifecycle |
| Tenant deletion | Placeholder | UI says manual database intervention; no delete endpoint |
| Global/tenant user management | Integrated source | UserDTO, forced tenant on admin create, target helper; existing JWTs not immediately revoked |
| Super-admin user shortcuts | Partial integration | Navigate to `/users`; registered page is `/user-management` |
| Stop impersonation from sidebar | Partial integration | Calls cold observable without subscription; request does not execute through that method |

Sources: [institutional guide](Applications/Public-Institutions-Portal.md), [source inventory](Reference/Source-Inventory.md), [API catalog](Reference/API.md).

## Shared engineering mechanisms

| Mechanism | Verified implementation and practical boundary |
| --- | --- |
| Shared backend | One Spring Boot service, not deployed domain microservices |
| Tenant isolation | One datasource, schema search path, global identity and directory; selected explicit cross-schema flows |
| Identifier encryption | Selected fields via AES/CBC; legacy fallback and SQL backfills require consistency review |
| Exact identifier search | Salted SHA-256 index; no general substring search on ciphertext |
| RBAC | Method checks on most domain APIs; public controller checks and role asymmetries remain |
| Soft delete | Many entity annotations/migrations; not universal physical cascade or data-retention policy |
| Change audit | Envers on selected entities, parcel history; not every table/action |
| Access audit | AOP on annotated methods, REQUIRES_NEW log write; no general audit-viewer route |
| Kafka | Contract/succession producers/consumer; application updates go directly to Spring messaging |
| WebSockets | Public SockJS handshake, simple topic broker, no subscription-specific access configuration |
| File storage | Local paths; household directories and signed-contract filenames not fully tenant partitioned |
| Database migrations | Public and tenant Flyway policies differ; startup repair/migrate/seeding active |
| Testing | Selected unit/controller/integration coverage; frontend mainly smoke tests; configuration gaps documented |
| Deployment | Compose/Nginx/Dockerfiles present; no observed CI/CD, HA, backups, or production hardening evidence |

## Corrections to historical descriptions

The complete original documents remain available; the following corrections orient current readers without replacing those originals.

| Historical statement | Current source |
| --- | --- |
| One frontend with citizen/admin roles | Two independent Angular applications, one shared backend |
| Java 17+ / one generic Angular version | Java 21, Angular 21 citizens and Angular 18 institutions |
| `X-Tenant-ID` chooses tenant | JWT institutional tenant claim; explicit public UAT/cross-tenant paths |
| Per-tenant user tables | Institutional users map explicitly to `public.users` |
| One automatic land per household | Multiple land records; current household service does not auto-create land |
| JTS/PostGIS polygon persistence / Google Maps / Draw | JSONB `JsonNode`, Leaflet/OSM, custom TypeScript coordinate conversion |
| Succession V39 and `persoane_fizice` | V53, `persons` single-table inheritance |
| Notice `tenant_id` / digital operator signature | Schema scoped, no tenant column; username metadata is not a cryptographic signature |
| Guaranteed log-free/private succession communication | Plain identifiers can appear in URLs/logs; general broker destination lacks tenant-specific access |
| CSV statistics | Current POI service returns `.xlsx` workbooks |
| Midnight expiry job | Active cron is every minute; midnight cron is commented |
| Asynchronous application email | Direct synchronous JavaMail call with caught errors |
| Route guards implemented on current main | Current institution routes lack guards; historical branch claims are not merged-state evidence |
| Automatic notary delivery/inheritance ownership | Notice records/internal Kafka event only |

## Historical requirements and future possibilities

Preserved specifications cover richer ownership quotas/title reconciliation, tax and subsidy models, national register exports, identity-provider/MFA integration, citizen annual declarations, mobile inspections, legal deadlines, declaration campaigns, spatial validation, complete role hardening, and operational scaling. They retain their original rationale, examples, Romanian terminology, diagrams, and branch context in [Historical](Historical/README.md).

These are not release commitments. Potential contributor work should begin with the existing partial integrations, source-backed tests, and clear business acceptance criteria. Legal references in archived research retain their historical meaning and were not revalidated as current legal advice during this documentation task.
