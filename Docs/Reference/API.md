# REST API reference

[Documentation index](../README.md) · [Backend conventions](../Backend.md) · [Fields and payloads](Domain.md)

Source-derived catalog of every active controller mapping. Paths include all class-level aliases. Input signatures retain query/body/path annotations and defaults; the linked controller remains authoritative for response types and manual checks. This is static source documentation, not a live API test or generated OpenAPI contract.

## Authentication and response conventions

The HTTP filter permits `/api/auth/**`, `/api/public/**`, and `/api/ws/**`; other paths require authentication. Class/method rules below apply in addition. Method `@PreAuthorize` overrides a class expression where present. `@TenantRequired` rejects public context on annotated tenant operations. “No additional method expression” does not mean anonymous access unless the HTTP path is permitted. Public profile/history/status/PDF methods also perform explicit principal/owner checks in their bodies.

Use same-origin cookies (`jwt` institutional, `jwt_cetatean` citizen); the filter also supports Bearer fallback. Do not send tenant headers to select schemas. Tenant domain routes use the JWT context; public application routes resolve a global UAT. See [multi-tenancy](../Multi-Tenancy.md).

List endpoints vary between arrays and Spring Page objects. Pageable parameters normally use `page`, `size`, and `sort`; inspect each signature. Errors vary between field maps, `message` maps, text, and Spring error bodies. Downloads return PDFs, actual XLSX bytes, or resources. No universal envelope is implemented.

Example institutional status update: `PUT /api/admin/cereri/42/status?status=ACCEPTED` with the institutional cookie. Application types/statuses and field constraints are listed in [Domain](Domain.md); synthetic HTTP request JSON body is in [Workflows](../Workflows.md).

## AdeverintaController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/AdeverintaController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/v1/adeverinte/rol-agricol/{gospodarieId}/persoana/{persoanaId}` | `generateAdeverintaRolAgricol(@PathVariable Long gospodarieId, @PathVariable Long persoanaId)` | Inherits class / HTTP rule |

## AdminCerereController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/AdminCerereController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/admin/cereri` | `getAllCereri()` | `hasAnyRole('ADMIN', 'USER')` |
| PUT | `/api/admin/cereri/{id}/status` | `updateStatus(@PathVariable Long id, @RequestParam StatusCerere status)` | `hasAnyRole('ADMIN', 'USER')` |

## AnimalController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/AnimalController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/animals/individual` | `getAllIndividuals(Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/animals/individual/{id}` | `getIndividualById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/animals/individual` | `createIndividual(@RequestBody AnimalIndividual animal)` | Inherits class / HTTP rule |
| PUT | `/api/animals/individual/{id}` | `updateIndividual(@PathVariable Long id, @RequestBody AnimalIndividual animal)` | Inherits class / HTTP rule |
| DELETE | `/api/animals/individual/{id}` | `deleteIndividual(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/animals/individual/{id}/evenimente` | `adaugaEveniment(@PathVariable Long id, @RequestBody EvenimentAnimal eveniment)` | Inherits class / HTTP rule |
| GET | `/api/animals/individual/{id}/evenimente` | `getTimeline(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/animals/individual/{id}/transfer` | `transferAnimal(@PathVariable Long id, @RequestBody CrossTenantTransferService.TransferRequest request)` | Inherits class / HTTP rule |
| GET | `/api/animals/grup` | `getAllGroups(Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/animals/grup/{id}` | `getGroupById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/animals/grup` | `createGroup(@RequestBody EfectivGrup grup)` | Inherits class / HTTP rule |
| POST | `/api/animals/grup/{id}/snapshot` | `addGrupSnapshot(@PathVariable Long id, @RequestBody EfectivGrup grup)` | Inherits class / HTTP rule |
| GET | `/api/animals/grup/{gospodarieId}/history` | `getGrupHistory(@PathVariable Long gospodarieId, Pageable pageable)` | Inherits class / HTTP rule |
| DELETE | `/api/animals/grup/{id}` | `deleteGroup(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/animals/proprietar/{proprietarId}` | `getAnimalsByProprietar(@PathVariable Long proprietarId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/animals/gospodarie/{gospodarieId}` | `getAnimalsByGospodarie(@PathVariable Long gospodarieId, Pageable pageable)` | Inherits class / HTTP rule |

