# Testing and documentation verification

[Documentation index](README.md) · [Development](Development.md) · [Implementation status](Implementation-Status.md)

The repository has backend unit/controller/integration tests and independent frontend test configurations. Test presence and source inspection are distinguished from test execution. This documentation-only change does not claim a successful application build, passing full test suite, live email/signing delivery, or database migration run.

## Backend tests

Run from `src/backend`:

```powershell
mvn test
# Example focused service selection:
mvn '-Dtest=EvidentaServiceTest' test
```

| Test class / group | What its source exercises |
| --- | --- |
| `TenantServiceTest` | Null/duplicate input, schema naming, provisioning failures, orphan cleanup, migrate-all continuation |
| `UatServiceTest` | Global UAT CRUD, required/duplicate SIRUTA, tenant assignment/removal, claimed-UAT behavior |
| `EvidentaServiceTest` | Treatment total quantity, overdose justification, harvest pause, fertilizer substances, winter override, nitrogen threshold |
| `TenantControllerTest` | Super-admin versus admin/user/anonymous tenant operations |
| `UatControllerTest` | Global UAT CRUD responses and selected role restrictions |
| `UserControllerTest` | Global/tenant user lists, target tenant checks, creation/edit/delete and password-related behavior |
| `GdprAuditIntegrationTest` | Person view/list operations and access-log IDs |
| `MultiTenantEnversIntegrationTest` | Envers isolation across two tenant schemas |
| `ParcelaHistoryIntegrationTest` | Parcel change revisions and field differences |

Sources: [backend test tree](../src/backend/src/test/java/com/multitenant), [embedded database setup](../src/backend/src/test/java/com/multitenant/config/EmbeddedPostgresEnvironmentPostProcessor.java).

`EmbeddedPostgresEnvironmentPostProcessor`, registered under test `META-INF/spring.factories`, starts PostgreSQL on fixed **port 5433** and overrides the datasource. That port also belongs to the Compose database host mapping. Stop/adjust conflicting infrastructure before a full integration run. Spring context tests also load the application configuration, required crypto/JWT/mail properties, startup runner, and related infrastructure; they are not completely isolated mock-only tests.

Mockito/controller tests do not prove actual schema provisioning or live authorization for every endpoint. The chemical service tests must track constructor/dependency changes; their current mocks do not exhaustively cover newer production-cycle paths. Historical tests and names can refer to earlier payloads (`sirutaCode` versus `tenantId`). Treat actual current results as the authority.

## Public Institutions Portal tests

From `src/frontend`:

```powershell
npm test -- --watch=false --browsers=ChromeHeadless
```

`angular.json` uses Jasmine/Karma with Chrome launcher/coverage packages and references `tsconfig.spec.json`. **That configuration file is absent from this workspace.** The command is the intended entry point and may fail before running tests until application work repairs the test configuration.

Eight checked-in specifications cover creation of components including UAT banner/breadcrumbs, parcel map, building management, household list/form/detail, and UAT details. They are largely “should create” smoke tests. They do not establish role-guard coverage, server authorization, GIS accuracy, or all agricultural workflows.

## Citizens Portal tests

From `src/portal-cetateni`:

```powershell
npm test -- --watch=false
```

The Angular unit-test builder uses Vitest/jsdom. Five specification files cover creation of the root, home, application form, application history, and tracking components, plus a generated root title assertion. The title assertion and root template should be checked together before assuming the generated test remains current. HTTP/router/service dependencies in component smoke tests also require the corresponding test setup.

No configured end-to-end runner or cross-application browser workflow suite was found. Generated README `ng e2e` examples are scaffolding instructions and require installing/configuring an e2e tool first.

## Meaningful manual verification scenarios

For future application changes, use disposable local data and test both applications together:

1. Citizen registration/login/profile update; refresh session; logout; check guest restrictions and error messages.
2. Submit a application to a provisioned UAT, find it in the intended institution tenant, decide it, observe live history, and retrieve an accepted PDF.
3. Try the same numeric application ID across two tenants and verify ownership/tenant disambiguation; test public tracking separately.
4. Create/edit a person, memberships, household head, member history/document, land, parcel, and a child agricultural record; inspect parcel history.
5. Verify individual animal lifecycle constraints and a transfer including simulated destination failure/compensation; compare latest group snapshots.
6. Exercise active protected-space cycle, treatment dosage/pause validation, fertilizer override/threshold, and harvest calculations.
7. Compare report values with repository aggregation rules, including equal-date group snapshots, current inventories versus selected year, and duplicated vegetal area card inputs.
8. Check denied roles, unknown/inactive tenants, missing cookies, stale JWTs, public endpoints, and broker subscription access independently of hidden UI controls.

External SMTP/SignNow transactions require a deliberately configured test destination. They are not necessary to validate this documentation change.

## Verification for this documentation expansion

Documentation checks cover repository-local links/images/anchors in active guides, source-reference existence, API endpoint extraction against all controller mapping annotations, entity/DTO and migration coverage, screenshot inventory, historical preservation, and unchanged pre-existing application/configuration hashes. Mermaid blocks use GitHub-supported flowchart/sequence/ER syntax. Any parser/render tooling availability and actual validation results are recorded in [audit notes](Audit.md).

Application builds/tests were not run merely to verify Markdown changes, and no database, email service, signing provider, or running application state was mutated. Existing application test limitations are documented rather than fixed as part of this task.
