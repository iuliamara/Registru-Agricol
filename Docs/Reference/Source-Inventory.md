# Audited source inventory

[Documentation index](../README.md) · [Audit method](../Audit.md) · [API](API.md) · [Domain](Domain.md)

This index covers the 608 source/configuration files read during the recursive audit. Dependencies, generated build/cache output, Git internals, runtime logs/uploads, and private `.env` values were excluded. Documentation/screenshots are indexed separately. Links resolve to the current authoritative repository, not recovery source. [Source hashes](Source-Hashes.json) record the audited file contents.

## Independent application routes

Exact current declarations retain the duplicate institutional `contracte` entry, absent institutional guards, and citizen guard placement. Embedded household/parcel modules add functionality without separate routes.

### Citizens Portal

[Route source](../../src/portal-cetateni/src/app/app.routes.ts)

```typescript
export const routes: Routes = [
  { path: '', component: Home },
  { path: 'login', component: Login },
  { path: 'register', component: Register },
  { path: 'cereri', component: Cereri, canActivate: [AuthGuard] },
  { path: 'cereri-mele', component: CereriMele, canActivate: [AuthGuard] },
  { path: 'stadiu', component: Stadiu },
  { path: 'contul-meu', component: ContulMeu },
  { path: '**', redirectTo: '' }
];
```

### Public Institutions Portal

[Route source](../../src/frontend/src/app/app.routes.ts)

```typescript
export const routes: Routes = [
  { path: 'login',          component: LoginComponent },
  { path: 'dashboard',      component: DashboardComponent },
  { path: 'super-admin',    component: SuperAdminDashboardComponent },
  { path: 'tenant-admin',   component: TenantAdminDashboardComponent },
  { path: 'user-management',component: UserManagementComponent },
  { path: 'tenants',        component: CreateTenantComponent },
  { path: 'persoane',        component: PersonListComponent },
  { path: 'persoane/new',    component: PersonFormComponent },
  { path: 'persoane/edit/:id', component: PersonFormComponent },
  { path: 'contracte',      component: ContractManagementComponent },
  { path: 'uats',           component: UatManagementComponent },
  { path: 'uats/:id',       component: UatDetailsComponent },
  { path: 'gospodarii',     component: GospodarieListComponent },
  { path: 'gospodarii/new', component: GospodarieFormComponent },
  { path: 'gospodarii/edit/:id', component: GospodarieFormComponent },
  { path: 'gospodarii/:id', component: GospodarieDetailsComponent },
  { path: 'terenuri/new',   component: TerenFormComponent },
  { path: 'terenuri/:id/parcele', component: TerenParceleComponent },
  { path: 'animale',         component: AnimalListComponent },
  { path: 'animale/individual/new', component: AnimalIndividualFormComponent },
  { path: 'animale/individual/edit/:id', component: AnimalIndividualFormComponent },
  { path: 'animale/grup/new', component: EfectivGrupFormComponent },
  // Snapshot route: adaugă un rând nou la efectivul existent (model append-only ANSVSA)
  { path: 'animale/grup/:id/snapshot', component: EfectivGrupFormComponent },
  { path: 'animale/individual/:id/istoric', component: AnimalTimelineComponent },
  { path: 'harta',          component: ParcelaMapComponent },
  { path: 'google-harta',   component: OsmMapComponent },
  { path: 'contracte',      component: ContractManagementComponent },
  { path: 'cereri-admin',   component: CereriAdminComponent },
  { path: 'evidenta-chimica', component: EvidentaChimicaComponent },
  { path: 'statistici',     component: StatisticiComponent },
  { path: 'succesiuni',     component: NotificareSuccesiuneComponent },
  { path: '',               redirectTo: '/login', pathMatch: 'full' }
];
```

## Citizens Portal source and configuration

| Source file | Declared type / responsibility indicator |
| --- | --- |
| [src/portal-cetateni/.gitignore](../../src/portal-cetateni/.gitignore) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/Dockerfile](../../src/portal-cetateni/Dockerfile) | Container build/runtime |
| [src/portal-cetateni/angular.json](../../src/portal-cetateni/angular.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/portal-cetateni/nginx.conf](../../src/portal-cetateni/nginx.conf) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/package-lock.json](../../src/portal-cetateni/package-lock.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/portal-cetateni/package.json](../../src/portal-cetateni/package.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/portal-cetateni/proxy.conf.json](../../src/portal-cetateni/proxy.conf.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/portal-cetateni/public/uats.json](../../src/portal-cetateni/public/uats.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/portal-cetateni/src/app/app.component.html](../../src/portal-cetateni/src/app/app.component.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/app.config.ts](../../src/portal-cetateni/src/app/app.config.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/app.css](../../src/portal-cetateni/src/app/app.css) | Application/component styles |
| [src/portal-cetateni/src/app/app.html](../../src/portal-cetateni/src/app/app.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/app.routes.ts](../../src/portal-cetateni/src/app/app.routes.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/app.spec.ts](../../src/portal-cetateni/src/app/app.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/app.ts](../../src/portal-cetateni/src/app/app.ts) | `App` |
| [src/portal-cetateni/src/app/data/uats.data.ts](../../src/portal-cetateni/src/app/data/uats.data.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/guards/auth.guard.ts](../../src/portal-cetateni/src/app/guards/auth.guard.ts) | `AuthGuard` |
| [src/portal-cetateni/src/app/pages/cereri-mele/cereri-mele.css](../../src/portal-cetateni/src/app/pages/cereri-mele/cereri-mele.css) | Application/component styles |
| [src/portal-cetateni/src/app/pages/cereri-mele/cereri-mele.html](../../src/portal-cetateni/src/app/pages/cereri-mele/cereri-mele.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/pages/cereri-mele/cereri-mele.spec.ts](../../src/portal-cetateni/src/app/pages/cereri-mele/cereri-mele.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/pages/cereri-mele/cereri-mele.ts](../../src/portal-cetateni/src/app/pages/cereri-mele/cereri-mele.ts) | `Cerere`, `CereriMele` |
| [src/portal-cetateni/src/app/pages/cereri/cereri.css](../../src/portal-cetateni/src/app/pages/cereri/cereri.css) | Application/component styles |
| [src/portal-cetateni/src/app/pages/cereri/cereri.html](../../src/portal-cetateni/src/app/pages/cereri/cereri.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/pages/cereri/cereri.spec.ts](../../src/portal-cetateni/src/app/pages/cereri/cereri.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/pages/cereri/cereri.ts](../../src/portal-cetateni/src/app/pages/cereri/cereri.ts) | `TipCerere`, `Cereri` |
| [src/portal-cetateni/src/app/pages/contul-meu/contul-meu.css](../../src/portal-cetateni/src/app/pages/contul-meu/contul-meu.css) | Application/component styles |
| [src/portal-cetateni/src/app/pages/contul-meu/contul-meu.html](../../src/portal-cetateni/src/app/pages/contul-meu/contul-meu.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/pages/contul-meu/contul-meu.ts](../../src/portal-cetateni/src/app/pages/contul-meu/contul-meu.ts) | `ContulMeu` |
| [src/portal-cetateni/src/app/pages/home/home.css](../../src/portal-cetateni/src/app/pages/home/home.css) | Application/component styles |
| [src/portal-cetateni/src/app/pages/home/home.html](../../src/portal-cetateni/src/app/pages/home/home.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/pages/home/home.spec.ts](../../src/portal-cetateni/src/app/pages/home/home.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/pages/home/home.ts](../../src/portal-cetateni/src/app/pages/home/home.ts) | `Home` |
| [src/portal-cetateni/src/app/pages/login/login.css](../../src/portal-cetateni/src/app/pages/login/login.css) | Application/component styles |
| [src/portal-cetateni/src/app/pages/login/login.html](../../src/portal-cetateni/src/app/pages/login/login.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/pages/login/login.ts](../../src/portal-cetateni/src/app/pages/login/login.ts) | `Login` |
| [src/portal-cetateni/src/app/pages/register/register.css](../../src/portal-cetateni/src/app/pages/register/register.css) | Application/component styles |
| [src/portal-cetateni/src/app/pages/register/register.html](../../src/portal-cetateni/src/app/pages/register/register.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/pages/register/register.ts](../../src/portal-cetateni/src/app/pages/register/register.ts) | `Register` |
| [src/portal-cetateni/src/app/pages/stadiu/stadiu.css](../../src/portal-cetateni/src/app/pages/stadiu/stadiu.css) | Application/component styles |
| [src/portal-cetateni/src/app/pages/stadiu/stadiu.html](../../src/portal-cetateni/src/app/pages/stadiu/stadiu.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/app/pages/stadiu/stadiu.spec.ts](../../src/portal-cetateni/src/app/pages/stadiu/stadiu.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/pages/stadiu/stadiu.ts](../../src/portal-cetateni/src/app/pages/stadiu/stadiu.ts) | `Stadiu` |
| [src/portal-cetateni/src/app/services/auth.service.ts](../../src/portal-cetateni/src/app/services/auth.service.ts) | `User`, `AuthService` |
| [src/portal-cetateni/src/app/services/jwt.interceptor.ts](../../src/portal-cetateni/src/app/services/jwt.interceptor.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/app/services/websocket.service.ts](../../src/portal-cetateni/src/app/services/websocket.service.ts) | `WebsocketService` |
| [src/portal-cetateni/src/index.html](../../src/portal-cetateni/src/index.html) | Angular / email / PDF template |
| [src/portal-cetateni/src/main.ts](../../src/portal-cetateni/src/main.ts) | Configuration / bootstrap / utility; see source |
| [src/portal-cetateni/src/styles.css](../../src/portal-cetateni/src/styles.css) | Application/component styles |
| [src/portal-cetateni/tsconfig.app.json](../../src/portal-cetateni/tsconfig.app.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/portal-cetateni/tsconfig.json](../../src/portal-cetateni/tsconfig.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/portal-cetateni/tsconfig.spec.json](../../src/portal-cetateni/tsconfig.spec.json) | Workspace, dependency lock, proxy, data, or compiler configuration |

## Public Institutions Portal source and configuration