## AtestatController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/AtestatController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/public/atestate/my-status` | `getMyStatus()` | Inherits class / HTTP rule |

## AuthController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/AuthController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/auth/me` | `getCurrentUser()` | Inherits class / HTTP rule |
| POST | `/api/auth/signin` | `authenticateUser(@RequestBody LoginRequest loginRequest)` | Inherits class / HTTP rule |
| POST | `/api/auth/impersonate` | `impersonateTenant(@RequestBody ImpersonateRequest request)` | `hasRole('ROLE_SUPER_ADMIN')` |
| POST | `/api/auth/signout` | `logoutUser()` | Inherits class / HTTP rule |

## CarteFunciaraController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CarteFunciaraController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/carti-funciare/teren/{terenId}` | `getByTerenId(@PathVariable Long terenId)` | Inherits class / HTTP rule |
| PUT | `/api/carti-funciare/{id}` | `updateCf(@PathVariable Long id, @Valid @RequestBody CarteFunciaraDTO dto)` | Inherits class / HTTP rule |

## CatalogIngrasaminteController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CatalogIngrasaminteController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/catalog/ingrasaminte` | `getCatalog(@RequestParam(value = "query", required = false) String query, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/catalog/ingrasaminte/{id}` | `getById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/catalog/ingrasaminte` | `create(@RequestBody CatalogIngrasaminteDTO dto)` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN')` |
| PUT | `/api/catalog/ingrasaminte/{id}` | `update(@PathVariable Long id, @RequestBody CatalogIngrasaminteDTO dto)` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN')` |
| DELETE | `/api/catalog/ingrasaminte/{id}` | `delete(@PathVariable Long id)` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN')` |

## CatalogPppController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CatalogPppController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/catalog/ppp` | `getCatalog(@RequestParam(value = "query", required = false) String query, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/catalog/ppp/{id}` | `getById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/catalog/ppp` | `create(@RequestBody CatalogPppDTO dto)` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN')` |
| PUT | `/api/catalog/ppp/{id}` | `update(@PathVariable Long id, @RequestBody CatalogPppDTO dto)` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN')` |
| DELETE | `/api/catalog/ppp/{id}` | `delete(@PathVariable Long id)` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN')` |

## CategorieFolosintaController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CategorieFolosintaController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/terenuri/{terenId}/categorii-folosinta` | `getCategoriiForTeren(@PathVariable Long terenId, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/terenuri/{terenId}/categorii-folosinta` | `createCategorie(@PathVariable Long terenId, @RequestBody CategorieFolosinta categorie)` | Inherits class / HTTP rule |
| PUT | `/api/categorii-folosinta/{id}` | `updateCategorie(@PathVariable Long id, @RequestBody CategorieFolosinta categorie)` | Inherits class / HTTP rule |
| DELETE | `/api/categorii-folosinta/{id}` | `deleteCategorie(@PathVariable Long id)` | Inherits class / HTTP rule |

## CerereController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CerereController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| POST | `/api/public/cereri` | `submitCerere(@RequestBody CerereDTO cerereDTO)` | Inherits class / HTTP rule |
| GET | `/api/public/cereri/{codCerere}` | `checkStatus(@PathVariable String codCerere, @RequestParam Long uatId)` | Inherits class / HTTP rule |
| GET | `/api/public/cereri/my-cereri` | `getMyCereri()` | Inherits class / HTTP rule |
| GET | `/api/public/cereri/by-cnp/{cnp}` | `getByCnp(@PathVariable String cnp, @RequestParam Long uatId)` | Inherits class / HTTP rule |

## CererePdfController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CererePdfController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/public/cereri/{id}/pdf` | `downloadCererePdf(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/admin/cereri/{id}/pdf` | `downloadCererePdf(@PathVariable Long id)` | Inherits class / HTTP rule |

