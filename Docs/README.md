# Registru-Agricol documentation

[Project showcase](../README.md) · [Citizens Portal](Applications/Citizens-Portal.md) · [Public Institutions Portal](Applications/Public-Institutions-Portal.md)

This documentation describes **two independent Angular applications and their shared Spring Boot backend**, verified against the current repository on 25 November 2026. It preserves original specifications separately so domain knowledge and development decisions remain available without confusing them with implemented behavior.

**Terminology:** an **administrative application** (Romanian *cerere*) is submitted by an **applicant** through the Citizens Portal and processed through the Public Institutions Portal. “Application” also names a software application where the context is architectural. “Request” retains its technical meaning for HTTP/API communication, bodies, headers, parameters, and literal source identifiers. Romanian text and accurately quoted interface labels retain their original wording.

## Choose a reading path

| Audience | Suggested path |
| --- | --- |
| Recruiter / interviewer | [Root showcase](../README.md) → both application guides → [architecture](Architecture.md) → [engineering/business workflows](Workflows.md) |
| Developer / contributor | [Local development](Development.md) → [backend](Backend.md) → [API](Reference/API.md) → [tests](Testing.md) → [status](Implementation-Status.md) |
| Domain analyst | [Institutional modules](Applications/Public-Institutions-Portal.md) → [workflows](Workflows.md) → [database](Database.md) → [full historical originals](Historical/README.md) |
| Tenant/security reviewer | [Multi-tenancy](Multi-Tenancy.md) → [authentication](Backend.md#authentication-and-authorization) → [isolation limits](Multi-Tenancy.md#isolation-limits) |

## Functional applications

| Guide | Coverage |
| --- | --- |
| [Citizens Portal](Applications/Citizens-Portal.md) | Registration, sessions, profile, eleven services, forms, UAT routing, personal/public tracking, accepted PDFs, attestation/booklet status, email and live alerts |
| [Public Institutions Portal](Applications/Public-Institutions-Portal.md) | Roles, dashboards, persons, households, membership, land/parcels, resources, production, animals, chemical evidence, contracts/signing, succession, applications, GIS, reports, tenant/UAT/user administration |
| [Business workflows](Workflows.md) | Cross-application applications, household establishment, protected-space production, animal transfer, contracts/alerts, succession correspondence, tenant onboarding |
| [Screenshot catalog](screenshots/README.md) | All 21 supplied screenshots, with accurate labels and links to the relevant feature guides |

## Technical documentation

| Guide | Coverage |
| --- | --- |
| [Architecture](Architecture.md) | Deployment units, component boundaries, HTTP request flows, events, external integrations |
| [Shared backend](Backend.md) | Controllers/services/repositories, DTO mapping, security, transactions, validation/errors, audit, notifications and reporting |
| [Multi-tenancy](Multi-Tenancy.md) | Schema strategy, tenant lifecycle, JWT resolution, connection routing, global/local UATs, cross-tenant operations and limits |
| [Database](Database.md) | Current relational model, schema ownership, encryption/audit/deletion, evolution |
| [Development](Development.md) | Compose/native setup, independent frontend startup, environment variables, demo data, storage and troubleshooting |
| [Testing](Testing.md) | Existing backend/frontend suites, commands, coverage gaps, meaningful manual scenarios |
| [Implementation status](Implementation-Status.md) | Integrated, partial, backend-only, frontend-only, demonstration, historical and future distinctions |
| [Audit notes](Audit.md) | Scope, evidence, preservation policy, verification results and task boundaries |

## Source reference catalogs

| Reference | Coverage |
| --- | --- |
| [REST API](Reference/API.md) | All 42 controllers, 192 method-mapping annotations, and 200 method/path entries after aliases |
| [Models, DTOs and payloads](Reference/Domain.md) | 113 source files, 825 declared instance fields, enums, persistence/validation annotations |
| [Flyway migrations](Reference/Migrations.md) | All 71 global/tenant SQL scripts, ordered and linked |
| [Source and routes](Reference/Source-Inventory.md) | Independent application routes plus 608 audited source/configuration files |
| [Source hashes](Reference/Source-Hashes.json) | SHA-256 audit snapshot for those source/configuration files; no secret values |

Catalogs are inspection aids, not substitute implementation specifications or a claim of live execution. Functional guides explain the relationships and limits behind their entries.

## Preserved knowledge

[Historical documentation](Historical/README.md) retains complete original Romanian/English documents, branch decisions, agricultural register/domain specifications, person/household/GIS plans, tax research, roadmaps, security reports, diagrams, the original Word domain model, and mail/succession documentation. Original attributions remain in context. No recovery application code was restored.

The original current [succession document](Derived/succesiuni_notificari_documentatie.md) remains at its existing path with a source-verification notice. Its full pre-expansion version is also preserved. App-local READMEs retain useful CLI instructions while linking to current setup and limitations.

Historical legal references, performance targets, branch states, and requirements are explicitly historical. The current implementation does not establish full statutory coverage, official nationwide deployment, or production security readiness.
