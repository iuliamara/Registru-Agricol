# Documentation audit and verification

[Documentation index](README.md) · [Source inventory](Reference/Source-Inventory.md) · [Implementation status](Implementation-Status.md) · [Historical collection](Historical/README.md)

The documentation expansion was based on the current working-tree implementation on **25 November 2026**, at repository HEAD `f4b39c0`. The active repository is authoritative; the accessible recovery directory was used only for historical documentation and assets. No recovery application code was copied or merged.

## Scope and evidence

The recursive inventory covered both independent Angular applications, the shared Java backend, SQL migrations, templates, tests, configuration, existing Markdown, and supplied screenshots. Dependencies, generated build outputs, caches, Git internals, compiled `.class` artifacts, runtime logs/uploads, and private `.env` contents were excluded from implementation documentation.

| Evidence set | Audit coverage |
| --- | --- |
| Source/configuration inventory | 608 files, approximately 3.95 million text characters, including lockfiles/configuration |
| Java | 278 files, including controllers/services/repositories/models/DTOs/security/config/events/aspects and tests |
| TypeScript | 138 files across the two frontends, including routes/pages/components/services/models/guards/interceptors/specifications |
| Templates/styles | 58 HTML, 31 CSS, and 3 SCSS files; application, email and PDF templates |
| API | 42 controllers, 192 method-mapping declarations, 200 expanded method/path entries including aliases |
| Data dictionary | 113 model/DTO/payload files, 825 instance fields, top-level/nested enums, plus the service-defined animal transfer record |
| Database migrations | 71 SQL scripts across public and tenant locations |
| Geographic reference data | Bundled UAT lists and 3,243-line `siruta.csv` |
| Current documentation | All five pre-existing Markdown documents inspected and snapshotted before expansion |
| Current screenshots | All 21 supplied PNG screenshots inspected; six citizen and fifteen institutional images |
| Recovery documentation/assets | 58 files preserved, including full Romanian/English histories, diagrams, Word model, mail report and walkthrough |

Source traces connect frontend routes/actions to HTTP consumers, controller rules, services, entity relationships, repository queries, and migrations. Dependencies were distinguished from active use: for example, the PostGIS image and spatial Maven declarations do not override current JSONB geometry or frontend coordinate conversion.

The catalogs supplement narrative explanations rather than replacing them. [API](Reference/API.md) retains method inputs and effective annotations; [Domain](Reference/Domain.md) lists fields and mapping/validation declarations; [Migrations](Reference/Migrations.md) preserves every script link; [Source inventory](Reference/Source-Inventory.md) covers the application units.

## Findings incorporated into the documentation

- Separate Angular 21 citizen and Angular 18 institutional applications with a shared Spring Boot backend.
- Super-admin and tenant-admin interfaces are sections of the institutional frontend.
- Schema-per-tenant database routing, shared global account/UAT tables, and deliberate cross-schema operations.
- Additional agricultural modules beyond the supplied screenshots, including protected production, harvests, forestry, resources, and household histories.
- `pantries.png` means households; `treatments.png` means plant-protection/fertilization; `affidavit-request.png` means certificate applications.
- Current security/authorization boundaries, public application routes, no institutional route guards, and WebSocket/storage limitations.
- Incomplete tenant-UAT actions, dashboard placeholders, role asymmetries, PDF ID ambiguity, and other partial integrations.
- Correction of older claims about GIS persistence, succession schema/migrations, asynchronous email, CSV reports, and midnight scheduling.

The [status register](Implementation-Status.md) distinguishes integrated source, partial integration, backend-only operations, frontend-only placeholders, demo data, historical specifications, and future possibilities.

## Preservation policy and verification

Historical documents were not condensed into gap tables. Their full content, data dictionaries, examples, diagrams, user journeys, attribution, and decisions remain in [Historical](Historical/README.md), with a historical-status notice. Binary diagrams remain unchanged. Two SMTP credential values in the historical mail report were redacted while preserving its explanation and code structure. A later terminology pass standardized English administrative applications across current and historical prose, diagrams, and captions; it preserved Romanian wording, quoted interface labels, technical request terminology, and source identifiers. The Word model has one English text substitution, with formatting XML and other package members unchanged.

[The preservation manifest](Historical/preservation-manifest.json) records each recovery-relative source, original SHA-256, preserved destination, redaction count, and any subsequent terminology substitutions. Preservation comparisons account only for these declared edits and the added historical notice. The recovery originals themselves remain untouched. Old machine-local/branch-specific links remain intentionally in original bodies. The curated historical index provides working navigation.

Five pre-expansion snapshots also retain the original current README, both app READMEs, Leaflet wrapper note, and Romanian succession document. The active succession file retains its complete content with corrections added above it. App-local CLI guidance remains available with corrected scope/testing notes.

## Documentation checks

Checks performed for this change include:

1. Active Markdown local links, source references, HTML image sources, image paths, and heading anchors resolve; code examples and original historical bodies are treated according to their context.
2. Every supplied screenshot is linked/embedded in the correct application guide and indexed; no screenshot binary was modified.
3. API coverage matches all controller method mappings and aliases; model/DTO/payload and migration catalogs cover their source sets.
4. Historical preservation matches the originals, except the declared credential/English terminology substitutions and added status notices.
5. [Source hashes](Reference/Source-Hashes.json) match the audited application/configuration files after documentation edits. Existing local application changes were preserved.
6. Git diff whitespace/error checks apply to tracked documentation edits. All added deliverables are documentation, historical documentation assets, or reference metadata.
7. New Mermaid blocks use GitHub flowchart, sequence, and ER syntax with explicit application, database, role/context, and integration boundaries. They were structurally checked; no live GitHub renderer or local Mermaid parser was available for rendering them.

Machine-readable counts/results are in [Validation.json](Reference/Validation.json). Application tests/builds were not run for these documentation-only edits. No database migration, data reset, production deployment, email send, or SignNow invitation was performed. [Testing](Testing.md) describes actual test infrastructure and its pre-existing limitations. The terminology pass also checked all Markdown/extensionless historical prose, internal heading links, retained technical usages, unchanged source/screenshot hashes, and the Word package structure. Word visual rendering was attempted but could not run because LibreOffice is unavailable; this limit is recorded separately from the successful structural checks.

## Maintenance

When application behavior changes, update the relevant functional guide and implementation-status entry together. Recheck frontend binding, controller authorization, tenant resolution, service rules, and migration before promoting a feature to integrated status. Regenerate/update source-reference catalogs and their hashes only from the authoritative current source. Keep historical originals separate, including their attribution and original language.