## CetateanAuthController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CetateanAuthController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| POST | `/api/public/cetatean/register` | `registerCetatean(@Valid @RequestBody CetateanSignupRequest request)` | Inherits class / HTTP rule |
| POST | `/api/public/cetatean/login` | `loginCetatean(@Valid @RequestBody CetateanLoginRequest request)` | Inherits class / HTTP rule |
| GET | `/api/public/cetatean/me` | `getCurrentCetatean()` | Inherits class / HTTP rule |
| POST | `/api/public/cetatean/signout` | `logoutCetatean()` | Inherits class / HTTP rule |
| PUT | `/api/public/cetatean/me` | `updateCurrentCetatean(@Valid @RequestBody CetateanUpdateRequest request)` | Inherits class / HTTP rule |

## CicluProductieController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CicluProductieController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/cicluri-productie/parcela/{parcelaId}` | `getCicluriByParcela(@PathVariable Long parcelaId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/cicluri-productie/{id}` | `getCicluById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/cicluri-productie` | `createCiclu(@Valid @RequestBody CicluProductieDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/cicluri-productie/{id}` | `updateCiclu(@PathVariable Long id, @Valid @RequestBody CicluProductieDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/cicluri-productie/{id}` | `deleteCiclu(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/cicluri-productie/export/pdf` | `exportPdf(@RequestParam(required = false) Integer anAgricol)` | Inherits class / HTTP rule |

## CladireController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CladireController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/gospodarii/{gospodarieId}/cladiri` | `getCladiri(@PathVariable Long gospodarieId, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/gospodarii/{gospodarieId}/cladiri` | `createCladire(@PathVariable Long gospodarieId, @RequestBody CladireDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/gospodarii/{gospodarieId}/cladiri/{id}` | `updateCladire(@PathVariable Long gospodarieId, @PathVariable Long id, @RequestBody CladireDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/gospodarii/{gospodarieId}/cladiri/{id}` | `deleteCladire(@PathVariable Long gospodarieId, @PathVariable Long id)` | Inherits class / HTTP rule |

## ContractUtilizareController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/ContractUtilizareController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/contracte` | `getAllContracts(@RequestParam(required = false) String uatCode, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/contracte/{id}` | `getContractById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/contracte` | `createContract(@RequestBody ContractUtilizareDTO contract)` | Inherits class / HTTP rule |
| PUT | `/api/contracte/{id}` | `updateContract(@PathVariable Long id, @RequestBody ContractUtilizareDTO contract)` | Inherits class / HTTP rule |
| DELETE | `/api/contracte/{id}` | `deleteContract(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/contracte/{id}/trimite-semnare` | `trimiteSpreSemnare(@PathVariable Long id, @RequestBody TrimiteSpreSemnareRequest request)` | Inherits class / HTTP rule |
| POST | `/api/contracte/{id}/status-semnare` | `verificaStatusSemnare(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/contracte/{id}/document-semnat` | `descarcaDocumentSemnat(@PathVariable Long id)` | Inherits class / HTTP rule |

## CrossTenantLookupController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CrossTenantLookupController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/transfers/destinations/gospodarii` | `getGospodariiForTransfer(@RequestParam String targetTenantId, @RequestParam(required = false) String uatCode)` | Inherits class / HTTP rule |
| GET | `/api/transfers/destinations/persons` | `getPersonsForTransfer(@RequestParam String targetTenantId)` | Inherits class / HTTP rule |

## CulturaParcelaController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/CulturaParcelaController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/parcele/{parcelaId}/culturi` | `getCulturi(@PathVariable Long parcelaId, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/parcele/{parcelaId}/culturi` | `addCultura(@PathVariable Long parcelaId, @RequestBody CulturaParcelaDto dto)` | Inherits class / HTTP rule |
| PUT | `/api/parcele/{parcelaId}/culturi/{culturaId}` | `updateCultura(@PathVariable Long parcelaId, @PathVariable Long culturaId, @RequestBody CulturaParcelaDto dto)` | Inherits class / HTTP rule |
| DELETE | `/api/parcele/{parcelaId}/culturi/{culturaId}` | `deleteCultura(@PathVariable Long parcelaId, @PathVariable Long culturaId)` | Inherits class / HTTP rule |

