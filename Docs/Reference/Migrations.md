# Flyway migration catalog

[Documentation index](../README.md) · [Database evolution](../Database.md) · [Tenant lifecycle](../Multi-Tenancy.md)

All checked-in SQL files from both Flyway locations are listed below. Versions are ordered numerically with underscore components; gaps and fractional versions are preserved. Global and tenant migration policies differ as documented in the linked guides. These files were inspected, not executed or modified.

## Global public schema

| Version and script | DDL targets / purpose from source |
| --- | --- |
| [V1__init_public_schema.sql](../../src/backend/src/main/resources/db/migration/V1__init_public_schema.sql) | init public schema — `public.tenants`, `public.users` |
| [V2__update_superadmin_password.sql](../../src/backend/src/main/resources/db/migration/V2__update_superadmin_password.sql) | update superadmin password — data/extension/migration operations; see script |
| [V3__create_public_uat_table.sql](../../src/backend/src/main/resources/db/migration/V3__create_public_uat_table.sql) | create public uat table — `public.uat` |
| [V4__add_user_profile_columns.sql](../../src/backend/src/main/resources/db/migration/V4__add_user_profile_columns.sql) | add user profile columns — `public.users` |
| [V6__add_lookup_tables.sql](../../src/backend/src/main/resources/db/migration/V6__add_lookup_tables.sql) | add lookup tables — `public.tip_sol`, `public.categorie_folosinta_ref`, `public.tip_sursa_apa` |
| [V7__populate_all_romanian_localities.sql](../../src/backend/src/main/resources/db/migration/V7__populate_all_romanian_localities.sql) | populate all romanian localities — data/extension/migration operations; see script |
| [V8__rename_public_tables_to_plural.sql](../../src/backend/src/main/resources/db/migration/V8__rename_public_tables_to_plural.sql) | rename public tables to plural — `public.uat`, `public.crotal_registry`, `public.tip_sol`, `public.categorie_folosinta_ref`, `public.tip_sursa_apa` |
| [V9__create_tip_document_table.sql](../../src/backend/src/main/resources/db/migration/V9__create_tip_document_table.sql) | create tip document table — `public.tip_document` |
| [V10__global_crotal_registry.sql](../../src/backend/src/main/resources/db/migration/V10__global_crotal_registry.sql) | global crotal registry — `public.crotal_registry` |
| [V11__create_cetateni_table.sql](../../src/backend/src/main/resources/db/migration/V11__create_cetateni_table.sql) | create cetateni table — `public.cetateni` |
| [V12__encrypt_cetateni_cnp.sql](../../src/backend/src/main/resources/db/migration/V12__encrypt_cetateni_cnp.sql) | encrypt cetateni cnp — `public.cetateni` |
| [V13__create_specii_pom_lookup_table.sql](../../src/backend/src/main/resources/db/migration/V13__create_specii_pom_lookup_table.sql) | create specii pom lookup table — `specii_pomi` |
| [V14__add_soft_delete_to_core_tables.sql](../../src/backend/src/main/resources/db/migration/V14__add_soft_delete_to_core_tables.sql) | add soft delete to core tables — `cetateni`, `uats`, `tenants`, `users` |
| [V15__add_tip_persoana_to_cetateni.sql](../../src/backend/src/main/resources/db/migration/V15__add_tip_persoana_to_cetateni.sql) | add tip persoana to cetateni — `public.cetateni` |
| [V16__add_atestat_flags_to_cetateni.sql](../../src/backend/src/main/resources/db/migration/V16__add_atestat_flags_to_cetateni.sql) | add atestat flags to cetateni — `public.cetateni` |

## Tenant schemas