| Source file | Declared type / responsibility indicator |
| --- | --- |
| [src/frontend/.gitignore](../../src/frontend/.gitignore) | Configuration / bootstrap / utility; see source |
| [src/frontend/Dockerfile](../../src/frontend/Dockerfile) | Container build/runtime |
| [src/frontend/angular.json](../../src/frontend/angular.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/frontend/nginx.conf](../../src/frontend/nginx.conf) | Configuration / bootstrap / utility; see source |
| [src/frontend/package-lock.json](../../src/frontend/package-lock.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/frontend/package.json](../../src/frontend/package.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/frontend/proxy.conf.json](../../src/frontend/proxy.conf.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/frontend/src/app/app.component.css](../../src/frontend/src/app/app.component.css) | Application/component styles |
| [src/frontend/src/app/app.component.html](../../src/frontend/src/app/app.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/app.component.ts](../../src/frontend/src/app/app.component.ts) | `AppComponent` |
| [src/frontend/src/app/app.config.ts](../../src/frontend/src/app/app.config.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/app.routes.ts](../../src/frontend/src/app/app.routes.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/components/active-uat-banner/active-uat-banner.component.css](../../src/frontend/src/app/components/active-uat-banner/active-uat-banner.component.css) | Application/component styles |
| [src/frontend/src/app/components/active-uat-banner/active-uat-banner.component.html](../../src/frontend/src/app/components/active-uat-banner/active-uat-banner.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/active-uat-banner/active-uat-banner.component.spec.ts](../../src/frontend/src/app/components/active-uat-banner/active-uat-banner.component.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/components/active-uat-banner/active-uat-banner.component.ts](../../src/frontend/src/app/components/active-uat-banner/active-uat-banner.component.ts) | `ActiveUatBannerComponent` |
| [src/frontend/src/app/components/breadcrumbs/breadcrumbs.component.css](../../src/frontend/src/app/components/breadcrumbs/breadcrumbs.component.css) | Application/component styles |
| [src/frontend/src/app/components/breadcrumbs/breadcrumbs.component.html](../../src/frontend/src/app/components/breadcrumbs/breadcrumbs.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/breadcrumbs/breadcrumbs.component.spec.ts](../../src/frontend/src/app/components/breadcrumbs/breadcrumbs.component.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/components/breadcrumbs/breadcrumbs.component.ts](../../src/frontend/src/app/components/breadcrumbs/breadcrumbs.component.ts) | `BreadcrumbItem`, `BreadcrumbsComponent` |
| [src/frontend/src/app/components/generic-form/generic-form.component.css](../../src/frontend/src/app/components/generic-form/generic-form.component.css) | Application/component styles |
| [src/frontend/src/app/components/generic-form/generic-form.component.html](../../src/frontend/src/app/components/generic-form/generic-form.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/generic-form/generic-form.component.ts](../../src/frontend/src/app/components/generic-form/generic-form.component.ts) | `GenericFormComponent` |
| [src/frontend/src/app/components/generic-form/generic-form.models.ts](../../src/frontend/src/app/components/generic-form/generic-form.models.ts) | `FormFieldOption`, `FormField`, `FormSection`, `FormConfig` |
| [src/frontend/src/app/components/generic-table/generic-table.component.css](../../src/frontend/src/app/components/generic-table/generic-table.component.css) | Application/component styles |
| [src/frontend/src/app/components/generic-table/generic-table.component.html](../../src/frontend/src/app/components/generic-table/generic-table.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/generic-table/generic-table.component.ts](../../src/frontend/src/app/components/generic-table/generic-table.component.ts) | `TableColumn`, `TableFilter`, `TableAction`, `GenericTableComponent` |
| [src/frontend/src/app/components/layout/layout.component.html](../../src/frontend/src/app/components/layout/layout.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/layout/layout.component.ts](../../src/frontend/src/app/components/layout/layout.component.ts) | `LayoutComponent` |
| [src/frontend/src/app/components/osm-map/osm-map.component.css](../../src/frontend/src/app/components/osm-map/osm-map.component.css) | Application/component styles |
| [src/frontend/src/app/components/osm-map/osm-map.component.html](../../src/frontend/src/app/components/osm-map/osm-map.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/osm-map/osm-map.component.ts](../../src/frontend/src/app/components/osm-map/osm-map.component.ts) | `OsmMapComponent` |
| [src/frontend/src/app/components/page-header/page-header.component.html](../../src/frontend/src/app/components/page-header/page-header.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/page-header/page-header.component.ts](../../src/frontend/src/app/components/page-header/page-header.component.ts) | `PageHeaderComponent` |
| [src/frontend/src/app/components/parcela-map/parcela-map.component.css](../../src/frontend/src/app/components/parcela-map/parcela-map.component.css) | Application/component styles |
| [src/frontend/src/app/components/parcela-map/parcela-map.component.html](../../src/frontend/src/app/components/parcela-map/parcela-map.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/parcela-map/parcela-map.component.spec.ts](../../src/frontend/src/app/components/parcela-map/parcela-map.component.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/components/parcela-map/parcela-map.component.ts](../../src/frontend/src/app/components/parcela-map/parcela-map.component.ts) | `ParcelaMapComponent` |
| [src/frontend/src/app/components/person-search-modal/person-search-modal.component.css](../../src/frontend/src/app/components/person-search-modal/person-search-modal.component.css) | Application/component styles |
| [src/frontend/src/app/components/person-search-modal/person-search-modal.component.html](../../src/frontend/src/app/components/person-search-modal/person-search-modal.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/person-search-modal/person-search-modal.component.ts](../../src/frontend/src/app/components/person-search-modal/person-search-modal.component.ts) | `PersonSearchModalComponent` |
| [src/frontend/src/app/components/sidebar/sidebar.component.html](../../src/frontend/src/app/components/sidebar/sidebar.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/sidebar/sidebar.component.ts](../../src/frontend/src/app/components/sidebar/sidebar.component.ts) | `SidebarComponent` |
| [src/frontend/src/app/components/street-autocomplete/street-autocomplete.component.css](../../src/frontend/src/app/components/street-autocomplete/street-autocomplete.component.css) | Application/component styles |
| [src/frontend/src/app/components/street-autocomplete/street-autocomplete.component.html](../../src/frontend/src/app/components/street-autocomplete/street-autocomplete.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/components/street-autocomplete/street-autocomplete.component.ts](../../src/frontend/src/app/components/street-autocomplete/street-autocomplete.component.ts) | `StreetAutocompleteComponent` |
| [src/frontend/src/app/dashboard/dashboard.component.css](../../src/frontend/src/app/dashboard/dashboard.component.css) | Application/component styles |
| [src/frontend/src/app/dashboard/dashboard.component.html](../../src/frontend/src/app/dashboard/dashboard.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/dashboard/dashboard.component.ts](../../src/frontend/src/app/dashboard/dashboard.component.ts) | `DashboardComponent` |
| [src/frontend/src/app/login/login.component.css](../../src/frontend/src/app/login/login.component.css) | Application/component styles |
| [src/frontend/src/app/login/login.component.html](../../src/frontend/src/app/login/login.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/login/login.component.ts](../../src/frontend/src/app/login/login.component.ts) | `LoginComponent` |
| [src/frontend/src/app/models/animal.model.ts](../../src/frontend/src/app/models/animal.model.ts) | `SpecieAnimal`, `SexAnimal`, `TipEvenimentAnimal`, `AnimalIndividual`, `EfectivGrup`, `ProprietarAnimals`, `GospodarieAnimals`, `EvenimentAnimal`, `TransferRequest`, `TransferResponse` |
| [src/frontend/src/app/models/carte-funciara.model.ts](../../src/frontend/src/app/models/carte-funciara.model.ts) | `CarteFunciara` |
| [src/frontend/src/app/models/catalog-ingrasaminte.model.ts](../../src/frontend/src/app/models/catalog-ingrasaminte.model.ts) | `CatalogIngrasaminte` |
| [src/frontend/src/app/models/catalog-ppp.model.ts](../../src/frontend/src/app/models/catalog-ppp.model.ts) | `CatalogPpp` |
| [src/frontend/src/app/models/categorie-folosinta.model.ts](../../src/frontend/src/app/models/categorie-folosinta.model.ts) | `CategorieFolosinta` |
| [src/frontend/src/app/models/ciclu-productie.model.ts](../../src/frontend/src/app/models/ciclu-productie.model.ts) | `CicluProductie` |
| [src/frontend/src/app/models/cladire.model.ts](../../src/frontend/src/app/models/cladire.model.ts) | `Cladire` |
| [src/frontend/src/app/models/cultura-parcela.model.ts](../../src/frontend/src/app/models/cultura-parcela.model.ts) | `CulturaParcela` |
| [src/frontend/src/app/models/document.model.ts](../../src/frontend/src/app/models/document.model.ts) | `TipDocument` |
| [src/frontend/src/app/models/fertilizare.model.ts](../../src/frontend/src/app/models/fertilizare.model.ts) | `Fertilizare` |
| [src/frontend/src/app/models/fila-parcelei.model.ts](../../src/frontend/src/app/models/fila-parcelei.model.ts) | `FilaParcelei` |
| [src/frontend/src/app/models/gospodarie.model.ts](../../src/frontend/src/app/models/gospodarie.model.ts) | `Adresa`, `Uat`, `Gospodarie` |
| [src/frontend/src/app/models/machinery.model.ts](../../src/frontend/src/app/models/machinery.model.ts) | `Machinery` |
| [src/frontend/src/app/models/padure.model.ts](../../src/frontend/src/app/models/padure.model.ts) | `Padure` |
| [src/frontend/src/app/models/paginated-response.model.ts](../../src/frontend/src/app/models/paginated-response.model.ts) | `PaginatedResponse` |
| [src/frontend/src/app/models/parcela.model.ts](../../src/frontend/src/app/models/parcela.model.ts) | `Parcela` |
| [src/frontend/src/app/models/pasune-faneata.model.ts](../../src/frontend/src/app/models/pasune-faneata.model.ts) | `TipFolosintaPasune`, `PasuneFaneata` |
| [src/frontend/src/app/models/persoana.model.ts](../../src/frontend/src/app/models/persoana.model.ts) | `Adresa`, `Persoana`, `PersoanaFizica`, `PersoanaJuridica` |
| [src/frontend/src/app/models/pom.model.ts](../../src/frontend/src/app/models/pom.model.ts) | `TipInregistrarePom`, `Pom` |
| [src/frontend/src/app/models/recoltare.model.ts](../../src/frontend/src/app/models/recoltare.model.ts) | `Recoltare` |
| [src/frontend/src/app/models/specie-ref.model.ts](../../src/frontend/src/app/models/specie-ref.model.ts) | `SpecieRef` |
| [src/frontend/src/app/models/sursa-apa.model.ts](../../src/frontend/src/app/models/sursa-apa.model.ts) | `SursaApa` |
| [src/frontend/src/app/models/teren.model.ts](../../src/frontend/src/app/models/teren.model.ts) | `Teren` |
| [src/frontend/src/app/models/tratament-fitosanitar.model.ts](../../src/frontend/src/app/models/tratament-fitosanitar.model.ts) | `TratamentFitosanitar` |
| [src/frontend/src/app/models/vita-de-vie.model.ts](../../src/frontend/src/app/models/vita-de-vie.model.ts) | `TipInregistrareVita`, `VitaDeVie` |
| [src/frontend/src/app/pages/animal-individual-form/animal-individual-form.component.css](../../src/frontend/src/app/pages/animal-individual-form/animal-individual-form.component.css) | Application/component styles |
| [src/frontend/src/app/pages/animal-individual-form/animal-individual-form.component.html](../../src/frontend/src/app/pages/animal-individual-form/animal-individual-form.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/animal-individual-form/animal-individual-form.component.ts](../../src/frontend/src/app/pages/animal-individual-form/animal-individual-form.component.ts) | `AnimalIndividualFormComponent` |
| [src/frontend/src/app/pages/animal-list/animal-list.component.html](../../src/frontend/src/app/pages/animal-list/animal-list.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/animal-list/animal-list.component.ts](../../src/frontend/src/app/pages/animal-list/animal-list.component.ts) | `AnimalListComponent` |
| [src/frontend/src/app/pages/animal-timeline/animal-timeline.component.css](../../src/frontend/src/app/pages/animal-timeline/animal-timeline.component.css) | Application/component styles |
| [src/frontend/src/app/pages/animal-timeline/animal-timeline.component.html](../../src/frontend/src/app/pages/animal-timeline/animal-timeline.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/animal-timeline/animal-timeline.component.ts](../../src/frontend/src/app/pages/animal-timeline/animal-timeline.component.ts) | `AnimalTimelineComponent` |
| [src/frontend/src/app/pages/cereri-admin/cereri-admin.component.css](../../src/frontend/src/app/pages/cereri-admin/cereri-admin.component.css) | Application/component styles |
| [src/frontend/src/app/pages/cereri-admin/cereri-admin.component.html](../../src/frontend/src/app/pages/cereri-admin/cereri-admin.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/cereri-admin/cereri-admin.component.ts](../../src/frontend/src/app/pages/cereri-admin/cereri-admin.component.ts) | `CereriAdminComponent` |
| [src/frontend/src/app/pages/cladire-management/cladire-management.component.html](../../src/frontend/src/app/pages/cladire-management/cladire-management.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/cladire-management/cladire-management.component.spec.ts](../../src/frontend/src/app/pages/cladire-management/cladire-management.component.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/pages/cladire-management/cladire-management.component.ts](../../src/frontend/src/app/pages/cladire-management/cladire-management.component.ts) | `CladireManagementComponent` |
| [src/frontend/src/app/pages/contract-management/contract-management.component.html](../../src/frontend/src/app/pages/contract-management/contract-management.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/contract-management/contract-management.component.scss](../../src/frontend/src/app/pages/contract-management/contract-management.component.scss) | Application/component styles |
| [src/frontend/src/app/pages/contract-management/contract-management.component.ts](../../src/frontend/src/app/pages/contract-management/contract-management.component.ts) | `ContractManagementComponent` |
| [src/frontend/src/app/pages/create-tenant/create-tenant.component.html](../../src/frontend/src/app/pages/create-tenant/create-tenant.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/create-tenant/create-tenant.component.ts](../../src/frontend/src/app/pages/create-tenant/create-tenant.component.ts) | `CreateTenantComponent` |
| [src/frontend/src/app/pages/document-management/document-management.component.html](../../src/frontend/src/app/pages/document-management/document-management.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/document-management/document-management.component.ts](../../src/frontend/src/app/pages/document-management/document-management.component.ts) | `DocumentManagementComponent` |
| [src/frontend/src/app/pages/efectiv-grup-form/efectiv-grup-form.component.html](../../src/frontend/src/app/pages/efectiv-grup-form/efectiv-grup-form.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/efectiv-grup-form/efectiv-grup-form.component.ts](../../src/frontend/src/app/pages/efectiv-grup-form/efectiv-grup-form.component.ts) | `EfectivGrupFormComponent` |
| [src/frontend/src/app/pages/evidenta-chimica/evidenta-chimica.component.css](../../src/frontend/src/app/pages/evidenta-chimica/evidenta-chimica.component.css) | Application/component styles |
| [src/frontend/src/app/pages/evidenta-chimica/evidenta-chimica.component.html](../../src/frontend/src/app/pages/evidenta-chimica/evidenta-chimica.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/evidenta-chimica/evidenta-chimica.component.ts](../../src/frontend/src/app/pages/evidenta-chimica/evidenta-chimica.component.ts) | `EvidentaChimicaComponent` |
| [src/frontend/src/app/pages/gospodarie-details/gospodarie-details.component.css](../../src/frontend/src/app/pages/gospodarie-details/gospodarie-details.component.css) | Application/component styles |
| [src/frontend/src/app/pages/gospodarie-details/gospodarie-details.component.html](../../src/frontend/src/app/pages/gospodarie-details/gospodarie-details.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/gospodarie-details/gospodarie-details.component.spec.ts](../../src/frontend/src/app/pages/gospodarie-details/gospodarie-details.component.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/pages/gospodarie-details/gospodarie-details.component.ts](../../src/frontend/src/app/pages/gospodarie-details/gospodarie-details.component.ts) | `GospodarieDetailsComponent` |
| [src/frontend/src/app/pages/gospodarie-form/gospodarie-form.component.css](../../src/frontend/src/app/pages/gospodarie-form/gospodarie-form.component.css) | Application/component styles |
| [src/frontend/src/app/pages/gospodarie-form/gospodarie-form.component.html](../../src/frontend/src/app/pages/gospodarie-form/gospodarie-form.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/gospodarie-form/gospodarie-form.component.spec.ts](../../src/frontend/src/app/pages/gospodarie-form/gospodarie-form.component.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/pages/gospodarie-form/gospodarie-form.component.ts](../../src/frontend/src/app/pages/gospodarie-form/gospodarie-form.component.ts) | `GospodarieFormComponent` |
| [src/frontend/src/app/pages/gospodarie-list/gospodarie-list.component.html](../../src/frontend/src/app/pages/gospodarie-list/gospodarie-list.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/gospodarie-list/gospodarie-list.component.spec.ts](../../src/frontend/src/app/pages/gospodarie-list/gospodarie-list.component.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/pages/gospodarie-list/gospodarie-list.component.ts](../../src/frontend/src/app/pages/gospodarie-list/gospodarie-list.component.ts) | `GospodarieListComponent` |
| [src/frontend/src/app/pages/machinery-management/machinery-management.component.html](../../src/frontend/src/app/pages/machinery-management/machinery-management.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/machinery-management/machinery-management.component.ts](../../src/frontend/src/app/pages/machinery-management/machinery-management.component.ts) | `MachineryManagementComponent` |
| [src/frontend/src/app/pages/notificare-succesiune/notificare-succesiune.component.html](../../src/frontend/src/app/pages/notificare-succesiune/notificare-succesiune.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/notificare-succesiune/notificare-succesiune.component.ts](../../src/frontend/src/app/pages/notificare-succesiune/notificare-succesiune.component.ts) | `NotificareSuccesiuneComponent` |
| [src/frontend/src/app/pages/persoana-form/persoana-form.component.html](../../src/frontend/src/app/pages/persoana-form/persoana-form.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/persoana-form/persoana-form.component.ts](../../src/frontend/src/app/pages/persoana-form/persoana-form.component.ts) | `PersonFormComponent` |
| [src/frontend/src/app/pages/persoana-list/persoana-list.component.html](../../src/frontend/src/app/pages/persoana-list/persoana-list.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/persoana-list/persoana-list.component.ts](../../src/frontend/src/app/pages/persoana-list/persoana-list.component.ts) | `PersonListComponent` |
| [src/frontend/src/app/pages/statistici/statistici.component.css](../../src/frontend/src/app/pages/statistici/statistici.component.css) | Application/component styles |
| [src/frontend/src/app/pages/statistici/statistici.component.html](../../src/frontend/src/app/pages/statistici/statistici.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/statistici/statistici.component.ts](../../src/frontend/src/app/pages/statistici/statistici.component.ts) | `StatisticiComponent` |
| [src/frontend/src/app/pages/super-admin-dashboard/super-admin-dashboard.component.html](../../src/frontend/src/app/pages/super-admin-dashboard/super-admin-dashboard.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/super-admin-dashboard/super-admin-dashboard.component.ts](../../src/frontend/src/app/pages/super-admin-dashboard/super-admin-dashboard.component.ts) | `SuperAdminDashboardComponent` |
| [src/frontend/src/app/pages/tenant-admin-dashboard/tenant-admin-dashboard.component.html](../../src/frontend/src/app/pages/tenant-admin-dashboard/tenant-admin-dashboard.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/tenant-admin-dashboard/tenant-admin-dashboard.component.ts](../../src/frontend/src/app/pages/tenant-admin-dashboard/tenant-admin-dashboard.component.ts) | `TenantAdminDashboardComponent` |
| [src/frontend/src/app/pages/teren-form/teren-form.component.css](../../src/frontend/src/app/pages/teren-form/teren-form.component.css) | Application/component styles |
| [src/frontend/src/app/pages/teren-form/teren-form.component.html](../../src/frontend/src/app/pages/teren-form/teren-form.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/teren-form/teren-form.component.ts](../../src/frontend/src/app/pages/teren-form/teren-form.component.ts) | `TerenFormComponent` |
| [src/frontend/src/app/pages/teren-parcele/teren-parcele.component.css](../../src/frontend/src/app/pages/teren-parcele/teren-parcele.component.css) | Application/component styles |
| [src/frontend/src/app/pages/teren-parcele/teren-parcele.component.html](../../src/frontend/src/app/pages/teren-parcele/teren-parcele.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/teren-parcele/teren-parcele.component.ts](../../src/frontend/src/app/pages/teren-parcele/teren-parcele.component.ts) | `TerenParceleComponent` |
| [src/frontend/src/app/pages/uat-details/uat-details.component.css](../../src/frontend/src/app/pages/uat-details/uat-details.component.css) | Application/component styles |
| [src/frontend/src/app/pages/uat-details/uat-details.component.html](../../src/frontend/src/app/pages/uat-details/uat-details.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/uat-details/uat-details.component.spec.ts](../../src/frontend/src/app/pages/uat-details/uat-details.component.spec.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/pages/uat-details/uat-details.component.ts](../../src/frontend/src/app/pages/uat-details/uat-details.component.ts) | `UAT`, `UatDetailsComponent` |
| [src/frontend/src/app/pages/uat-management/uat-management.component.html](../../src/frontend/src/app/pages/uat-management/uat-management.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/uat-management/uat-management.component.scss](../../src/frontend/src/app/pages/uat-management/uat-management.component.scss) | Application/component styles |
| [src/frontend/src/app/pages/uat-management/uat-management.component.ts](../../src/frontend/src/app/pages/uat-management/uat-management.component.ts) | `UAT`, `UatManagementComponent` |
| [src/frontend/src/app/pages/user-management/user-management.component.html](../../src/frontend/src/app/pages/user-management/user-management.component.html) | Angular / email / PDF template |
| [src/frontend/src/app/pages/user-management/user-management.component.ts](../../src/frontend/src/app/pages/user-management/user-management.component.ts) | `UserManagementComponent` |
| [src/frontend/src/app/services/animal.service.ts](../../src/frontend/src/app/services/animal.service.ts) | `AnimalService` |
| [src/frontend/src/app/services/auth.service.ts](../../src/frontend/src/app/services/auth.service.ts) | `UserInfo`, `AuthService` |
| [src/frontend/src/app/services/carte-funciara.service.ts](../../src/frontend/src/app/services/carte-funciara.service.ts) | `CarteFunciaraService` |
| [src/frontend/src/app/services/catalog-ingrasaminte.service.ts](../../src/frontend/src/app/services/catalog-ingrasaminte.service.ts) | `CatalogIngrasaminteService` |
| [src/frontend/src/app/services/catalog-ppp.service.ts](../../src/frontend/src/app/services/catalog-ppp.service.ts) | `CatalogPppService` |
| [src/frontend/src/app/services/categorie-folosinta.service.ts](../../src/frontend/src/app/services/categorie-folosinta.service.ts) | `CategorieFolosintaService` |
| [src/frontend/src/app/services/ciclu-productie.service.ts](../../src/frontend/src/app/services/ciclu-productie.service.ts) | `CicluProductieService` |
| [src/frontend/src/app/services/cladire.service.ts](../../src/frontend/src/app/services/cladire.service.ts) | `CladireService` |
| [src/frontend/src/app/services/contract-utilizare.service.ts](../../src/frontend/src/app/services/contract-utilizare.service.ts) | `ContractUtilizare`, `ContractUtilizareRequest`, `ContractUtilizareService` |
| [src/frontend/src/app/services/coord-conversion.service.ts](../../src/frontend/src/app/services/coord-conversion.service.ts) | `CoordConversionService` |
| [src/frontend/src/app/services/cultura-parcela.service.ts](../../src/frontend/src/app/services/cultura-parcela.service.ts) | `CulturaParcelaService` |
| [src/frontend/src/app/services/document.service.ts](../../src/frontend/src/app/services/document.service.ts) | `DocumentEntity`, `DocumentUploadRequest`, `TipDocument`, `DocumentService` |
| [src/frontend/src/app/services/fertilizare.service.ts](../../src/frontend/src/app/services/fertilizare.service.ts) | `FertilizareService` |
| [src/frontend/src/app/services/fila-parcelei.service.ts](../../src/frontend/src/app/services/fila-parcelei.service.ts) | `FilaParceleiService` |
| [src/frontend/src/app/services/gospodarie.service.ts](../../src/frontend/src/app/services/gospodarie.service.ts) | `GospodarieService` |
| [src/frontend/src/app/services/jwt.interceptor.ts](../../src/frontend/src/app/services/jwt.interceptor.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/app/services/lookup.service.ts](../../src/frontend/src/app/services/lookup.service.ts) | `LookupService` |
| [src/frontend/src/app/services/machinery.service.ts](../../src/frontend/src/app/services/machinery.service.ts) | `MachineryService` |
| [src/frontend/src/app/services/notificare-succesiune.service.ts](../../src/frontend/src/app/services/notificare-succesiune.service.ts) | `NotificareSuccesiuneService` |
| [src/frontend/src/app/services/padure.service.ts](../../src/frontend/src/app/services/padure.service.ts) | `PadureService` |
| [src/frontend/src/app/services/parcela.service.ts](../../src/frontend/src/app/services/parcela.service.ts) | `ParcelaService` |
| [src/frontend/src/app/services/pasune-faneata.service.ts](../../src/frontend/src/app/services/pasune-faneata.service.ts) | `PasuneFaneataService` |
| [src/frontend/src/app/services/persoana.service.ts](../../src/frontend/src/app/services/persoana.service.ts) | `PersoanaService` |
| [src/frontend/src/app/services/pom.service.ts](../../src/frontend/src/app/services/pom.service.ts) | `PomService` |
| [src/frontend/src/app/services/raport-statistic.service.ts](../../src/frontend/src/app/services/raport-statistic.service.ts) | `RaportStatisticService` |
| [src/frontend/src/app/services/recoltare.service.ts](../../src/frontend/src/app/services/recoltare.service.ts) | `CentralizatorRecoltare`, `RecoltareService` |
| [src/frontend/src/app/services/street-autocomplete.service.ts](../../src/frontend/src/app/services/street-autocomplete.service.ts) | `NominatimAddress`, `NominatimResult`, `StreetAutocompleteService` |
| [src/frontend/src/app/services/sursa-apa.service.ts](../../src/frontend/src/app/services/sursa-apa.service.ts) | `SursaApaService` |
| [src/frontend/src/app/services/teren.service.ts](../../src/frontend/src/app/services/teren.service.ts) | `TerenService` |
| [src/frontend/src/app/services/translate.pipe.ts](../../src/frontend/src/app/services/translate.pipe.ts) | `AppTranslatePipe` |
| [src/frontend/src/app/services/tratament-fitosanitar.service.ts](../../src/frontend/src/app/services/tratament-fitosanitar.service.ts) | `TratamentFitosanitarService` |
| [src/frontend/src/app/services/uat-context.service.ts](../../src/frontend/src/app/services/uat-context.service.ts) | `UatContextService` |
| [src/frontend/src/app/services/uat.service.ts](../../src/frontend/src/app/services/uat.service.ts) | `UatService` |
| [src/frontend/src/app/services/vita-de-vie.service.ts](../../src/frontend/src/app/services/vita-de-vie.service.ts) | `VitaDeVieService` |
| [src/frontend/src/app/shared/utils/leaflet-esm.ts](../../src/frontend/src/app/shared/utils/leaflet-esm.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/environments/environment.prod.template.ts](../../src/frontend/src/environments/environment.prod.template.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/environments/environment.prod.ts](../../src/frontend/src/environments/environment.prod.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/environments/environment.template.ts](../../src/frontend/src/environments/environment.template.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/environments/environment.ts](../../src/frontend/src/environments/environment.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/index.html](../../src/frontend/src/index.html) | Angular / email / PDF template |
| [src/frontend/src/locale/messages.en.xlf](../../src/frontend/src/locale/messages.en.xlf) | Angular translation messages |
| [src/frontend/src/locale/messages.xlf](../../src/frontend/src/locale/messages.xlf) | Angular translation messages |
| [src/frontend/src/main.ts](../../src/frontend/src/main.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/styles.css](../../src/frontend/src/styles.css) | Application/component styles |
| [src/frontend/src/styles.scss](../../src/frontend/src/styles.scss) | Application/component styles |
| [src/frontend/src/typings.d.ts](../../src/frontend/src/typings.d.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/src/typings/leaflet-esm.d.ts](../../src/frontend/src/typings/leaflet-esm.d.ts) | Configuration / bootstrap / utility; see source |
| [src/frontend/tsconfig.app.json](../../src/frontend/tsconfig.app.json) | Workspace, dependency lock, proxy, data, or compiler configuration |
| [src/frontend/tsconfig.json](../../src/frontend/tsconfig.json) | Workspace, dependency lock, proxy, data, or compiler configuration |