## DocumentController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/DocumentController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/documente` | `getAllDocuments(@RequestParam(required = false) String uatCode, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/documente/gospodarie/{gospodarieId}` | `getDocumentsByGospodarie(@PathVariable Long gospodarieId, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/documente` | `uploadDocument(@RequestPart("document") DocumentDTO dto, @RequestPart("file") MultipartFile file)` | Inherits class / HTTP rule |
| GET | `/api/documente/{id}/download` | `downloadDocument(@PathVariable Long id, @RequestParam Long gospodarieId)` | Inherits class / HTTP rule |
| DELETE | `/api/documente/{id}` | `deleteDocument(@PathVariable Long id, @RequestParam Long gospodarieId)` | Inherits class / HTTP rule |

## FactoriMediuController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/FactoriMediuController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/factori-mediu/parcela/{parcelaId}` | `getReadingsByParcela(@PathVariable Long parcelaId, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/factori-mediu` | `createReading(@Valid @RequestBody FactoriMediuDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/factori-mediu/{id}` | `deleteReading(@PathVariable Long id)` | Inherits class / HTTP rule |

## FertilizareController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/FertilizareController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/fertilizari` | `getFertilizari(@RequestParam(value = "parcelaId", required = false) Long parcelaId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/fertilizari/{id}` | `getById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/fertilizari` | `create(@RequestBody FertilizareDTO dto, @RequestParam(value = "confirmInterdictie", required = false, defaultValue = "false") boolean confirmInterdictie)` | Inherits class / HTTP rule |
| PUT | `/api/fertilizari/{id}` | `update(@PathVariable Long id, @RequestBody FertilizareDTO dto, @RequestParam(value = "confirmInterdictie", required = false, defaultValue = "false") boolean confirmInterdictie)` | Inherits class / HTTP rule |
| DELETE | `/api/fertilizari/{id}` | `delete(@PathVariable Long id)` | Inherits class / HTTP rule |

## FilaParceleiController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/FilaParceleiController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/parcele/{parcelaId}/fila` | `getFilaParcelei(@PathVariable Long parcelaId, @RequestParam(value = "anAgricol", required = false) Integer anAgricol)` | Inherits class / HTTP rule |

## GospodarieController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/GospodarieController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/gospodarii/{id}` | `getGospodarieById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/gospodarii` | `createGospodarie(@RequestBody Gospodarie gospodarie)` | Inherits class / HTTP rule |
| PUT | `/api/gospodarii/{id}` | `updateGospodarie(@PathVariable Long id, @RequestBody Gospodarie gospodarie)` | Inherits class / HTTP rule |
| DELETE | `/api/gospodarii/{id}` | `deleteGospodarie(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/gospodarii` | `getAllGospodarii(@RequestParam(required = false) String uatCode, @RequestParam(required = false) String tipGospodarie, @RequestParam(required = false) Boolean activa, @RequestParam(required = false) String search, Pageable pageable)` | Inherits class / HTTP rule |
| PUT | `/api/gospodarii/{gospodarieId}/cap-gospodarie/{persoanaId}` | `seteazaCapGospodariePath(@PathVariable Long gospodarieId, @PathVariable Long persoanaId)` | Inherits class / HTTP rule |
| PUT | `/api/gospodarii/{gospodarieId}/cap-gospodarie` | `seteazaCapGospodarieQuery(@PathVariable Long gospodarieId, @RequestParam(required = false) Long persoanaId)` | Inherits class / HTTP rule |
| GET | `/api/gospodarii/{gospodarieId}/istoric-membri` | `getIstoricMembri(@PathVariable Long gospodarieId)` | Inherits class / HTTP rule |
| POST | `/api/gospodarii/{gospodarieId}/istoric-membri` | `adaugaEvenimentIstoric(@PathVariable Long gospodarieId, @RequestBody IstoricMembruDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/gospodarii/{gospodarieId}/istoric-membri/{evenimentId}` | `updateEvenimentIstoric(@PathVariable Long gospodarieId, @PathVariable Long evenimentId, @RequestBody IstoricMembruDTO dto)` | Inherits class / HTTP rule |

