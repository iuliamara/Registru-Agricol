# Historical documentation collection

[Current documentation](../README.md) · [Current implementation status](../Implementation-Status.md) · [Preservation manifest](preservation-manifest.json)

This collection retains complete original explanations, Romanian specifications, diagrams, examples, user journeys, decisions, data dictionaries, and roadmaps from `C:/practica/Registru-Agricol-recovery/`, plus five snapshots of current documentation before expansion. No recovery application source was restored, merged, or modified.

**Status:** historical documents, not authoritative current implementation claims. Original legal references and branch-state claims were not revalidated as current legal advice or merged code. Current guides verify behavior against the active repository.

Recovered documents retain their full content and structure after a historical notice. Exceptions to byte-exact preservation are two redacted SMTP credential values in the mail report and the contextual standardization of English administrative terminology from “request” to “application.” Romanian text, quoted interface labels, source identifiers, and technical request terminology remain intact. Binary diagrams are unchanged; the Word model has one English terminology edit with all formatting and other package parts preserved. The manifest records original hashes, destinations, redaction counts, and terminology edits. Old machine-local links, removed-file references, and historical errors remain visible as part of the record; use current guides for working source links.

## Recommended reading

| Topic | Full originals | Current verified guide |
| --- | --- | --- |
| Register and proposed domain | [Register](Original/RegistruAgricol.md), [Word model](Original/Agricultural_Registry_Domain_Model.docx), [early overview](Archive/AgricultureRegisterV1.md) | [Database](../Database.md) |
| Person/household evolution | [Person model](Archive/PersonModel.md), [CRUD](Archive/Person_CRUD.md), [members](Derived/household-member-tracking.md), [household analysis](BusinessAnalysis/Gospodarie.md) | [Institutional guide](../Applications/Public-Institutions-Portal.md) |
| GIS/parcels | [GIS history](Archive/gospodarii_parcele_gis_documentation.md), [parcel requirements](BusinessAnalysis/Parcele.md) | [Current GIS](../Applications/Public-Institutions-Portal.md#gis-and-maps) |
| Initialization | [Database plan](Archive/plan_implementare_baza_date.md), [report](Archive/raport_modificari.md), [walkthrough](walkthrough.md) | [Tenancy](../Multi-Tenancy.md) |
| Succession/email | [Romanian succession](Derived/succesiuni_notificari_documentatie.md), [mail report](DOCUMENTATIE_MAIL_SI_MODIFICARI.md) | [Workflows](../Workflows.md) |
| Branch decisions | [BranchesDocumentation](BranchesDocumentation.md), [domain/use cases](DomeniuSiUseCases.md) | [Status](../Implementation-Status.md) |
| Roadmaps/fiscal research | [Original roadmap](Original/RoadmapRegistrulAgricol.md), [redefined roadmap](Archive/roadmap), [tax research](Original/ResearchTaxeImpozite.md) | [Future possibilities](../Implementation-Status.md#historical-requirements-and-future-possibilities) |

## Full recovered file catalog

| Recovery path | Preserved full file |
| --- | --- |
| `Docs/Archive/AgricultureRegisterChangeLogV1.1.md` | [Archive/AgricultureRegisterChangeLogV1.1.md](Archive/AgricultureRegisterChangeLogV1.1.md) |
| `Docs/Archive/AgricultureRegisterV1.md` | [Archive/AgricultureRegisterV1.md](Archive/AgricultureRegisterV1.md) |
| `Docs/Archive/gospodarii_parcele_gis_documentation.md` | [Archive/gospodarii_parcele_gis_documentation.md](Archive/gospodarii_parcele_gis_documentation.md) |
| `Docs/Archive/MODULES.md` | [Archive/MODULES.md](Archive/MODULES.md) |
| `Docs/Archive/Person_CRUD.md` | [Archive/Person_CRUD.md](Archive/Person_CRUD.md) |
| `Docs/Archive/PersonModel.md` | [Archive/PersonModel.md](Archive/PersonModel.md) |
| `Docs/Archive/plan_implementare_baza_date.md` | [Archive/plan_implementare_baza_date.md](Archive/plan_implementare_baza_date.md) |
| `Docs/Archive/raport_modificari.md` | [Archive/raport_modificari.md](Archive/raport_modificari.md) |
| `Docs/Archive/roadmap` | [Archive/roadmap](Archive/roadmap) |
| `Docs/BranchesDocumentation.md` | [BranchesDocumentation.md](BranchesDocumentation.md) |
| `Docs/Bugs/Lombok_JPA_Entities_Refactoring.md` | [Bugs/Lombok_JPA_Entities_Refactoring.md](Bugs/Lombok_JPA_Entities_Refactoring.md) |
| `Docs/Bugs/SecurityVulnerabilitiesFix.md` | [Bugs/SecurityVulnerabilitiesFix.md](Bugs/SecurityVulnerabilitiesFix.md) |
| `Docs/Bugs/sqli-after.png` | [Bugs/sqli-after.png](Bugs/sqli-after.png) |
| `Docs/Bugs/sqli-before-1.png` | [Bugs/sqli-before-1.png](Bugs/sqli-before-1.png) |
| `Docs/Bugs/sqli-before-2.png` | [Bugs/sqli-before-2.png](Bugs/sqli-before-2.png) |
| `Docs/Bugs/SQLInjectionFix.md` | [Bugs/SQLInjectionFix.md](Bugs/SQLInjectionFix.md) |
| `Docs/BusinessAnalysis/CarteFunciara.md` | [BusinessAnalysis/CarteFunciara.md](BusinessAnalysis/CarteFunciara.md) |
| `Docs/BusinessAnalysis/Cereri.md` | [BusinessAnalysis/Cereri.md](BusinessAnalysis/Cereri.md) |
| `Docs/BusinessAnalysis/Gospodarie.md` | [BusinessAnalysis/Gospodarie.md](BusinessAnalysis/Gospodarie.md) |
| `Docs/BusinessAnalysis/MembriiGospodarie.md` | [BusinessAnalysis/MembriiGospodarie.md](BusinessAnalysis/MembriiGospodarie.md) |
| `Docs/BusinessAnalysis/Parcele.md` | [BusinessAnalysis/Parcele.md](BusinessAnalysis/Parcele.md) |
| `Docs/BusinessAnalysis/Persoane_IdentityDocs.md` | [BusinessAnalysis/Persoane_IdentityDocs.md](BusinessAnalysis/Persoane_IdentityDocs.md) |
| `Docs/BusinessAnalysis/PortalCetateni.md` | [BusinessAnalysis/PortalCetateni.md](BusinessAnalysis/PortalCetateni.md) |
| `Docs/BusinessAnalysis/Terenuri.md` | [BusinessAnalysis/Terenuri.md](BusinessAnalysis/Terenuri.md) |
| `Docs/Derived/cultura-parcela.md` | [Derived/cultura-parcela.md](Derived/cultura-parcela.md) |
| `Docs/Derived/document-repository.md` | [Derived/document-repository.md](Derived/document-repository.md) |
| `Docs/Derived/entity-history-tracking.md` | [Derived/entity-history-tracking.md](Derived/entity-history-tracking.md) |
| `Docs/Derived/evidenta-pomi.md` | [Derived/evidenta-pomi.md](Derived/evidenta-pomi.md) |
| `Docs/Derived/gdpr-audit-logging.md` | [Derived/gdpr-audit-logging.md](Derived/gdpr-audit-logging.md) |
| `Docs/Derived/household-member-tracking.md` | [Derived/household-member-tracking.md](Derived/household-member-tracking.md) |
| `Docs/Derived/lookup-tables.md` | [Derived/lookup-tables.md](Derived/lookup-tables.md) |
| `Docs/Derived/statistici-export-excel.md` | [Derived/statistici-export-excel.md](Derived/statistici-export-excel.md) |
| `Docs/Derived/succesiuni_notificari_documentatie.md` | [Derived/succesiuni_notificari_documentatie.md](Derived/succesiuni_notificari_documentatie.md) |
| `Docs/Derived/sursa-apa.md` | [Derived/sursa-apa.md](Derived/sursa-apa.md) |
| `Docs/Derived/uat-frontend-context.md` | [Derived/uat-frontend-context.md](Derived/uat-frontend-context.md) |
| `Docs/DomeniuSiUseCases.md` | [DomeniuSiUseCases.md](DomeniuSiUseCases.md) |
| `Docs/Original/.env.example` | [Original/.env.example](Original/.env.example) |
| `Docs/Original/Agricultural_Registry_Domain_Model.docx` | [Original/Agricultural_Registry_Domain_Model.docx](Original/Agricultural_Registry_Domain_Model.docx) |
| `Docs/Original/AgricultureRegisterV1.2.md` | [Original/AgricultureRegisterV1.2.md](Original/AgricultureRegisterV1.2.md) |
| `Docs/Original/ANIMAL_MANAGEMENT_DOCS.md` | [Original/ANIMAL_MANAGEMENT_DOCS.md](Original/ANIMAL_MANAGEMENT_DOCS.md) |
| `Docs/Original/AuditDataPersonale.md` | [Original/AuditDataPersonale.md](Original/AuditDataPersonale.md) |
| `Docs/Original/CategorieFolosinta.md` | [Original/CategorieFolosinta.md](Original/CategorieFolosinta.md) |
| `Docs/Original/CodeReview-Carina.md` | [Original/CodeReview-Carina.md](Original/CodeReview-Carina.md) |
| `Docs/Original/EnumStorageResearch.md` | [Original/EnumStorageResearch.md](Original/EnumStorageResearch.md) |
| `Docs/Original/ExportStatistici.md` | [Original/ExportStatistici.md](Original/ExportStatistici.md) |
| `Docs/Original/Local_Development_Guide.md` | [Original/Local_Development_Guide.md](Original/Local_Development_Guide.md) |
| `Docs/Original/mermaid-diagram-2026-05-29.png` | [Original/mermaid-diagram-2026-05-29.png](Original/mermaid-diagram-2026-05-29.png) |
| `Docs/Original/raport_contract_utilizare.md` | [Original/raport_contract_utilizare.md](Original/raport_contract_utilizare.md) |
| `Docs/Original/raport_scheduler_contracte.md` | [Original/raport_scheduler_contracte.md](Original/raport_scheduler_contracte.md) |
| `Docs/Original/README.md` | [Original/README.md](Original/README.md) |
| `Docs/Original/RegistruAgricol.md` | [Original/RegistruAgricol.md](Original/RegistruAgricol.md) |
| `Docs/Original/ResearchTaxeImpozite.md` | [Original/ResearchTaxeImpozite.md](Original/ResearchTaxeImpozite.md) |
| `Docs/Original/RoadmapRegistrulAgricol.md` | [Original/RoadmapRegistrulAgricol.md](Original/RoadmapRegistrulAgricol.md) |
| `Docs/Original/security_and_code_review.md` | [Original/security_and_code_review.md](Original/security_and_code_review.md) |
| `Docs/Original/SoilTypeDocumentation.md` | [Original/SoilTypeDocumentation.md](Original/SoilTypeDocumentation.md) |
| `DOCUMENTATIE_MAIL_SI_MODIFICARI.md` | [DOCUMENTATIE_MAIL_SI_MODIFICARI.md](DOCUMENTATIE_MAIL_SI_MODIFICARI.md) |
| `walkthrough.md` | [walkthrough.md](walkthrough.md) |
| `README.md` | [recovery-root-README.md](recovery-root-README.md) |

## Pre-expansion current documentation

Snapshots retain original text independently from expanded versions:

- [pre-expansion/Docs/Derived/succesiuni_notificari_documentatie.md](pre-expansion/Docs/Derived/succesiuni_notificari_documentatie.md)
- [pre-expansion/README.md](pre-expansion/README.md)
- [pre-expansion/src/frontend/leaflet-esm-wrapper.md](pre-expansion/src/frontend/leaflet-esm-wrapper.md)
- [pre-expansion/src/frontend/README.md](pre-expansion/src/frontend/README.md)
- [pre-expansion/src/portal-cetateni/README.md](pre-expansion/src/portal-cetateni/README.md)

The branch document retains author/branch attribution in its original context. It does not establish sole authorship of the platform or any remote branch state today.