| Version and script | DDL targets / purpose from source |
| --- | --- |
| [V1__init_tenant_schema.sql](../../src/backend/src/main/resources/db/tenant/V1__init_tenant_schema.sql) | init tenant schema — `uat`, `gospodarie` |
| [V2__create_person_tables.sql](../../src/backend/src/main/resources/db/tenant/V2__create_person_tables.sql) | create person tables — `persons`, `identity_documents`, `person_relations` |
| [V3__add_register_columns_to_persons.sql](../../src/backend/src/main/resources/db/tenant/V3__add_register_columns_to_persons.sql) | add register columns to persons — `persons` |
| [V4__update_gospodarie_adresa.sql](../../src/backend/src/main/resources/db/tenant/V4__update_gospodarie_adresa.sql) | update gospodarie adresa — `gospodarie` |
| [V5__create_parcele_table.sql](../../src/backend/src/main/resources/db/tenant/V5__create_parcele_table.sql) | create parcele table — `parcele` |
| [V6__create_teren_table.sql](../../src/backend/src/main/resources/db/tenant/V6__create_teren_table.sql) | create teren table — `teren`, `parcele` |
| [V7__link_person_to_gospodarie.sql](../../src/backend/src/main/resources/db/tenant/V7__link_person_to_gospodarie.sql) | link person to gospodarie — `persons` |
| [V9__fix_uat_foreign_keys.sql](../../src/backend/src/main/resources/db/tenant/V9__fix_uat_foreign_keys.sql) | fix uat foreign keys — `gospodarie` |
| [V10__update_teren_schema.sql](../../src/backend/src/main/resources/db/tenant/V10__update_teren_schema.sql) | update teren schema — `teren` |
| [V11__create_categorie_folosinta_table.sql](../../src/backend/src/main/resources/db/tenant/V11__create_categorie_folosinta_table.sql) | create categorie folosinta table — `categorie_folosinta` |
| [V12__create_utilaje_table.sql](../../src/backend/src/main/resources/db/tenant/V12__create_utilaje_table.sql) | create utilaje table — `utilaje` |
| [V13__create_cladire_table.sql](../../src/backend/src/main/resources/db/tenant/V13__create_cladire_table.sql) | create cladire table — `cladiri` |
| [V14__create_animal_tables.sql](../../src/backend/src/main/resources/db/tenant/V14__create_animal_tables.sql) | create animal tables — `animal_individual`, `efectiv_grup` |
| [V15__create_eveniment_animal_table.sql](../../src/backend/src/main/resources/db/tenant/V15__create_eveniment_animal_table.sql) | create eveniment animal table — `eveniment_animal` |
| [V16__animal_module_improvements.sql](../../src/backend/src/main/resources/db/tenant/V16__animal_module_improvements.sql) | animal module improvements — `eveniment_animal`, `efectiv_grup` |
| [V16_1__fix_parcele_polygon_type.sql](../../src/backend/src/main/resources/db/tenant/V16_1__fix_parcele_polygon_type.sql) | fix parcele polygon type — `parcele` |
| [V17__create_cultura_parcela_table.sql](../../src/backend/src/main/resources/db/tenant/V17__create_cultura_parcela_table.sql) | create cultura parcela table — `cultura_parcela` |
| [V18__rename_gospodarie_id_to_teren_id_parcele.sql](../../src/backend/src/main/resources/db/tenant/V18__rename_gospodarie_id_to_teren_id_parcele.sql) | rename gospodarie id to teren id parcele — `parcele` |
| [V19__create_contract_utilizare_table.sql](../../src/backend/src/main/resources/db/tenant/V19__create_contract_utilizare_table.sql) | create contract utilizare table — `contract_utilizare` |
| [V20__create_surse_apa_table.sql](../../src/backend/src/main/resources/db/tenant/V20__create_surse_apa_table.sql) | create surse apa table — `surse_apa` |
| [V21__persoana_gospodarii_many_to_many.sql](../../src/backend/src/main/resources/db/tenant/V21__persoana_gospodarii_many_to_many.sql) | persoana gospodarii many to many — `persoana_gospodarie`, `persons` |
| [V21_1__recreate_contract_utilizare_if_missing.sql](../../src/backend/src/main/resources/db/tenant/V21_1__recreate_contract_utilizare_if_missing.sql) | recreate contract utilizare if missing — `contract_utilizare` |
| [V22__fix_utilizator_operare_fk.sql](../../src/backend/src/main/resources/db/tenant/V22__fix_utilizator_operare_fk.sql) | fix utilizator operare fk — `contract_utilizare` |
| [V23__rename_tenant_tables_to_plural.sql](../../src/backend/src/main/resources/db/tenant/V23__rename_tenant_tables_to_plural.sql) | rename tenant tables to plural — `gospodarie`, `teren`, `categorie_folosinta`, `animal_individual`, `efectiv_grup`, `eveniment_animal`, `cultura_parcela`, `contract_utilizare`, `persoana_gospodarie` |
| [V24__rename_tenant_uat_to_uats.sql](../../src/backend/src/main/resources/db/tenant/V24__rename_tenant_uat_to_uats.sql) | rename tenant uat to uats — `uat` |
| [V25__create_document_table.sql](../../src/backend/src/main/resources/db/tenant/V25__create_document_table.sql) | create document table — `document` |
| [V26__rename_document_table_to_plural.sql](../../src/backend/src/main/resources/db/tenant/V26__rename_document_table_to_plural.sql) | rename document table to plural — `document` |
| [V27__contract_utilizare_teren_to_parcela.sql](../../src/backend/src/main/resources/db/tenant/V27__contract_utilizare_teren_to_parcela.sql) | contract utilizare teren to parcela — `contracte_utilizare` |
| [V28__add_data_inregistrare_to_efective_grup.sql](../../src/backend/src/main/resources/db/tenant/V28__add_data_inregistrare_to_efective_grup.sql) | add data inregistrare to efective grup — `efective_grup` |
| [V29__add_destinatar_tenant_id_to_evenimente_animale.sql](../../src/backend/src/main/resources/db/tenant/V29__add_destinatar_tenant_id_to_evenimente_animale.sql) | add destinatar tenant id to evenimente animale — `evenimente_animale` |
| [V30__create_carte_funciara_table.sql](../../src/backend/src/main/resources/db/tenant/V30__create_carte_funciara_table.sql) | create carte funciara table — `carti_funciare` |
| [V31__extend_parcele_cf_fields.sql](../../src/backend/src/main/resources/db/tenant/V31__extend_parcele_cf_fields.sql) | extend parcele cf fields — `parcele` |
| [V32__create_gdpr_audit_log_table.sql](../../src/backend/src/main/resources/db/tenant/V32__create_gdpr_audit_log_table.sql) | create gdpr audit log table — `gdpr_audit_logs` |
| [V33__create_envers_audit_tables.sql](../../src/backend/src/main/resources/db/tenant/V33__create_envers_audit_tables.sql) | create envers audit tables — `revinfo`, `gospodarii_aud`, `cladiri_aud`, `parcele_aud` |
| [V34__create_cereri_table.sql](../../src/backend/src/main/resources/db/tenant/V34__create_cereri_table.sql) | create cereri table — `cereri` |
| [V35__add_cnp_cui_to_cereri.sql](../../src/backend/src/main/resources/db/tenant/V35__add_cnp_cui_to_cereri.sql) | add cnp cui to cereri — `cereri` |
| [V36__add_persons_and_teren_to_envers.sql](../../src/backend/src/main/resources/db/tenant/V36__add_persons_and_teren_to_envers.sql) | add persons and teren to envers — `persons_aud`, `terenuri_aud` |
| [V37__encrypt_cnp_cui.sql](../../src/backend/src/main/resources/db/tenant/V37__encrypt_cnp_cui.sql) | encrypt cnp cui — `persons`, `persons_aud` |
| [V38__encrypt_cereri_cnpcui.sql](../../src/backend/src/main/resources/db/tenant/V38__encrypt_cereri_cnpcui.sql) | encrypt cereri cnpcui — `cereri` |
| [V39__create_pomi_table.sql](../../src/backend/src/main/resources/db/tenant/V39__create_pomi_table.sql) | create pomi table — `pomi` |
| [V40__create_vita_de_vie_table.sql](../../src/backend/src/main/resources/db/tenant/V40__create_vita_de_vie_table.sql) | create vita de vie table — `vita_de_vie` |
| [V41__create_pasuni_fanete_table.sql](../../src/backend/src/main/resources/db/tenant/V41__create_pasuni_fanete_table.sql) | create pasuni fanete table — `pasuni_fanete` |
| [V42__add_soft_delete_to_tenant_tables.sql](../../src/backend/src/main/resources/db/tenant/V42__add_soft_delete_to_tenant_tables.sql) | add soft delete to tenant tables — `vita_de_vie`, `terenuri`, `surse_apa`, `pomi`, `pasuni_fanete`, `parcele`, `utilaje`, `gospodarii`, `documente`, `culturi_parcele`, `contracte_utilizare`, `cladiri`, `cereri`, `categorii_folosinta`, `carti_funciare`, `person_relations`, `identity_documents`, `persons`, `uats`, `animale_individuale`, `evenimente_animale`, `efective_grup`, `gospodarii_aud`, `cladiri_aud`, `parcele_aud`, `persons_aud`, `terenuri_aud` |
| [V43__add_atestate_si_carnete.sql](../../src/backend/src/main/resources/db/tenant/V43__add_atestate_si_carnete.sql) | add atestate si carnete — `atestate_producator`, `carnete_comercializare`, `atestate_producator_aud`, `carnete_comercializare_aud`, `cereri` |
| [V43_1__create_evidenta_pesticide_ingrasaminte.sql](../../src/backend/src/main/resources/db/tenant/V43_1__create_evidenta_pesticide_ingrasaminte.sql) | create evidenta pesticide ingrasaminte — `catalog_ppp`, `catalog_ingrasaminte`, `tratamente_fitosanitare`, `fertilizari`, `catalog_ppp_aud`, `catalog_ingrasaminte_aud`, `tratamente_fitosanitare_aud`, `fertilizari_aud` |
| [V44__add_created_at_to_audit_tables.sql](../../src/backend/src/main/resources/db/tenant/V44__add_created_at_to_audit_tables.sql) | add created at to audit tables — `atestate_producator_aud`, `carnete_comercializare_aud` |
| [V45__modul_separare_productie.sql](../../src/backend/src/main/resources/db/tenant/V45__modul_separare_productie.sql) | modul separare productie — `parcele`, `parcele_aud`, `cicluri_productie`, `cicluri_productie_aud`, `factori_mediu`, `recoltari`, `recoltari_aud`, `tratamente_fitosanitare`, `tratamente_fitosanitare_aud`, `fertilizari`, `fertilizari_aud` |
| [V45_2__add_head_of_household_and_member_history.sql](../../src/backend/src/main/resources/db/tenant/V45_2__add_head_of_household_and_member_history.sql) | add head of household and member history — `persons`, `persons_aud`, `gospodarii`, `gospodarii_aud`, `istoric_membri_gospodarie`, `istoric_membri_gospodarie_aud` |
| [V46__create_evidenta_pesticide_ingrasaminte.sql](../../src/backend/src/main/resources/db/tenant/V46__create_evidenta_pesticide_ingrasaminte.sql) | create evidenta pesticide ingrasaminte — `catalog_ppp`, `catalog_ingrasaminte`, `tratamente_fitosanitare`, `fertilizari`, `catalog_ppp_aud`, `catalog_ingrasaminte_aud`, `tratamente_fitosanitare_aud`, `fertilizari_aud` |
| [V47__add_semnatura_electronica_contract_utilizare.sql](../../src/backend/src/main/resources/db/tenant/V47__add_semnatura_electronica_contract_utilizare.sql) | add semnatura electronica contract utilizare — `contracte_utilizare` |
| [V48__redrop_utilizator_operare_fk.sql](../../src/backend/src/main/resources/db/tenant/V48__redrop_utilizator_operare_fk.sql) | redrop utilizator operare fk — `contracte_utilizare` |
| [V49__add_signnow_contract_utilizare.sql](../../src/backend/src/main/resources/db/tenant/V49__add_signnow_contract_utilizare.sql) | add signnow contract utilizare — `contracte_utilizare` |
| [V50__create_paduri_table.sql](../../src/backend/src/main/resources/db/tenant/V50__create_paduri_table.sql) | create paduri table — `paduri`, `paduri_aud` |
| [V51__add_missing_V45_columns.sql](../../src/backend/src/main/resources/db/tenant/V51__add_missing_V45_columns.sql) | add missing V45 columns — `parcele`, `parcele_aud`, `cicluri_productie`, `cicluri_productie_aud`, `factori_mediu`, `recoltari`, `recoltari_aud`, `tratamente_fitosanitare`, `tratamente_fitosanitare_aud`, `fertilizari`, `fertilizari_aud` |
| [V52__add_document_to_member_history.sql](../../src/backend/src/main/resources/db/tenant/V52__add_document_to_member_history.sql) | add document to member history — `istoric_membri_gospodarie`, `istoric_membri_gospodarie_aud` |
| [V53__notificari_succesiuni.sql](../../src/backend/src/main/resources/db/tenant/V53__notificari_succesiuni.sql) | notificari succesiuni — `persons`, `persons_aud`, `notificari_succesiuni` |