## LookupController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/LookupController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/lookup/tip-sol` | `getTipuriSol()` | Inherits class / HTTP rule |
| GET | `/api/lookup/categorie-folosinta` | `getCategoriiFolosinta()` | Inherits class / HTTP rule |
| GET | `/api/lookup/tip-sursa-apa` | `getTipuriSursaApa()` | Inherits class / HTTP rule |
| GET | `/api/lookup/tip-document` | `getTipuriDocument()` | Inherits class / HTTP rule |
| GET | `/api/lookup/specii-pomi` | `getSpeciiPomi()` | Inherits class / HTTP rule |

## MachineryController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/MachineryController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/machinery` | `getAllMachinery(Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/machinery/gospodarie/{gospodarieId}` | `getMachineryByGospodarie(@PathVariable Long gospodarieId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/machinery/{id}` | `getMachineryById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/machinery` | `createMachinery(@RequestBody MachineryDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/machinery/{id}` | `updateMachinery(@PathVariable Long id, @RequestBody MachineryDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/machinery/{id}` | `deleteMachinery(@PathVariable Long id)` | Inherits class / HTTP rule |

## NominatimProxyController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/NominatimProxyController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/proxy/nominatim` | `searchNominatim(@RequestParam String q)` | Inherits class / HTTP rule |

## NotificareSuccesiuneController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/NotificareSuccesiuneController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| POST | `/api/succesiuni` | `createNotificare(@RequestBody NotificareSuccesiuneDTO dto)` | Inherits class / HTTP rule |
| GET | `/api/succesiuni` | `getAllNotificari()` | Inherits class / HTTP rule |
| GET | `/api/succesiuni/defunct/{cnp}` | `getNotificariByDefunctCnp(@PathVariable String cnp)` | Inherits class / HTTP rule |
| PATCH | `/api/succesiuni/{id}/stadiu` | `updateStadiu(@PathVariable Long id, @RequestParam String stadiu)` | Inherits class / HTTP rule |

## PadureController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/PadureController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/parcele/{parcelaId}/paduri` | `getAll(@PathVariable Long parcelaId, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/parcele/{parcelaId}/paduri` | `create(@PathVariable Long parcelaId, @Valid @RequestBody PadureDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/parcele/{parcelaId}/paduri/{id}` | `update(@PathVariable Long parcelaId, @PathVariable Long id, @Valid @RequestBody PadureDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/parcele/{parcelaId}/paduri/{id}` | `delete(@PathVariable Long parcelaId, @PathVariable Long id)` | Inherits class / HTTP rule |

## ParcelaController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/ParcelaController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/parcele` | `getAllParcele(Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/parcele/teren/{terenId}` | `getParcele(@PathVariable Long terenId, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/parcele/teren/{terenId}` | `addParcela(@PathVariable Long terenId, @Valid @RequestBody Parcela parcela)` | Inherits class / HTTP rule |
| PUT | `/api/parcele/{id}` | `updateParcela(@PathVariable Long id, @Valid @RequestBody Parcela parcela)` | Inherits class / HTTP rule |
| DELETE | `/api/parcele/{id}` | `deleteParcela(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/parcele/{id}/istoric` | `getParcelaHistory(@PathVariable Long id)` | Inherits class / HTTP rule |

## PasuneFaneataController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/PasuneFaneataController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/parcele/{parcelaId}/pasuni-fanete` | `getAll(@PathVariable Long parcelaId, @RequestParam(required = false) TipFolosintaPasune tip, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/parcele/{parcelaId}/pasuni-fanete` | `add(@PathVariable Long parcelaId, @Valid @RequestBody PasuneFaneataDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/parcele/{parcelaId}/pasuni-fanete/{id}` | `update(@PathVariable Long parcelaId, @PathVariable Long id, @Valid @RequestBody PasuneFaneataDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/parcele/{parcelaId}/pasuni-fanete/{id}` | `delete(@PathVariable Long parcelaId, @PathVariable Long id)` | Inherits class / HTTP rule |