## Shared backend source and configuration

| Source file | Declared type / responsibility indicator |
| --- | --- |
| [src/backend/DbCheck.java](../../src/backend/DbCheck.java) | `DbCheck` |
| [src/backend/Dockerfile](../../src/backend/Dockerfile) | Container build/runtime |
| [src/backend/pom.xml](../../src/backend/pom.xml) | Configuration / bootstrap / utility; see source |
| [src/backend/src/main/java/com/multitenant/BackendApplication.java](../../src/backend/src/main/java/com/multitenant/BackendApplication.java) | `BackendApplication` |
| [src/backend/src/main/java/com/multitenant/annotation/GdprAudited.java](../../src/backend/src/main/java/com/multitenant/annotation/GdprAudited.java) | Configuration / bootstrap / utility; see source |
| [src/backend/src/main/java/com/multitenant/annotation/TenantRequired.java](../../src/backend/src/main/java/com/multitenant/annotation/TenantRequired.java) | Configuration / bootstrap / utility; see source |
| [src/backend/src/main/java/com/multitenant/aspect/GdprAuditAspect.java](../../src/backend/src/main/java/com/multitenant/aspect/GdprAuditAspect.java) | `GdprAuditAspect` |
| [src/backend/src/main/java/com/multitenant/aspect/TenantRequiredAspect.java](../../src/backend/src/main/java/com/multitenant/aspect/TenantRequiredAspect.java) | `TenantRequiredAspect` |
| [src/backend/src/main/java/com/multitenant/config/DatabaseSeeder.java](../../src/backend/src/main/java/com/multitenant/config/DatabaseSeeder.java) | `DatabaseSeeder` |
| [src/backend/src/main/java/com/multitenant/config/JacksonConfig.java](../../src/backend/src/main/java/com/multitenant/config/JacksonConfig.java) | `JacksonConfig` |
| [src/backend/src/main/java/com/multitenant/config/KafkaTopicConfig.java](../../src/backend/src/main/java/com/multitenant/config/KafkaTopicConfig.java) | `KafkaTopicConfig` |
| [src/backend/src/main/java/com/multitenant/config/ModelMapperConfig.java](../../src/backend/src/main/java/com/multitenant/config/ModelMapperConfig.java) | `ModelMapperConfig` |
| [src/backend/src/main/java/com/multitenant/config/WebSocketConfig.java](../../src/backend/src/main/java/com/multitenant/config/WebSocketConfig.java) | `WebSocketConfig` |
| [src/backend/src/main/java/com/multitenant/config/tenant/JpaConfig.java](../../src/backend/src/main/java/com/multitenant/config/tenant/JpaConfig.java) | `JpaConfig` |
| [src/backend/src/main/java/com/multitenant/config/tenant/MultiTenantConnectionProviderImpl.java](../../src/backend/src/main/java/com/multitenant/config/tenant/MultiTenantConnectionProviderImpl.java) | `MultiTenantConnectionProviderImpl` |
| [src/backend/src/main/java/com/multitenant/config/tenant/TenantContext.java](../../src/backend/src/main/java/com/multitenant/config/tenant/TenantContext.java) | `TenantContext` |
| [src/backend/src/main/java/com/multitenant/config/tenant/TenantFilter.java](../../src/backend/src/main/java/com/multitenant/config/tenant/TenantFilter.java) | `TenantFilter` |
| [src/backend/src/main/java/com/multitenant/config/tenant/TenantIdentifierResolver.java](../../src/backend/src/main/java/com/multitenant/config/tenant/TenantIdentifierResolver.java) | `TenantIdentifierResolver` |
| [src/backend/src/main/java/com/multitenant/controller/AdeverintaController.java](../../src/backend/src/main/java/com/multitenant/controller/AdeverintaController.java) | `AdeverintaController` |
| [src/backend/src/main/java/com/multitenant/controller/AdminCerereController.java](../../src/backend/src/main/java/com/multitenant/controller/AdminCerereController.java) | `AdminCerereController` |
| [src/backend/src/main/java/com/multitenant/controller/AnimalController.java](../../src/backend/src/main/java/com/multitenant/controller/AnimalController.java) | `AnimalController` |
| [src/backend/src/main/java/com/multitenant/controller/AtestatController.java](../../src/backend/src/main/java/com/multitenant/controller/AtestatController.java) | `AtestatController` |
| [src/backend/src/main/java/com/multitenant/controller/AuthController.java](../../src/backend/src/main/java/com/multitenant/controller/AuthController.java) | `AuthController` |
| [src/backend/src/main/java/com/multitenant/controller/CarteFunciaraController.java](../../src/backend/src/main/java/com/multitenant/controller/CarteFunciaraController.java) | `CarteFunciaraController` |
| [src/backend/src/main/java/com/multitenant/controller/CatalogIngrasaminteController.java](../../src/backend/src/main/java/com/multitenant/controller/CatalogIngrasaminteController.java) | `CatalogIngrasaminteController` |
| [src/backend/src/main/java/com/multitenant/controller/CatalogPppController.java](../../src/backend/src/main/java/com/multitenant/controller/CatalogPppController.java) | `CatalogPppController` |
| [src/backend/src/main/java/com/multitenant/controller/CategorieFolosintaController.java](../../src/backend/src/main/java/com/multitenant/controller/CategorieFolosintaController.java) | `CategorieFolosintaController` |
| [src/backend/src/main/java/com/multitenant/controller/CerereController.java](../../src/backend/src/main/java/com/multitenant/controller/CerereController.java) | `CerereController` |
| [src/backend/src/main/java/com/multitenant/controller/CererePdfController.java](../../src/backend/src/main/java/com/multitenant/controller/CererePdfController.java) | `CererePdfController` |
| [src/backend/src/main/java/com/multitenant/controller/CetateanAuthController.java](../../src/backend/src/main/java/com/multitenant/controller/CetateanAuthController.java) | `CetateanAuthController` |
| [src/backend/src/main/java/com/multitenant/controller/CicluProductieController.java](../../src/backend/src/main/java/com/multitenant/controller/CicluProductieController.java) | `CicluProductieController` |
| [src/backend/src/main/java/com/multitenant/controller/CladireController.java](../../src/backend/src/main/java/com/multitenant/controller/CladireController.java) | `CladireController` |
| [src/backend/src/main/java/com/multitenant/controller/ContractUtilizareController.java](../../src/backend/src/main/java/com/multitenant/controller/ContractUtilizareController.java) | `ContractUtilizareController` |
| [src/backend/src/main/java/com/multitenant/controller/CrossTenantLookupController.java](../../src/backend/src/main/java/com/multitenant/controller/CrossTenantLookupController.java) | `CrossTenantLookupController` |
| [src/backend/src/main/java/com/multitenant/controller/CulturaParcelaController.java](../../src/backend/src/main/java/com/multitenant/controller/CulturaParcelaController.java) | `CulturaParcelaController` |
| [src/backend/src/main/java/com/multitenant/controller/DocumentController.java](../../src/backend/src/main/java/com/multitenant/controller/DocumentController.java) | `DocumentController` |
| [src/backend/src/main/java/com/multitenant/controller/FactoriMediuController.java](../../src/backend/src/main/java/com/multitenant/controller/FactoriMediuController.java) | `FactoriMediuController` |
| [src/backend/src/main/java/com/multitenant/controller/FertilizareController.java](../../src/backend/src/main/java/com/multitenant/controller/FertilizareController.java) | `FertilizareController` |
| [src/backend/src/main/java/com/multitenant/controller/FilaParceleiController.java](../../src/backend/src/main/java/com/multitenant/controller/FilaParceleiController.java) | `FilaParceleiController` |
| [src/backend/src/main/java/com/multitenant/controller/GospodarieController.java](../../src/backend/src/main/java/com/multitenant/controller/GospodarieController.java) | `GospodarieController` |
| [src/backend/src/main/java/com/multitenant/controller/LookupController.java](../../src/backend/src/main/java/com/multitenant/controller/LookupController.java) | `LookupController` |
| [src/backend/src/main/java/com/multitenant/controller/MachineryController.java](../../src/backend/src/main/java/com/multitenant/controller/MachineryController.java) | `MachineryController` |
| [src/backend/src/main/java/com/multitenant/controller/NominatimProxyController.java](../../src/backend/src/main/java/com/multitenant/controller/NominatimProxyController.java) | `NominatimProxyController` |
| [src/backend/src/main/java/com/multitenant/controller/NotificareSuccesiuneController.java](../../src/backend/src/main/java/com/multitenant/controller/NotificareSuccesiuneController.java) | `NotificareSuccesiuneController` |
| [src/backend/src/main/java/com/multitenant/controller/PadureController.java](../../src/backend/src/main/java/com/multitenant/controller/PadureController.java) | `PadureController` |
| [src/backend/src/main/java/com/multitenant/controller/ParcelaController.java](../../src/backend/src/main/java/com/multitenant/controller/ParcelaController.java) | `ParcelaController` |
| [src/backend/src/main/java/com/multitenant/controller/PasuneFaneataController.java](../../src/backend/src/main/java/com/multitenant/controller/PasuneFaneataController.java) | `PasuneFaneataController` |
| [src/backend/src/main/java/com/multitenant/controller/PersoanaController.java](../../src/backend/src/main/java/com/multitenant/controller/PersoanaController.java) | `PersoanaController` |
| [src/backend/src/main/java/com/multitenant/controller/PomController.java](../../src/backend/src/main/java/com/multitenant/controller/PomController.java) | `PomController` |
| [src/backend/src/main/java/com/multitenant/controller/PublicCitizenController.java](../../src/backend/src/main/java/com/multitenant/controller/PublicCitizenController.java) | `PublicCitizenController` |
| [src/backend/src/main/java/com/multitenant/controller/PublicUatEndpointController.java](../../src/backend/src/main/java/com/multitenant/controller/PublicUatEndpointController.java) | `PublicUatEndpointController` |
| [src/backend/src/main/java/com/multitenant/controller/RaportStatisticController.java](../../src/backend/src/main/java/com/multitenant/controller/RaportStatisticController.java) | `RaportStatisticController` |
| [src/backend/src/main/java/com/multitenant/controller/RecoltareController.java](../../src/backend/src/main/java/com/multitenant/controller/RecoltareController.java) | `RecoltareController` |
| [src/backend/src/main/java/com/multitenant/controller/SursaApaController.java](../../src/backend/src/main/java/com/multitenant/controller/SursaApaController.java) | `SursaApaController` |
| [src/backend/src/main/java/com/multitenant/controller/TenantController.java](../../src/backend/src/main/java/com/multitenant/controller/TenantController.java) | `TenantController` |
| [src/backend/src/main/java/com/multitenant/controller/TerenController.java](../../src/backend/src/main/java/com/multitenant/controller/TerenController.java) | `TerenController` |
| [src/backend/src/main/java/com/multitenant/controller/TratamentFitosanitarController.java](../../src/backend/src/main/java/com/multitenant/controller/TratamentFitosanitarController.java) | `TratamentFitosanitarController` |
| [src/backend/src/main/java/com/multitenant/controller/UatController.java](../../src/backend/src/main/java/com/multitenant/controller/UatController.java) | `UatController` |
| [src/backend/src/main/java/com/multitenant/controller/UserController.java](../../src/backend/src/main/java/com/multitenant/controller/UserController.java) | `UserController` |
| [src/backend/src/main/java/com/multitenant/controller/VitaDeVieController.java](../../src/backend/src/main/java/com/multitenant/controller/VitaDeVieController.java) | `VitaDeVieController` |
| [src/backend/src/main/java/com/multitenant/converter/AesCryptoConverter.java](../../src/backend/src/main/java/com/multitenant/converter/AesCryptoConverter.java) | `AesCryptoConverter` |
| [src/backend/src/main/java/com/multitenant/dto/AnimalIndividualDTO.java](../../src/backend/src/main/java/com/multitenant/dto/AnimalIndividualDTO.java) | `AnimalIndividualDTO` |
| [src/backend/src/main/java/com/multitenant/dto/AtestatStatusDTO.java](../../src/backend/src/main/java/com/multitenant/dto/AtestatStatusDTO.java) | `AtestatStatusDTO` |
| [src/backend/src/main/java/com/multitenant/dto/CarteFunciaraDTO.java](../../src/backend/src/main/java/com/multitenant/dto/CarteFunciaraDTO.java) | `CarteFunciaraDTO` |
| [src/backend/src/main/java/com/multitenant/dto/CatalogIngrasaminteDTO.java](../../src/backend/src/main/java/com/multitenant/dto/CatalogIngrasaminteDTO.java) | `CatalogIngrasaminteDTO` |
| [src/backend/src/main/java/com/multitenant/dto/CatalogPppDTO.java](../../src/backend/src/main/java/com/multitenant/dto/CatalogPppDTO.java) | `CatalogPppDTO` |
| [src/backend/src/main/java/com/multitenant/dto/CentralizatorRecoltareDto.java](../../src/backend/src/main/java/com/multitenant/dto/CentralizatorRecoltareDto.java) | `CentralizatorRecoltareDto` |
| [src/backend/src/main/java/com/multitenant/dto/CerereDTO.java](../../src/backend/src/main/java/com/multitenant/dto/CerereDTO.java) | `CerereDTO` |
| [src/backend/src/main/java/com/multitenant/dto/CicluProductieDTO.java](../../src/backend/src/main/java/com/multitenant/dto/CicluProductieDTO.java) | `CicluProductieDTO` |
| [src/backend/src/main/java/com/multitenant/dto/CladireDTO.java](../../src/backend/src/main/java/com/multitenant/dto/CladireDTO.java) | `CladireDTO` |
| [src/backend/src/main/java/com/multitenant/dto/ContractUtilizareDTO.java](../../src/backend/src/main/java/com/multitenant/dto/ContractUtilizareDTO.java) | `ContractUtilizareDTO` |
| [src/backend/src/main/java/com/multitenant/dto/ContractUtilizareResponseDTO.java](../../src/backend/src/main/java/com/multitenant/dto/ContractUtilizareResponseDTO.java) | `ContractUtilizareResponseDTO` |
| [src/backend/src/main/java/com/multitenant/dto/CulturaParcelaDto.java](../../src/backend/src/main/java/com/multitenant/dto/CulturaParcelaDto.java) | `CulturaParcelaDto` |
| [src/backend/src/main/java/com/multitenant/dto/DocumentDTO.java](../../src/backend/src/main/java/com/multitenant/dto/DocumentDTO.java) | `DocumentDTO` |
| [src/backend/src/main/java/com/multitenant/dto/EfectivGrupDTO.java](../../src/backend/src/main/java/com/multitenant/dto/EfectivGrupDTO.java) | `EfectivGrupDTO` |
| [src/backend/src/main/java/com/multitenant/dto/EvenimentAnimalDTO.java](../../src/backend/src/main/java/com/multitenant/dto/EvenimentAnimalDTO.java) | `EvenimentAnimalDTO` |
| [src/backend/src/main/java/com/multitenant/dto/FactoriMediuDTO.java](../../src/backend/src/main/java/com/multitenant/dto/FactoriMediuDTO.java) | `FactoriMediuDTO` |
| [src/backend/src/main/java/com/multitenant/dto/FertilizareDTO.java](../../src/backend/src/main/java/com/multitenant/dto/FertilizareDTO.java) | `FertilizareDTO` |
| [src/backend/src/main/java/com/multitenant/dto/FieldDiff.java](../../src/backend/src/main/java/com/multitenant/dto/FieldDiff.java) | `FieldDiff` |
| [src/backend/src/main/java/com/multitenant/dto/FilaParceleiDTO.java](../../src/backend/src/main/java/com/multitenant/dto/FilaParceleiDTO.java) | `FilaParceleiDTO` |
| [src/backend/src/main/java/com/multitenant/dto/GospodarieDTO.java](../../src/backend/src/main/java/com/multitenant/dto/GospodarieDTO.java) | `GospodarieDTO` |
| [src/backend/src/main/java/com/multitenant/dto/IstoricMembruDTO.java](../../src/backend/src/main/java/com/multitenant/dto/IstoricMembruDTO.java) | `IstoricMembruDTO` |
| [src/backend/src/main/java/com/multitenant/dto/MachineryDTO.java](../../src/backend/src/main/java/com/multitenant/dto/MachineryDTO.java) | `MachineryDTO` |
| [src/backend/src/main/java/com/multitenant/dto/NotificareSuccesiuneDTO.java](../../src/backend/src/main/java/com/multitenant/dto/NotificareSuccesiuneDTO.java) | `NotificareSuccesiuneDTO` |
| [src/backend/src/main/java/com/multitenant/dto/PadureDTO.java](../../src/backend/src/main/java/com/multitenant/dto/PadureDTO.java) | `PadureDTO` |
| [src/backend/src/main/java/com/multitenant/dto/ParcelaRevisionDto.java](../../src/backend/src/main/java/com/multitenant/dto/ParcelaRevisionDto.java) | `ParcelaRevisionDto` |
| [src/backend/src/main/java/com/multitenant/dto/PasuneFaneataDTO.java](../../src/backend/src/main/java/com/multitenant/dto/PasuneFaneataDTO.java) | `PasuneFaneataDTO` |
| [src/backend/src/main/java/com/multitenant/dto/PersoanaDTO.java](../../src/backend/src/main/java/com/multitenant/dto/PersoanaDTO.java) | `PersoanaDTO` |
| [src/backend/src/main/java/com/multitenant/dto/PomDTO.java](../../src/backend/src/main/java/com/multitenant/dto/PomDTO.java) | `PomDTO` |
| [src/backend/src/main/java/com/multitenant/dto/RecoltareDTO.java](../../src/backend/src/main/java/com/multitenant/dto/RecoltareDTO.java) | `RecoltareDTO` |
| [src/backend/src/main/java/com/multitenant/dto/SpecieRefDTO.java](../../src/backend/src/main/java/com/multitenant/dto/SpecieRefDTO.java) | Configuration / bootstrap / utility; see source |
| [src/backend/src/main/java/com/multitenant/dto/StatisticaAnimalDto.java](../../src/backend/src/main/java/com/multitenant/dto/StatisticaAnimalDto.java) | `StatisticaAnimalDto` |
| [src/backend/src/main/java/com/multitenant/dto/StatisticaCategorieFolosintaDto.java](../../src/backend/src/main/java/com/multitenant/dto/StatisticaCategorieFolosintaDto.java) | `StatisticaCategorieFolosintaDto` |
| [src/backend/src/main/java/com/multitenant/dto/StatisticaCulturaDto.java](../../src/backend/src/main/java/com/multitenant/dto/StatisticaCulturaDto.java) | `StatisticaCulturaDto` |
| [src/backend/src/main/java/com/multitenant/dto/StatisticaEfectivGrupDto.java](../../src/backend/src/main/java/com/multitenant/dto/StatisticaEfectivGrupDto.java) | `StatisticaEfectivGrupDto` |
| [src/backend/src/main/java/com/multitenant/dto/StatisticaUtilajDto.java](../../src/backend/src/main/java/com/multitenant/dto/StatisticaUtilajDto.java) | `StatisticaUtilajDto` |
| [src/backend/src/main/java/com/multitenant/dto/StatisticiRaportCompletDto.java](../../src/backend/src/main/java/com/multitenant/dto/StatisticiRaportCompletDto.java) | `StatisticiRaportCompletDto` |
| [src/backend/src/main/java/com/multitenant/dto/SursaApaDTO.java](../../src/backend/src/main/java/com/multitenant/dto/SursaApaDTO.java) | `SursaApaDTO` |
| [src/backend/src/main/java/com/multitenant/dto/TerenCreateDTO.java](../../src/backend/src/main/java/com/multitenant/dto/TerenCreateDTO.java) | `TerenCreateDTO` |
| [src/backend/src/main/java/com/multitenant/dto/TerenWithParcelaDTO.java](../../src/backend/src/main/java/com/multitenant/dto/TerenWithParcelaDTO.java) | `TerenWithParcelaDTO` |
| [src/backend/src/main/java/com/multitenant/dto/TipDocumentDTO.java](../../src/backend/src/main/java/com/multitenant/dto/TipDocumentDTO.java) | Configuration / bootstrap / utility; see source |
| [src/backend/src/main/java/com/multitenant/dto/TratamentFitosanitarDTO.java](../../src/backend/src/main/java/com/multitenant/dto/TratamentFitosanitarDTO.java) | `TratamentFitosanitarDTO` |
| [src/backend/src/main/java/com/multitenant/dto/TrimiteSpreSemnareRequest.java](../../src/backend/src/main/java/com/multitenant/dto/TrimiteSpreSemnareRequest.java) | `TrimiteSpreSemnareRequest` |
| [src/backend/src/main/java/com/multitenant/dto/UserDTO.java](../../src/backend/src/main/java/com/multitenant/dto/UserDTO.java) | `UserDTO` |
| [src/backend/src/main/java/com/multitenant/dto/VitaDeVieDTO.java](../../src/backend/src/main/java/com/multitenant/dto/VitaDeVieDTO.java) | `VitaDeVieDTO` |
| [src/backend/src/main/java/com/multitenant/event/CarteFunciaraEventListener.java](../../src/backend/src/main/java/com/multitenant/event/CarteFunciaraEventListener.java) | `CarteFunciaraEventListener` |
| [src/backend/src/main/java/com/multitenant/event/ParcelaAdaugataEvent.java](../../src/backend/src/main/java/com/multitenant/event/ParcelaAdaugataEvent.java) | Configuration / bootstrap / utility; see source |
| [src/backend/src/main/java/com/multitenant/event/TerenCreatedEvent.java](../../src/backend/src/main/java/com/multitenant/event/TerenCreatedEvent.java) | Configuration / bootstrap / utility; see source |
| [src/backend/src/main/java/com/multitenant/exception/GlobalExceptionHandler.java](../../src/backend/src/main/java/com/multitenant/exception/GlobalExceptionHandler.java) | `GlobalExceptionHandler` |
| [src/backend/src/main/java/com/multitenant/model/animal/AnimalIndividual.java](../../src/backend/src/main/java/com/multitenant/model/animal/AnimalIndividual.java) | `AnimalIndividual` |
| [src/backend/src/main/java/com/multitenant/model/animal/EfectivGrup.java](../../src/backend/src/main/java/com/multitenant/model/animal/EfectivGrup.java) | `EfectivGrup` |
| [src/backend/src/main/java/com/multitenant/model/animal/EvenimentAnimal.java](../../src/backend/src/main/java/com/multitenant/model/animal/EvenimentAnimal.java) | `EvenimentAnimal` |
| [src/backend/src/main/java/com/multitenant/model/animal/SexAnimal.java](../../src/backend/src/main/java/com/multitenant/model/animal/SexAnimal.java) | `SexAnimal` |
| [src/backend/src/main/java/com/multitenant/model/animal/SpecieAnimal.java](../../src/backend/src/main/java/com/multitenant/model/animal/SpecieAnimal.java) | `SpecieAnimal` |
| [src/backend/src/main/java/com/multitenant/model/animal/TipEvenimentAnimal.java](../../src/backend/src/main/java/com/multitenant/model/animal/TipEvenimentAnimal.java) | `TipEvenimentAnimal` |
| [src/backend/src/main/java/com/multitenant/model/audit/CustomRevisionEntity.java](../../src/backend/src/main/java/com/multitenant/model/audit/CustomRevisionEntity.java) | `CustomRevisionEntity` |
| [src/backend/src/main/java/com/multitenant/model/audit/CustomRevisionListener.java](../../src/backend/src/main/java/com/multitenant/model/audit/CustomRevisionListener.java) | `CustomRevisionListener` |
| [src/backend/src/main/java/com/multitenant/model/audit/GdprActionType.java](../../src/backend/src/main/java/com/multitenant/model/audit/GdprActionType.java) | `GdprActionType` |
| [src/backend/src/main/java/com/multitenant/model/audit/GdprAuditLog.java](../../src/backend/src/main/java/com/multitenant/model/audit/GdprAuditLog.java) | `GdprAuditLog` |
| [src/backend/src/main/java/com/multitenant/model/common/Adresa.java](../../src/backend/src/main/java/com/multitenant/model/common/Adresa.java) | `Adresa` |
| [src/backend/src/main/java/com/multitenant/model/core/Cetatean.java](../../src/backend/src/main/java/com/multitenant/model/core/Cetatean.java) | `Cetatean` |
| [src/backend/src/main/java/com/multitenant/model/core/PublicUat.java](../../src/backend/src/main/java/com/multitenant/model/core/PublicUat.java) | `PublicUat` |
| [src/backend/src/main/java/com/multitenant/model/core/Tenant.java](../../src/backend/src/main/java/com/multitenant/model/core/Tenant.java) | `Tenant` |
| [src/backend/src/main/java/com/multitenant/model/core/TipPersoanaCetatean.java](../../src/backend/src/main/java/com/multitenant/model/core/TipPersoanaCetatean.java) | `TipPersoanaCetatean` |
| [src/backend/src/main/java/com/multitenant/model/core/Uat.java](../../src/backend/src/main/java/com/multitenant/model/core/Uat.java) | `Uat` |
| [src/backend/src/main/java/com/multitenant/model/core/User.java](../../src/backend/src/main/java/com/multitenant/model/core/User.java) | `User` |
| [src/backend/src/main/java/com/multitenant/model/persoana/ActIdentitate.java](../../src/backend/src/main/java/com/multitenant/model/persoana/ActIdentitate.java) | `ActIdentitate`, `IdentityCardType` |
| [src/backend/src/main/java/com/multitenant/model/persoana/Persoana.java](../../src/backend/src/main/java/com/multitenant/model/persoana/Persoana.java) | `Persoana` |
| [src/backend/src/main/java/com/multitenant/model/persoana/PersoanaFizica.java](../../src/backend/src/main/java/com/multitenant/model/persoana/PersoanaFizica.java) | `PersoanaFizica` |
| [src/backend/src/main/java/com/multitenant/model/persoana/PersoanaJuridica.java](../../src/backend/src/main/java/com/multitenant/model/persoana/PersoanaJuridica.java) | `PersoanaJuridica` |
| [src/backend/src/main/java/com/multitenant/model/persoana/RelatieRudenie.java](../../src/backend/src/main/java/com/multitenant/model/persoana/RelatieRudenie.java) | `RelatieRudenie`, `KinshipType` |
| [src/backend/src/main/java/com/multitenant/model/registru/AtestatProducator.java](../../src/backend/src/main/java/com/multitenant/model/registru/AtestatProducator.java) | `AtestatProducator` |
| [src/backend/src/main/java/com/multitenant/model/registru/CarnetComercializare.java](../../src/backend/src/main/java/com/multitenant/model/registru/CarnetComercializare.java) | `CarnetComercializare` |
| [src/backend/src/main/java/com/multitenant/model/registru/CarteFunciara.java](../../src/backend/src/main/java/com/multitenant/model/registru/CarteFunciara.java) | `CarteFunciara` |
| [src/backend/src/main/java/com/multitenant/model/registru/CatalogIngrasaminte.java](../../src/backend/src/main/java/com/multitenant/model/registru/CatalogIngrasaminte.java) | `CatalogIngrasaminte` |
| [src/backend/src/main/java/com/multitenant/model/registru/CatalogPpp.java](../../src/backend/src/main/java/com/multitenant/model/registru/CatalogPpp.java) | `CatalogPpp` |
| [src/backend/src/main/java/com/multitenant/model/registru/CategorieFolosinta.java](../../src/backend/src/main/java/com/multitenant/model/registru/CategorieFolosinta.java) | `CategorieFolosinta` |
| [src/backend/src/main/java/com/multitenant/model/registru/Cerere.java](../../src/backend/src/main/java/com/multitenant/model/registru/Cerere.java) | `Cerere` |
| [src/backend/src/main/java/com/multitenant/model/registru/CicluProductie.java](../../src/backend/src/main/java/com/multitenant/model/registru/CicluProductie.java) | `CicluProductie` |
| [src/backend/src/main/java/com/multitenant/model/registru/CicluStatus.java](../../src/backend/src/main/java/com/multitenant/model/registru/CicluStatus.java) | `CicluStatus` |
| [src/backend/src/main/java/com/multitenant/model/registru/Cladire.java](../../src/backend/src/main/java/com/multitenant/model/registru/Cladire.java) | `Cladire` |
| [src/backend/src/main/java/com/multitenant/model/registru/ContractUtilizare.java](../../src/backend/src/main/java/com/multitenant/model/registru/ContractUtilizare.java) | `ContractUtilizare` |
| [src/backend/src/main/java/com/multitenant/model/registru/CulturaParcela.java](../../src/backend/src/main/java/com/multitenant/model/registru/CulturaParcela.java) | `CulturaParcela` |
| [src/backend/src/main/java/com/multitenant/model/registru/Document.java](../../src/backend/src/main/java/com/multitenant/model/registru/Document.java) | `Document` |
| [src/backend/src/main/java/com/multitenant/model/registru/FactoriMediu.java](../../src/backend/src/main/java/com/multitenant/model/registru/FactoriMediu.java) | `FactoriMediu` |
| [src/backend/src/main/java/com/multitenant/model/registru/Fertilizare.java](../../src/backend/src/main/java/com/multitenant/model/registru/Fertilizare.java) | `Fertilizare` |
| [src/backend/src/main/java/com/multitenant/model/registru/Gospodarie.java](../../src/backend/src/main/java/com/multitenant/model/registru/Gospodarie.java) | `Gospodarie` |
| [src/backend/src/main/java/com/multitenant/model/registru/IstoricMembruGospodarie.java](../../src/backend/src/main/java/com/multitenant/model/registru/IstoricMembruGospodarie.java) | `IstoricMembruGospodarie` |
| [src/backend/src/main/java/com/multitenant/model/registru/Machinery.java](../../src/backend/src/main/java/com/multitenant/model/registru/Machinery.java) | `Machinery` |
| [src/backend/src/main/java/com/multitenant/model/registru/NotificareSuccesiune.java](../../src/backend/src/main/java/com/multitenant/model/registru/NotificareSuccesiune.java) | `NotificareSuccesiune` |
| [src/backend/src/main/java/com/multitenant/model/registru/Padure.java](../../src/backend/src/main/java/com/multitenant/model/registru/Padure.java) | `Padure` |
| [src/backend/src/main/java/com/multitenant/model/registru/Parcela.java](../../src/backend/src/main/java/com/multitenant/model/registru/Parcela.java) | `Parcela` |
| [src/backend/src/main/java/com/multitenant/model/registru/PasuneFaneata.java](../../src/backend/src/main/java/com/multitenant/model/registru/PasuneFaneata.java) | `PasuneFaneata` |
| [src/backend/src/main/java/com/multitenant/model/registru/Pom.java](../../src/backend/src/main/java/com/multitenant/model/registru/Pom.java) | `Pom` |
| [src/backend/src/main/java/com/multitenant/model/registru/Recoltare.java](../../src/backend/src/main/java/com/multitenant/model/registru/Recoltare.java) | `Recoltare` |
| [src/backend/src/main/java/com/multitenant/model/registru/StatusCerere.java](../../src/backend/src/main/java/com/multitenant/model/registru/StatusCerere.java) | `StatusCerere` |
| [src/backend/src/main/java/com/multitenant/model/registru/StatusContractUtilizare.java](../../src/backend/src/main/java/com/multitenant/model/registru/StatusContractUtilizare.java) | `StatusContractUtilizare` |
| [src/backend/src/main/java/com/multitenant/model/registru/SursaApa.java](../../src/backend/src/main/java/com/multitenant/model/registru/SursaApa.java) | `SursaApa` |
| [src/backend/src/main/java/com/multitenant/model/registru/Teren.java](../../src/backend/src/main/java/com/multitenant/model/registru/Teren.java) | `Teren` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipCerere.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipCerere.java) | `TipCerere` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipContractUtilizare.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipContractUtilizare.java) | `TipContractUtilizare` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipEvenimentMembru.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipEvenimentMembru.java) | `TipEvenimentMembru` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipFolosintaPasune.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipFolosintaPasune.java) | `TipFolosintaPasune` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipGospodarie.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipGospodarie.java) | `TipGospodarie` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipInregistrarePom.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipInregistrarePom.java) | `TipInregistrarePom` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipInregistrareVita.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipInregistrareVita.java) | `TipInregistrareVita` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipMediu.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipMediu.java) | `TipMediu` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipSursaApa.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipSursaApa.java) | `TipSursaApa` |
| [src/backend/src/main/java/com/multitenant/model/registru/TipZona.java](../../src/backend/src/main/java/com/multitenant/model/registru/TipZona.java) | `TipZona` |
| [src/backend/src/main/java/com/multitenant/model/registru/TratamentFitosanitar.java](../../src/backend/src/main/java/com/multitenant/model/registru/TratamentFitosanitar.java) | `TratamentFitosanitar` |
| [src/backend/src/main/java/com/multitenant/model/registru/VitaDeVie.java](../../src/backend/src/main/java/com/multitenant/model/registru/VitaDeVie.java) | `VitaDeVie` |
| [src/backend/src/main/java/com/multitenant/payload/CetateanLoginRequest.java](../../src/backend/src/main/java/com/multitenant/payload/CetateanLoginRequest.java) | `CetateanLoginRequest` |
| [src/backend/src/main/java/com/multitenant/payload/CetateanSignupRequest.java](../../src/backend/src/main/java/com/multitenant/payload/CetateanSignupRequest.java) | `CetateanSignupRequest` |
| [src/backend/src/main/java/com/multitenant/payload/CetateanUpdateRequest.java](../../src/backend/src/main/java/com/multitenant/payload/CetateanUpdateRequest.java) | `CetateanUpdateRequest` |
| [src/backend/src/main/java/com/multitenant/payload/ImpersonateRequest.java](../../src/backend/src/main/java/com/multitenant/payload/ImpersonateRequest.java) | `ImpersonateRequest` |
| [src/backend/src/main/java/com/multitenant/payload/LoginRequest.java](../../src/backend/src/main/java/com/multitenant/payload/LoginRequest.java) | `LoginRequest` |
| [src/backend/src/main/java/com/multitenant/payload/TenantCreateRequest.java](../../src/backend/src/main/java/com/multitenant/payload/TenantCreateRequest.java) | `TenantCreateRequest` |
| [src/backend/src/main/java/com/multitenant/payload/UserInfoResponse.java](../../src/backend/src/main/java/com/multitenant/payload/UserInfoResponse.java) | `UserInfoResponse` |
| [src/backend/src/main/java/com/multitenant/repository/AnimalIndividualRepository.java](../../src/backend/src/main/java/com/multitenant/repository/AnimalIndividualRepository.java) | `AnimalIndividualRepository` |
| [src/backend/src/main/java/com/multitenant/repository/AtestatProducatorRepository.java](../../src/backend/src/main/java/com/multitenant/repository/AtestatProducatorRepository.java) | `AtestatProducatorRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CarnetComercializareRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CarnetComercializareRepository.java) | `CarnetComercializareRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CarteFunciaraRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CarteFunciaraRepository.java) | `CarteFunciaraRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CatalogIngrasaminteRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CatalogIngrasaminteRepository.java) | `CatalogIngrasaminteRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CatalogPppRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CatalogPppRepository.java) | `CatalogPppRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CategorieFolosintaRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CategorieFolosintaRepository.java) | `CategorieFolosintaRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CerereRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CerereRepository.java) | `CerereRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CicluProductieRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CicluProductieRepository.java) | `CicluProductieRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CladireRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CladireRepository.java) | `CladireRepository` |
| [src/backend/src/main/java/com/multitenant/repository/ContractUtilizareRepository.java](../../src/backend/src/main/java/com/multitenant/repository/ContractUtilizareRepository.java) | `ContractUtilizareRepository` |
| [src/backend/src/main/java/com/multitenant/repository/CulturaParcelaRepository.java](../../src/backend/src/main/java/com/multitenant/repository/CulturaParcelaRepository.java) | `CulturaParcelaRepository` |
| [src/backend/src/main/java/com/multitenant/repository/DocumentRepository.java](../../src/backend/src/main/java/com/multitenant/repository/DocumentRepository.java) | `DocumentRepository` |
| [src/backend/src/main/java/com/multitenant/repository/EfectivGrupRepository.java](../../src/backend/src/main/java/com/multitenant/repository/EfectivGrupRepository.java) | `EfectivGrupRepository` |
| [src/backend/src/main/java/com/multitenant/repository/EvenimentAnimalRepository.java](../../src/backend/src/main/java/com/multitenant/repository/EvenimentAnimalRepository.java) | `EvenimentAnimalRepository` |
| [src/backend/src/main/java/com/multitenant/repository/FactoriMediuRepository.java](../../src/backend/src/main/java/com/multitenant/repository/FactoriMediuRepository.java) | `FactoriMediuRepository` |
| [src/backend/src/main/java/com/multitenant/repository/FertilizareRepository.java](../../src/backend/src/main/java/com/multitenant/repository/FertilizareRepository.java) | `FertilizareRepository` |
| [src/backend/src/main/java/com/multitenant/repository/GdprAuditLogRepository.java](../../src/backend/src/main/java/com/multitenant/repository/GdprAuditLogRepository.java) | `GdprAuditLogRepository` |
| [src/backend/src/main/java/com/multitenant/repository/GospodarieRepository.java](../../src/backend/src/main/java/com/multitenant/repository/GospodarieRepository.java) | `GospodarieRepository` |
| [src/backend/src/main/java/com/multitenant/repository/IstoricMembruRepository.java](../../src/backend/src/main/java/com/multitenant/repository/IstoricMembruRepository.java) | `IstoricMembruRepository` |
| [src/backend/src/main/java/com/multitenant/repository/LookupRepository.java](../../src/backend/src/main/java/com/multitenant/repository/LookupRepository.java) | `LookupRepository` |
| [src/backend/src/main/java/com/multitenant/repository/MachineryRepository.java](../../src/backend/src/main/java/com/multitenant/repository/MachineryRepository.java) | `MachineryRepository` |
| [src/backend/src/main/java/com/multitenant/repository/NotificareSuccesiuneRepository.java](../../src/backend/src/main/java/com/multitenant/repository/NotificareSuccesiuneRepository.java) | `NotificareSuccesiuneRepository` |
| [src/backend/src/main/java/com/multitenant/repository/PadureRepository.java](../../src/backend/src/main/java/com/multitenant/repository/PadureRepository.java) | `PadureRepository` |
| [src/backend/src/main/java/com/multitenant/repository/ParcelaRepository.java](../../src/backend/src/main/java/com/multitenant/repository/ParcelaRepository.java) | `ParcelaRepository` |
| [src/backend/src/main/java/com/multitenant/repository/PasuneFaneataRepository.java](../../src/backend/src/main/java/com/multitenant/repository/PasuneFaneataRepository.java) | `PasuneFaneataRepository` |
| [src/backend/src/main/java/com/multitenant/repository/PersoanaRepository.java](../../src/backend/src/main/java/com/multitenant/repository/PersoanaRepository.java) | `PersoanaRepository` |
| [src/backend/src/main/java/com/multitenant/repository/PomRepository.java](../../src/backend/src/main/java/com/multitenant/repository/PomRepository.java) | `PomRepository` |
| [src/backend/src/main/java/com/multitenant/repository/PublicUatRepository.java](../../src/backend/src/main/java/com/multitenant/repository/PublicUatRepository.java) | `PublicUatRepository` |
| [src/backend/src/main/java/com/multitenant/repository/RecoltareRepository.java](../../src/backend/src/main/java/com/multitenant/repository/RecoltareRepository.java) | `RecoltareRepository` |
| [src/backend/src/main/java/com/multitenant/repository/SursaApaRepository.java](../../src/backend/src/main/java/com/multitenant/repository/SursaApaRepository.java) | `SursaApaRepository` |
| [src/backend/src/main/java/com/multitenant/repository/TenantRepository.java](../../src/backend/src/main/java/com/multitenant/repository/TenantRepository.java) | `TenantRepository` |
| [src/backend/src/main/java/com/multitenant/repository/TerenRepository.java](../../src/backend/src/main/java/com/multitenant/repository/TerenRepository.java) | `TerenRepository` |
| [src/backend/src/main/java/com/multitenant/repository/TratamentFitosanitarRepository.java](../../src/backend/src/main/java/com/multitenant/repository/TratamentFitosanitarRepository.java) | `TratamentFitosanitarRepository` |
| [src/backend/src/main/java/com/multitenant/repository/UatRepository.java](../../src/backend/src/main/java/com/multitenant/repository/UatRepository.java) | `UatRepository` |
| [src/backend/src/main/java/com/multitenant/repository/UserRepository.java](../../src/backend/src/main/java/com/multitenant/repository/UserRepository.java) | `UserRepository` |
| [src/backend/src/main/java/com/multitenant/repository/VitaDeVieRepository.java](../../src/backend/src/main/java/com/multitenant/repository/VitaDeVieRepository.java) | `VitaDeVieRepository` |
| [src/backend/src/main/java/com/multitenant/repository/core/CetateanRepository.java](../../src/backend/src/main/java/com/multitenant/repository/core/CetateanRepository.java) | `CetateanRepository` |
| [src/backend/src/main/java/com/multitenant/security/JwtAuthenticationFilter.java](../../src/backend/src/main/java/com/multitenant/security/JwtAuthenticationFilter.java) | `JwtAuthenticationFilter` |
| [src/backend/src/main/java/com/multitenant/security/JwtUtils.java](../../src/backend/src/main/java/com/multitenant/security/JwtUtils.java) | `JwtUtils` |
| [src/backend/src/main/java/com/multitenant/security/SecurityConfig.java](../../src/backend/src/main/java/com/multitenant/security/SecurityConfig.java) | `SecurityConfig` |
| [src/backend/src/main/java/com/multitenant/security/UserDetailsImpl.java](../../src/backend/src/main/java/com/multitenant/security/UserDetailsImpl.java) | `UserDetailsImpl` |
| [src/backend/src/main/java/com/multitenant/security/UserDetailsServiceImpl.java](../../src/backend/src/main/java/com/multitenant/security/UserDetailsServiceImpl.java) | `UserDetailsServiceImpl` |
| [src/backend/src/main/java/com/multitenant/security/UserSecurity.java](../../src/backend/src/main/java/com/multitenant/security/UserSecurity.java) | `UserSecurity` |
| [src/backend/src/main/java/com/multitenant/service/AnimalIndividualService.java](../../src/backend/src/main/java/com/multitenant/service/AnimalIndividualService.java) | `AnimalIndividualService` |
| [src/backend/src/main/java/com/multitenant/service/CatalogIngrasaminteService.java](../../src/backend/src/main/java/com/multitenant/service/CatalogIngrasaminteService.java) | `CatalogIngrasaminteService` |
| [src/backend/src/main/java/com/multitenant/service/CatalogPppService.java](../../src/backend/src/main/java/com/multitenant/service/CatalogPppService.java) | `CatalogPppService` |
| [src/backend/src/main/java/com/multitenant/service/CategorieFolosintaService.java](../../src/backend/src/main/java/com/multitenant/service/CategorieFolosintaService.java) | `CategorieFolosintaService` |
| [src/backend/src/main/java/com/multitenant/service/CerereService.java](../../src/backend/src/main/java/com/multitenant/service/CerereService.java) | `CerereService` |
| [src/backend/src/main/java/com/multitenant/service/CicluProductieService.java](../../src/backend/src/main/java/com/multitenant/service/CicluProductieService.java) | `CicluProductieService` |
| [src/backend/src/main/java/com/multitenant/service/CladireService.java](../../src/backend/src/main/java/com/multitenant/service/CladireService.java) | `CladireService` |
| [src/backend/src/main/java/com/multitenant/service/CladireServiceImpl.java](../../src/backend/src/main/java/com/multitenant/service/CladireServiceImpl.java) | `CladireServiceImpl` |
| [src/backend/src/main/java/com/multitenant/service/ContractExpirationScheduler.java](../../src/backend/src/main/java/com/multitenant/service/ContractExpirationScheduler.java) | `ContractExpirationScheduler` |
| [src/backend/src/main/java/com/multitenant/service/ContractKafkaProducer.java](../../src/backend/src/main/java/com/multitenant/service/ContractKafkaProducer.java) | `ContractKafkaProducer` |
| [src/backend/src/main/java/com/multitenant/service/ContractSemnaturaService.java](../../src/backend/src/main/java/com/multitenant/service/ContractSemnaturaService.java) | `ContractSemnaturaService` |
| [src/backend/src/main/java/com/multitenant/service/ContractUtilizareService.java](../../src/backend/src/main/java/com/multitenant/service/ContractUtilizareService.java) | `ContractUtilizareService` |
| [src/backend/src/main/java/com/multitenant/service/CrossTenantTransferService.java](../../src/backend/src/main/java/com/multitenant/service/CrossTenantTransferService.java) | `CrossTenantTransferService` |
| [src/backend/src/main/java/com/multitenant/service/CrotalRegistryService.java](../../src/backend/src/main/java/com/multitenant/service/CrotalRegistryService.java) | `CrotalRegistryService` |
| [src/backend/src/main/java/com/multitenant/service/CulturaParcelaService.java](../../src/backend/src/main/java/com/multitenant/service/CulturaParcelaService.java) | `CulturaParcelaService` |
| [src/backend/src/main/java/com/multitenant/service/DocumentService.java](../../src/backend/src/main/java/com/multitenant/service/DocumentService.java) | `DocumentService` |
| [src/backend/src/main/java/com/multitenant/service/EfectivGrupService.java](../../src/backend/src/main/java/com/multitenant/service/EfectivGrupService.java) | `EfectivGrupService` |
| [src/backend/src/main/java/com/multitenant/service/EmailService.java](../../src/backend/src/main/java/com/multitenant/service/EmailService.java) | `EmailService` |
| [src/backend/src/main/java/com/multitenant/service/EvenimentAnimalService.java](../../src/backend/src/main/java/com/multitenant/service/EvenimentAnimalService.java) | `EvenimentAnimalService` |
| [src/backend/src/main/java/com/multitenant/service/FactoriMediuService.java](../../src/backend/src/main/java/com/multitenant/service/FactoriMediuService.java) | `FactoriMediuService` |
| [src/backend/src/main/java/com/multitenant/service/FertilizareService.java](../../src/backend/src/main/java/com/multitenant/service/FertilizareService.java) | `FertilizareService` |
| [src/backend/src/main/java/com/multitenant/service/FilaParceleiService.java](../../src/backend/src/main/java/com/multitenant/service/FilaParceleiService.java) | `FilaParceleiService` |
| [src/backend/src/main/java/com/multitenant/service/GdprAuditService.java](../../src/backend/src/main/java/com/multitenant/service/GdprAuditService.java) | `GdprAuditService` |
| [src/backend/src/main/java/com/multitenant/service/GospodarieService.java](../../src/backend/src/main/java/com/multitenant/service/GospodarieService.java) | `GospodarieService` |
| [src/backend/src/main/java/com/multitenant/service/LookupService.java](../../src/backend/src/main/java/com/multitenant/service/LookupService.java) | `LookupService` |
| [src/backend/src/main/java/com/multitenant/service/MachineryService.java](../../src/backend/src/main/java/com/multitenant/service/MachineryService.java) | `MachineryService` |
| [src/backend/src/main/java/com/multitenant/service/MachineryServiceImpl.java](../../src/backend/src/main/java/com/multitenant/service/MachineryServiceImpl.java) | `MachineryServiceImpl` |
| [src/backend/src/main/java/com/multitenant/service/NotificareSuccesiuneKafkaProducer.java](../../src/backend/src/main/java/com/multitenant/service/NotificareSuccesiuneKafkaProducer.java) | `NotificareSuccesiuneKafkaProducer` |
| [src/backend/src/main/java/com/multitenant/service/NotificareSuccesiuneService.java](../../src/backend/src/main/java/com/multitenant/service/NotificareSuccesiuneService.java) | `NotificareSuccesiuneService` |
| [src/backend/src/main/java/com/multitenant/service/NotificareSuccesiuneServiceImpl.java](../../src/backend/src/main/java/com/multitenant/service/NotificareSuccesiuneServiceImpl.java) | `NotificareSuccesiuneServiceImpl` |
| [src/backend/src/main/java/com/multitenant/service/NotificationKafkaConsumer.java](../../src/backend/src/main/java/com/multitenant/service/NotificationKafkaConsumer.java) | `NotificationKafkaConsumer` |
| [src/backend/src/main/java/com/multitenant/service/PadureService.java](../../src/backend/src/main/java/com/multitenant/service/PadureService.java) | `PadureService` |
| [src/backend/src/main/java/com/multitenant/service/ParcelaService.java](../../src/backend/src/main/java/com/multitenant/service/ParcelaService.java) | `ParcelaService` |
| [src/backend/src/main/java/com/multitenant/service/PasuneFaneataService.java](../../src/backend/src/main/java/com/multitenant/service/PasuneFaneataService.java) | `PasuneFaneataService` |
| [src/backend/src/main/java/com/multitenant/service/PdfGeneratorService.java](../../src/backend/src/main/java/com/multitenant/service/PdfGeneratorService.java) | `PdfGeneratorService` |
| [src/backend/src/main/java/com/multitenant/service/PersoanaService.java](../../src/backend/src/main/java/com/multitenant/service/PersoanaService.java) | `PersoanaService` |
| [src/backend/src/main/java/com/multitenant/service/PomService.java](../../src/backend/src/main/java/com/multitenant/service/PomService.java) | `PomService` |
| [src/backend/src/main/java/com/multitenant/service/RaportStatisticService.java](../../src/backend/src/main/java/com/multitenant/service/RaportStatisticService.java) | `RaportStatisticService` |
| [src/backend/src/main/java/com/multitenant/service/RecoltareService.java](../../src/backend/src/main/java/com/multitenant/service/RecoltareService.java) | `RecoltareService` |
| [src/backend/src/main/java/com/multitenant/service/SursaApaService.java](../../src/backend/src/main/java/com/multitenant/service/SursaApaService.java) | `SursaApaService` |
| [src/backend/src/main/java/com/multitenant/service/TenantService.java](../../src/backend/src/main/java/com/multitenant/service/TenantService.java) | `TenantService` |
| [src/backend/src/main/java/com/multitenant/service/TerenService.java](../../src/backend/src/main/java/com/multitenant/service/TerenService.java) | `TerenService` |
| [src/backend/src/main/java/com/multitenant/service/TratamentFitosanitarService.java](../../src/backend/src/main/java/com/multitenant/service/TratamentFitosanitarService.java) | `TratamentFitosanitarService` |
| [src/backend/src/main/java/com/multitenant/service/UatService.java](../../src/backend/src/main/java/com/multitenant/service/UatService.java) | `UatService` |
| [src/backend/src/main/java/com/multitenant/service/VitaDeVieService.java](../../src/backend/src/main/java/com/multitenant/service/VitaDeVieService.java) | `VitaDeVieService` |
| [src/backend/src/main/java/com/multitenant/service/signnow/SignNowClient.java](../../src/backend/src/main/java/com/multitenant/service/signnow/SignNowClient.java) | `SignNowClient` |
| [src/backend/src/main/java/com/multitenant/util/CryptoUtils.java](../../src/backend/src/main/java/com/multitenant/util/CryptoUtils.java) | `CryptoUtils` |
| [src/backend/src/main/resources/application.yml](../../src/backend/src/main/resources/application.yml) | Configuration / bootstrap / utility; see source |
| [src/backend/src/main/resources/db/migration/V10__global_crotal_registry.sql](../../src/backend/src/main/resources/db/migration/V10__global_crotal_registry.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V11__create_cetateni_table.sql](../../src/backend/src/main/resources/db/migration/V11__create_cetateni_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V12__encrypt_cetateni_cnp.sql](../../src/backend/src/main/resources/db/migration/V12__encrypt_cetateni_cnp.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V13__create_specii_pom_lookup_table.sql](../../src/backend/src/main/resources/db/migration/V13__create_specii_pom_lookup_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V14__add_soft_delete_to_core_tables.sql](../../src/backend/src/main/resources/db/migration/V14__add_soft_delete_to_core_tables.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V15__add_tip_persoana_to_cetateni.sql](../../src/backend/src/main/resources/db/migration/V15__add_tip_persoana_to_cetateni.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V16__add_atestat_flags_to_cetateni.sql](../../src/backend/src/main/resources/db/migration/V16__add_atestat_flags_to_cetateni.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V1__init_public_schema.sql](../../src/backend/src/main/resources/db/migration/V1__init_public_schema.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V2__update_superadmin_password.sql](../../src/backend/src/main/resources/db/migration/V2__update_superadmin_password.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V3__create_public_uat_table.sql](../../src/backend/src/main/resources/db/migration/V3__create_public_uat_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V4__add_user_profile_columns.sql](../../src/backend/src/main/resources/db/migration/V4__add_user_profile_columns.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V6__add_lookup_tables.sql](../../src/backend/src/main/resources/db/migration/V6__add_lookup_tables.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V7__populate_all_romanian_localities.sql](../../src/backend/src/main/resources/db/migration/V7__populate_all_romanian_localities.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V8__rename_public_tables_to_plural.sql](../../src/backend/src/main/resources/db/migration/V8__rename_public_tables_to_plural.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/migration/V9__create_tip_document_table.sql](../../src/backend/src/main/resources/db/migration/V9__create_tip_document_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V10__update_teren_schema.sql](../../src/backend/src/main/resources/db/tenant/V10__update_teren_schema.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V11__create_categorie_folosinta_table.sql](../../src/backend/src/main/resources/db/tenant/V11__create_categorie_folosinta_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V12__create_utilaje_table.sql](../../src/backend/src/main/resources/db/tenant/V12__create_utilaje_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V13__create_cladire_table.sql](../../src/backend/src/main/resources/db/tenant/V13__create_cladire_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V14__create_animal_tables.sql](../../src/backend/src/main/resources/db/tenant/V14__create_animal_tables.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V15__create_eveniment_animal_table.sql](../../src/backend/src/main/resources/db/tenant/V15__create_eveniment_animal_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V16_1__fix_parcele_polygon_type.sql](../../src/backend/src/main/resources/db/tenant/V16_1__fix_parcele_polygon_type.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V16__animal_module_improvements.sql](../../src/backend/src/main/resources/db/tenant/V16__animal_module_improvements.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V17__create_cultura_parcela_table.sql](../../src/backend/src/main/resources/db/tenant/V17__create_cultura_parcela_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V18__rename_gospodarie_id_to_teren_id_parcele.sql](../../src/backend/src/main/resources/db/tenant/V18__rename_gospodarie_id_to_teren_id_parcele.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V19__create_contract_utilizare_table.sql](../../src/backend/src/main/resources/db/tenant/V19__create_contract_utilizare_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V1__init_tenant_schema.sql](../../src/backend/src/main/resources/db/tenant/V1__init_tenant_schema.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V20__create_surse_apa_table.sql](../../src/backend/src/main/resources/db/tenant/V20__create_surse_apa_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V21_1__recreate_contract_utilizare_if_missing.sql](../../src/backend/src/main/resources/db/tenant/V21_1__recreate_contract_utilizare_if_missing.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V21__persoana_gospodarii_many_to_many.sql](../../src/backend/src/main/resources/db/tenant/V21__persoana_gospodarii_many_to_many.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V22__fix_utilizator_operare_fk.sql](../../src/backend/src/main/resources/db/tenant/V22__fix_utilizator_operare_fk.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V23__rename_tenant_tables_to_plural.sql](../../src/backend/src/main/resources/db/tenant/V23__rename_tenant_tables_to_plural.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V24__rename_tenant_uat_to_uats.sql](../../src/backend/src/main/resources/db/tenant/V24__rename_tenant_uat_to_uats.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V25__create_document_table.sql](../../src/backend/src/main/resources/db/tenant/V25__create_document_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V26__rename_document_table_to_plural.sql](../../src/backend/src/main/resources/db/tenant/V26__rename_document_table_to_plural.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V27__contract_utilizare_teren_to_parcela.sql](../../src/backend/src/main/resources/db/tenant/V27__contract_utilizare_teren_to_parcela.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V28__add_data_inregistrare_to_efective_grup.sql](../../src/backend/src/main/resources/db/tenant/V28__add_data_inregistrare_to_efective_grup.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V29__add_destinatar_tenant_id_to_evenimente_animale.sql](../../src/backend/src/main/resources/db/tenant/V29__add_destinatar_tenant_id_to_evenimente_animale.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V2__create_person_tables.sql](../../src/backend/src/main/resources/db/tenant/V2__create_person_tables.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V30__create_carte_funciara_table.sql](../../src/backend/src/main/resources/db/tenant/V30__create_carte_funciara_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V31__extend_parcele_cf_fields.sql](../../src/backend/src/main/resources/db/tenant/V31__extend_parcele_cf_fields.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V32__create_gdpr_audit_log_table.sql](../../src/backend/src/main/resources/db/tenant/V32__create_gdpr_audit_log_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V33__create_envers_audit_tables.sql](../../src/backend/src/main/resources/db/tenant/V33__create_envers_audit_tables.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V34__create_cereri_table.sql](../../src/backend/src/main/resources/db/tenant/V34__create_cereri_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V35__add_cnp_cui_to_cereri.sql](../../src/backend/src/main/resources/db/tenant/V35__add_cnp_cui_to_cereri.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V36__add_persons_and_teren_to_envers.sql](../../src/backend/src/main/resources/db/tenant/V36__add_persons_and_teren_to_envers.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V37__encrypt_cnp_cui.sql](../../src/backend/src/main/resources/db/tenant/V37__encrypt_cnp_cui.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V38__encrypt_cereri_cnpcui.sql](../../src/backend/src/main/resources/db/tenant/V38__encrypt_cereri_cnpcui.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V39__create_pomi_table.sql](../../src/backend/src/main/resources/db/tenant/V39__create_pomi_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V3__add_register_columns_to_persons.sql](../../src/backend/src/main/resources/db/tenant/V3__add_register_columns_to_persons.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V40__create_vita_de_vie_table.sql](../../src/backend/src/main/resources/db/tenant/V40__create_vita_de_vie_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V41__create_pasuni_fanete_table.sql](../../src/backend/src/main/resources/db/tenant/V41__create_pasuni_fanete_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V42__add_soft_delete_to_tenant_tables.sql](../../src/backend/src/main/resources/db/tenant/V42__add_soft_delete_to_tenant_tables.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V43_1__create_evidenta_pesticide_ingrasaminte.sql](../../src/backend/src/main/resources/db/tenant/V43_1__create_evidenta_pesticide_ingrasaminte.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V43__add_atestate_si_carnete.sql](../../src/backend/src/main/resources/db/tenant/V43__add_atestate_si_carnete.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V44__add_created_at_to_audit_tables.sql](../../src/backend/src/main/resources/db/tenant/V44__add_created_at_to_audit_tables.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V45_2__add_head_of_household_and_member_history.sql](../../src/backend/src/main/resources/db/tenant/V45_2__add_head_of_household_and_member_history.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V45__modul_separare_productie.sql](../../src/backend/src/main/resources/db/tenant/V45__modul_separare_productie.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V46__create_evidenta_pesticide_ingrasaminte.sql](../../src/backend/src/main/resources/db/tenant/V46__create_evidenta_pesticide_ingrasaminte.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V47__add_semnatura_electronica_contract_utilizare.sql](../../src/backend/src/main/resources/db/tenant/V47__add_semnatura_electronica_contract_utilizare.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V48__redrop_utilizator_operare_fk.sql](../../src/backend/src/main/resources/db/tenant/V48__redrop_utilizator_operare_fk.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V49__add_signnow_contract_utilizare.sql](../../src/backend/src/main/resources/db/tenant/V49__add_signnow_contract_utilizare.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V4__update_gospodarie_adresa.sql](../../src/backend/src/main/resources/db/tenant/V4__update_gospodarie_adresa.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V50__create_paduri_table.sql](../../src/backend/src/main/resources/db/tenant/V50__create_paduri_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V51__add_missing_V45_columns.sql](../../src/backend/src/main/resources/db/tenant/V51__add_missing_V45_columns.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V52__add_document_to_member_history.sql](../../src/backend/src/main/resources/db/tenant/V52__add_document_to_member_history.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V53__notificari_succesiuni.sql](../../src/backend/src/main/resources/db/tenant/V53__notificari_succesiuni.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V5__create_parcele_table.sql](../../src/backend/src/main/resources/db/tenant/V5__create_parcele_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V6__create_teren_table.sql](../../src/backend/src/main/resources/db/tenant/V6__create_teren_table.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V7__link_person_to_gospodarie.sql](../../src/backend/src/main/resources/db/tenant/V7__link_person_to_gospodarie.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/db/tenant/V9__fix_uat_foreign_keys.sql](../../src/backend/src/main/resources/db/tenant/V9__fix_uat_foreign_keys.sql) | Flyway migration; [ordered catalog](Migrations.md) |
| [src/backend/src/main/resources/templates/email/email-confirmare-cerere.html](../../src/backend/src/main/resources/templates/email/email-confirmare-cerere.html) | Angular / email / PDF template |
| [src/backend/src/main/resources/templates/pdf/adeverinta-rol-agricol.html](../../src/backend/src/main/resources/templates/pdf/adeverinta-rol-agricol.html) | Angular / email / PDF template |
| [src/backend/src/main/resources/templates/pdf/adeverinta_rol.html](../../src/backend/src/main/resources/templates/pdf/adeverinta_rol.html) | Angular / email / PDF template |
| [src/backend/src/main/resources/templates/pdf/atestat_producator.html](../../src/backend/src/main/resources/templates/pdf/atestat_producator.html) | Angular / email / PDF template |
| [src/backend/src/main/resources/templates/pdf/carnet_comercializare.html](../../src/backend/src/main/resources/templates/pdf/carnet_comercializare.html) | Angular / email / PDF template |
| [src/backend/src/main/resources/templates/pdf/cerere_generica.html](../../src/backend/src/main/resources/templates/pdf/cerere_generica.html) | Angular / email / PDF template |
| [src/backend/src/main/resources/templates/pdf/registru-pesticide.html](../../src/backend/src/main/resources/templates/pdf/registru-pesticide.html) | Angular / email / PDF template |
| [src/backend/src/main/resources/templates/pdf/registru-spatii-protejate.html](../../src/backend/src/main/resources/templates/pdf/registru-spatii-protejate.html) | Angular / email / PDF template |
| [src/backend/src/main/test/java/com/multitenant/SirutaImporter.java](../../src/backend/src/main/test/java/com/multitenant/SirutaImporter.java) | `SirutaImporter` |
| [src/backend/src/test/java/com/multitenant/config/EmbeddedPostgresEnvironmentPostProcessor.java](../../src/backend/src/test/java/com/multitenant/config/EmbeddedPostgresEnvironmentPostProcessor.java) | `EmbeddedPostgresEnvironmentPostProcessor` |
| [src/backend/src/test/java/com/multitenant/controller/TenantControllerTest.java](../../src/backend/src/test/java/com/multitenant/controller/TenantControllerTest.java) | `TenantControllerTest` |
| [src/backend/src/test/java/com/multitenant/controller/UatControllerTest.java](../../src/backend/src/test/java/com/multitenant/controller/UatControllerTest.java) | `UatControllerTest` |
| [src/backend/src/test/java/com/multitenant/controller/UserControllerTest.java](../../src/backend/src/test/java/com/multitenant/controller/UserControllerTest.java) | `UserControllerTest` |
| [src/backend/src/test/java/com/multitenant/integration/GdprAuditIntegrationTest.java](../../src/backend/src/test/java/com/multitenant/integration/GdprAuditIntegrationTest.java) | `GdprAuditIntegrationTest` |
| [src/backend/src/test/java/com/multitenant/integration/MultiTenantEnversIntegrationTest.java](../../src/backend/src/test/java/com/multitenant/integration/MultiTenantEnversIntegrationTest.java) | `MultiTenantEnversIntegrationTest` |
| [src/backend/src/test/java/com/multitenant/integration/ParcelaHistoryIntegrationTest.java](../../src/backend/src/test/java/com/multitenant/integration/ParcelaHistoryIntegrationTest.java) | `ParcelaHistoryIntegrationTest` |
| [src/backend/src/test/java/com/multitenant/service/EvidentaServiceTest.java](../../src/backend/src/test/java/com/multitenant/service/EvidentaServiceTest.java) | `EvidentaServiceTest` |
| [src/backend/src/test/java/com/multitenant/service/TenantServiceTest.java](../../src/backend/src/test/java/com/multitenant/service/TenantServiceTest.java) | `TenantServiceTest` |
| [src/backend/src/test/java/com/multitenant/service/UatServiceTest.java](../../src/backend/src/test/java/com/multitenant/service/UatServiceTest.java) | `UatServiceTest` |
| [src/backend/teren_response.json](../../src/backend/teren_response.json) | Workspace, dependency lock, proxy, data, or compiler configuration |

## Root configuration

| Source file | Declared type / responsibility indicator |
| --- | --- |
| [.env.example](../../.env.example) | Configuration / bootstrap / utility; see source |
| [.gitignore](../../.gitignore) | Configuration / bootstrap / utility; see source |
| [docker-compose.yml](../../docker-compose.yml) | Configuration / bootstrap / utility; see source |

## Additional inspected material

- Five current Markdown documentation files and all 21 PNG application screenshots.
- Recovery Archive, BusinessAnalysis, Derived, Original, branch/use-case documents, mail report, walkthrough, and Word domain model; preserved in [Historical](../Historical/README.md).
- Hand-maintained CSV locality data and static UAT lists; presence does not imply an operational tenant for every locality.
- Docker/proxy/env templates and test bootstrap infrastructure. Private `.env` values and uploaded citizen documents were not copied.