## PersoanaController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/PersoanaController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| POST | `/api/persons` | `createPerson(@Valid @RequestBody Persoana persoana)` | Inherits class / HTTP rule |
| POST | `/api/persoane` | `createPerson(@Valid @RequestBody Persoana persoana)` | Inherits class / HTTP rule |
| GET | `/api/persons` | `getAllPersons(@RequestParam(required = false) String search, @RequestParam(required = false) String type, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/persoane` | `getAllPersons(@RequestParam(required = false) String search, @RequestParam(required = false) String type, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/persons/gospodarie/{gospodarieId}` | `getPersonsByGospodarieId(@PathVariable Long gospodarieId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/persoane/gospodarie/{gospodarieId}` | `getPersonsByGospodarieId(@PathVariable Long gospodarieId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/persons/{id}` | `getPersonById(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/persoane/{id}` | `getPersonById(@PathVariable Long id)` | Inherits class / HTTP rule |
| PUT | `/api/persons/{id}` | `updatePerson(@PathVariable Long id, @Valid @RequestBody Persoana persoana)` | Inherits class / HTTP rule |
| PUT | `/api/persoane/{id}` | `updatePerson(@PathVariable Long id, @Valid @RequestBody Persoana persoana)` | Inherits class / HTTP rule |
| DELETE | `/api/persons/{id}` | `deletePerson(@PathVariable Long id)` | Inherits class / HTTP rule |
| DELETE | `/api/persoane/{id}` | `deletePerson(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/persons/{persoanaId}/gospodarii/{gospodarieId}` | `addPersonToGospodarie(@PathVariable Long persoanaId, @PathVariable Long gospodarieId)` | Inherits class / HTTP rule |
| POST | `/api/persoane/{persoanaId}/gospodarii/{gospodarieId}` | `addPersonToGospodarie(@PathVariable Long persoanaId, @PathVariable Long gospodarieId)` | Inherits class / HTTP rule |

## PomController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/PomController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/parcele/{parcelaId}/pomi` | `getPomi(@PathVariable Long parcelaId, @RequestParam(required = false) TipInregistrarePom tip, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/parcele/{parcelaId}/pomi` | `addPom(@PathVariable Long parcelaId, @Valid @RequestBody PomDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/parcele/{parcelaId}/pomi/{pomId}` | `updatePom(@PathVariable Long parcelaId, @PathVariable Long pomId, @Valid @RequestBody PomDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/parcele/{parcelaId}/pomi/{pomId}` | `deletePom(@PathVariable Long parcelaId, @PathVariable Long pomId)` | Inherits class / HTTP rule |

## PublicCitizenController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/PublicCitizenController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/public/cetateni/verify` | `verifyCitizen(@RequestParam String cnp, @RequestParam String initials, @RequestParam Long uatId)` | Inherits class / HTTP rule |

## PublicUatEndpointController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/PublicUatEndpointController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/public/uats/judete` | `getJudete()` | Inherits class / HTTP rule |
| GET | `/api/public/uats/localitati` | `getLocalitatiByJudet(@RequestParam String judet)` | Inherits class / HTTP rule |
| GET | `/api/public/uats/all` | `getAllLocalitati()` | Inherits class / HTTP rule |

## RaportStatisticController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/RaportStatisticController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/v1/statistici/complet` | `getComplet(@RequestParam(required = false, defaultValue = "2026") Integer an, @RequestParam(required = false) String uatCode)` | Inherits class / HTTP rule |
| GET | `/api/v1/statistici/export/vegetal` | `exportVegetal(@RequestParam(required = false, defaultValue = "2026") Integer an, @RequestParam(required = false) String uatCode)` | Inherits class / HTTP rule |
| GET | `/api/v1/statistici/export/zootehnic` | `exportZootehnic(@RequestParam(required = false) String uatCode)` | Inherits class / HTTP rule |
| GET | `/api/v1/statistici/export/utilaje` | `exportUtilaje(@RequestParam(required = false) String uatCode)` | Inherits class / HTTP rule |

## RecoltareController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/RecoltareController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/recoltari/parcela/{parcelaId}` | `getRecoltariByParcela(@PathVariable Long parcelaId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/recoltari/{id}` | `getRecoltareById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/recoltari` | `createRecoltare(@Valid @RequestBody RecoltareDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/recoltari/{id}` | `updateRecoltare(@PathVariable Long id, @Valid @RequestBody RecoltareDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/recoltari/{id}` | `deleteRecoltare(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/recoltari/centralizator` | `getCentralizator(@RequestParam(required = false) Integer anAgricol)` | Inherits class / HTTP rule |

## SursaApaController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/SursaApaController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/parcele/{parcelaId}/surse-apa` | `getSurse(@PathVariable Long parcelaId, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/parcele/{parcelaId}/surse-apa` | `addSursa(@PathVariable Long parcelaId, @RequestBody SursaApaDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/parcele/{parcelaId}/surse-apa/{sursaId}` | `updateSursa(@PathVariable Long parcelaId, @PathVariable Long sursaId, @RequestBody SursaApaDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/parcele/{parcelaId}/surse-apa/{sursaId}` | `deleteSursa(@PathVariable Long parcelaId, @PathVariable Long sursaId)` | Inherits class / HTTP rule |

## TenantController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/TenantController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN')` · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| POST | `/api/tenants` | `createTenant(@RequestBody TenantCreateRequest request)` | Inherits class / HTTP rule |
| GET | `/api/tenants` | `getAllTenants()` | Inherits class / HTTP rule |
| PUT | `/api/tenants/{tenantId}` | `updateTenant(@PathVariable String tenantId, @RequestBody TenantCreateRequest request)` | Inherits class / HTTP rule |
| POST | `/api/tenants/migrate-all` | `migrateAllTenants()` | Inherits class / HTTP rule |

## TerenController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/TerenController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/terenuri` | `getAllTerenuri(Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/terenuri/gospodarie/{gospodarieId}` | `getTerenByGospodarieId(@PathVariable Long gospodarieId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/terenuri/{id}` | `getTerenById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/terenuri` | `createTeren(@Valid @RequestBody TerenCreateDTO dto)` | Inherits class / HTTP rule |
| POST | `/api/terenuri/with-parcela` | `createTerenWithParcela(@Valid @RequestBody TerenWithParcelaDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/terenuri/{id}` | `updateTeren(@PathVariable Long id, @Valid @RequestBody Teren teren)` | Inherits class / HTTP rule |
| DELETE | `/api/terenuri/{id}` | `deleteTeren(@PathVariable Long id)` | Inherits class / HTTP rule |

## TratamentFitosanitarController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/TratamentFitosanitarController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/tratamente` | `getTratamente(@RequestParam(value = "parcelaId", required = false) Long parcelaId, Pageable pageable)` | Inherits class / HTTP rule |
| GET | `/api/tratamente/{id}` | `getById(@PathVariable Long id)` | Inherits class / HTTP rule |
| POST | `/api/tratamente` | `create(@RequestBody TratamentFitosanitarDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/tratamente/{id}` | `update(@PathVariable Long id, @RequestBody TratamentFitosanitarDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/tratamente/{id}` | `delete(@PathVariable Long id)` | Inherits class / HTTP rule |
| GET | `/api/tratamente/export/pdf` | `downloadRegistruPdf()` | Inherits class / HTTP rule |

## UatController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/UatController.java) · Class authorization: no class expression · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/uats` | `getAllPublicUats()` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` |
| POST | `/api/uats` | `createPublicUat(@RequestBody PublicUat uat)` | `hasRole('ROLE_SUPER_ADMIN')` |
| PUT | `/api/uats/{codSiruta}` | `updatePublicUat(@PathVariable String codSiruta, @RequestBody PublicUat request)` | `hasRole('ROLE_SUPER_ADMIN')` |
| DELETE | `/api/uats/{codSiruta}` | `deletePublicUat(@PathVariable String codSiruta)` | `hasRole('ROLE_SUPER_ADMIN')` |
| GET | `/api/uats/judete` | `getJudete()` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` |
| GET | `/api/uats/localitati` | `getLocalitatiByJudet(@RequestParam String judet)` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` |
| GET | `/api/uats/tenant` | `getTenantUats()` | `hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` |
| POST | `/api/uats/tenant/{codSiruta}` | `assignUatToTenant(@PathVariable String codSiruta)` | `hasRole('ROLE_ADMIN')` |
| DELETE | `/api/uats/tenant/{codSiruta}` | `removeUatFromTenant(@PathVariable String codSiruta)` | `hasRole('ROLE_ADMIN')` |

## UserController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/UserController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **no**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| POST | `/api/users` | `createUser(@RequestBody User user)` | `hasRole('ROLE_SUPER_ADMIN') or (hasRole('ROLE_ADMIN') and #user.role != 'ROLE_SUPER_ADMIN')` |
| GET | `/api/users` | `getAllUsers(Pageable pageable)` | `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN')` |
| GET | `/api/users/{id}` | `getUser(@PathVariable long id)` | `@userSecurity.canAccessUser(principal, #id)` |
| PUT | `/api/users/{id}` | `updateUser(@PathVariable long id, @RequestBody User userDetails)` | `@userSecurity.canAccessUser(principal, #id) and (hasRole('ROLE_SUPER_ADMIN') or (hasRole('ROLE_ADMIN') and #userDetails.role != 'ROLE_SUPER_ADMIN') or (hasRole('ROLE_USER') and #id == principal.id and #userDetails.role == null))` |
| DELETE | `/api/users/{id}` | `deleteUser(@PathVariable long id)` | `@userSecurity.canAccessUser(principal, #id) and (hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN'))` |

## VitaDeVieController

[Controller source](../../src/backend/src/main/java/com/multitenant/controller/VitaDeVieController.java) · Class authorization: `hasRole('ROLE_SUPER_ADMIN') or hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')` · Tenant-required annotation: **yes**.

| Method | Complete route | Input signature | Method authorization override |
| --- | --- | --- | --- |
| GET | `/api/parcele/{parcelaId}/vita-de-vie` | `getVitaDeVie(@PathVariable Long parcelaId, @RequestParam(required = false) TipInregistrareVita tip, Pageable pageable)` | Inherits class / HTTP rule |
| POST | `/api/parcele/{parcelaId}/vita-de-vie` | `addVita(@PathVariable Long parcelaId, @Valid @RequestBody VitaDeVieDTO dto)` | Inherits class / HTTP rule |
| PUT | `/api/parcele/{parcelaId}/vita-de-vie/{vitaId}` | `updateVita(@PathVariable Long parcelaId, @PathVariable Long vitaId, @Valid @RequestBody VitaDeVieDTO dto)` | Inherits class / HTTP rule |
| DELETE | `/api/parcele/{parcelaId}/vita-de-vie/{vitaId}` | `deleteVita(@PathVariable Long parcelaId, @PathVariable Long vitaId)` | Inherits class / HTTP rule |

## Controller-local checks worth reading

- Citizen profile/history/attestation methods require a citizen principal despite their public prefix.
- Public application create/tracking/by-CNP and citizen verification are exposed with their supplied lookup inputs.
- PDF generation checks accepted status and owner/admin in method code; role recognition differs from the application-decision controller, and numeric IDs are scanned across schemas.
- Animal destination lookup deliberately changes context to the supplied target tenant.
- User target operations call `userSecurity`; user creation forces the current tenant for ordinary admins.
- SignNow actions may send external invitations; listing them is not authorization to invoke them with real recipients.

See [implementation status](../Implementation-Status.md) for known role/path mismatches and [source inventory](Source-Inventory.md) for frontend consumers.
