# Domain models, DTOs, and payloads

[Documentation index](../README.md) · [Database relationships](../Database.md) · [API signatures](API.md)

This reference enumerates declared instance fields and enums from current source. It supplements functional/database explanations; annotations alone do not prove an API validates every field. Controllers must invoke validation, and services/migrations can have different constraints. Some endpoints return entities while others use DTOs. Inherited fields are listed under the base type.

Sensitive fields appear by name/type only; no runtime identities, passwords, tokens, or environment values are included.

## Model

### AnimalIndividual

[Source](../../src/backend/src/main/java/com/multitenant/model/animal/AnimalIndividual.java)

Table declaration: `name = "animale_individuale"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `gospodarie` | `Gospodarie` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "gospodarie_id", nullable = false)` |
| `gospodarieId` | `Long` | `@Transient` |
| `proprietar` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "proprietar_id", nullable = false)` |
| `proprietarId` | `Long` | `@Transient` |
| `numarCrotal` | `String` | `@Column(name = "numar_crotal", unique = true)` |
| `specie` | `SpecieAnimal` | `@Enumerated(EnumType.STRING); @Column(name = "specie", nullable = false)` |
| `rasa` | `String` | `@Column(name = "rasa")` |
| `sex` | `SexAnimal` | `@Enumerated(EnumType.STRING); @Column(name = "sex", nullable = false)` |
| `dataNastere` | `LocalDate` | `@Column(name = "data_nastere")` |
| `greutateKg` | `Double` | `@Column(name = "greutate_kg")` |
| `stareActiva` | `boolean` | `@Column(name = "stare_activa", nullable = false)` |
| `tenantId` | `String` | `@Column(name = "tenant_id")` |
| `evenimente` | `List<EvenimentAnimal>` | `@OneToMany(fetch = FetchType.LAZY, mappedBy = "animal", cascade = CascadeType.ALL, orphanRemoval = true); @JsonIgnore` |

### EfectivGrup

[Source](../../src/backend/src/main/java/com/multitenant/model/animal/EfectivGrup.java)

Table declaration: `name = "efective_grup"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `gospodarie` | `Gospodarie` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "gospodarie_id", nullable = false)` |
| `gospodarieId` | `Long` | `@Transient` |
| `proprietar` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "proprietar_id", nullable = false)` |
| `proprietarId` | `Long` | `@Transient` |
| `specie` | `SpecieAnimal` | `@Enumerated(EnumType.STRING); @Column(name = "specie", nullable = false)` |
| `numarCapeteFamilii` | `int` | `@Column(name = "numar_capete_familii", nullable = false)` |
| `dataInregistrare` | `LocalDate` | `@Column(name = "data_inregistrare", nullable = false)` |
| `detalii` | `String` | `@Column(name = "detalii")` |
| `tenantId` | `String` | `@Column(name = "tenant_id")` |

### EvenimentAnimal

[Source](../../src/backend/src/main/java/com/multitenant/model/animal/EvenimentAnimal.java)

Table declaration: `name = "evenimente_animale"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `animal` | `AnimalIndividual` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "animal_id", nullable = false)` |
| `tipEveniment` | `TipEvenimentAnimal` | `@Enumerated(EnumType.STRING); @Column(name = "tip_eveniment", nullable = false)` |
| `dataEveniment` | `LocalDate` | `@Column(name = "data_eveniment", nullable = false)` |
| `detalii` | `String` | `@Column(name = "detalii", columnDefinition = "TEXT")` |
| `destinatarTenantId` | `String` | `@Column(name = "destinatar_tenant_id")` |
| `tenantId` | `String` | `@Column(name = "tenant_id")` |

### SexAnimal

[Source](../../src/backend/src/main/java/com/multitenant/model/animal/SexAnimal.java)

Values: `MASCULIN`, `FEMININ`.

### SpecieAnimal

[Source](../../src/backend/src/main/java/com/multitenant/model/animal/SpecieAnimal.java)

Values: `BOVINE`, `PORCINE`, `OVINE`, `CAPRINE`, `PASARI`, `ECVINE`, `APICOLE`, `ALTELE`.

### TipEvenimentAnimal

[Source](../../src/backend/src/main/java/com/multitenant/model/animal/TipEvenimentAnimal.java)

Values: `NASTERE`, `CUMPARARE`, `TRANSFER_INTRARE`, `TRATAMENT_VETERINAR`, `VANZARE`, `SACRIFICARE_PROPRIE`, `MOARTE`, `UCIDERE_FOCAR`, `DISPARITIE`.

### CustomRevisionEntity

[Source](../../src/backend/src/main/java/com/multitenant/model/audit/CustomRevisionEntity.java)

Table declaration: `name = "revinfo"`.

Declared mechanisms: `@RevisionEntity`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `rev` | `int` | See source/service |
| `revtstmp` | `long` | See source/service |
| `username` | `String` | `@Column(length = 255)` |

### CustomRevisionListener

[Source](../../src/backend/src/main/java/com/multitenant/model/audit/CustomRevisionListener.java)

Support/listener type; see source for behavior.

### GdprActionType

[Source](../../src/backend/src/main/java/com/multitenant/model/audit/GdprActionType.java)

Values: `VIEW`, `CREATE`, `UPDATE`, `DELETE`.

### GdprAuditLog

[Source](../../src/backend/src/main/java/com/multitenant/model/audit/GdprAuditLog.java)

Table declaration: `name = "gdpr_audit_logs"`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `timestamp` | `Instant` | `@Column(nullable = false)` |
| `utilizator` | `String` | `@Column(nullable = false)` |
| `tipActiune` | `GdprActionType` | `@Enumerated(EnumType.STRING); @Column(name = "tip_actiune", nullable = false, length = 50)` |
| `entitateVizata` | `String` | `@Column(name = "entitate_vizata", nullable = false)` |
| `idPersoanaVizata` | `String` | `@Column(name = "id_persoana_vizata", length = 1024)` |
| `endpoint` | `String` | `@Column(length = 512)` |
| `tenantId` | `String` | `@Column(name = "tenant_id")` |

### Adresa

[Source](../../src/backend/src/main/java/com/multitenant/model/common/Adresa.java)

Declared mechanisms: `@Embeddable`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `county` | `String` | See source/service |
| `localitate` | `String` | See source/service |
| `street` | `String` | See source/service |
| `streetNumber` | `String` | `@Column(name = "street_number")` |
| `building` | `String` | `@Column(nullable = true)` |
| `staircase` | `String` | `@Column(nullable = true)` |
| `floor` | `Integer` | `@Column(nullable = true)` |
| `apartmentNumber` | `Integer` | `@Column(name = "apartment_number", nullable = true)` |
| `postalCode` | `String` | `@Column(name = "postal_code")` |

### Cetatean

[Source](../../src/backend/src/main/java/com/multitenant/model/core/Cetatean.java)

Table declaration: `name = "cetateni", schema = "public", indexes = { @Index(name = "idx_cetateni_cnp_hash", columnList = "cnp_hash") }`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `nume` | `String` | `@Column(nullable = false, length = 255)` |
| `prenume` | `String` | `@Column(length = 255)` |
| `tipPersoana` | `TipPersoanaCetatean` | `@Enumerated(EnumType.STRING); @Column(name = "tip_persoana", nullable = false, length = 20)` |
| `cnp` | `String` | `@Column(nullable = false, length = 255); @Convert(converter = AesCryptoConverter.class)` |
| `cnpHash` | `String` | `@Column(name = "cnp_hash", length = 64)` |
| `email` | `String` | `@Column(nullable = false, length = 255, unique = true)` |
| `parola` | `String` | `@Column(nullable = false)` |
| `telefon` | `String` | `@Column(nullable = false, length = 50)` |
| `judet` | `String` | `@Column(nullable = false, length = 255)` |
| `localitate` | `String` | `@Column(nullable = false, length = 255)` |
| `strada` | `String` | `@Column(nullable = false, length = 255)` |
| `numar` | `String` | `@Column(nullable = false, length = 50)` |
| `bloc` | `String` | `@Column(length = 50)` |
| `scara` | `String` | `@Column(length = 50)` |
| `etaj` | `String` | `@Column(length = 50)` |
| `apartament` | `String` | `@Column(length = 50)` |
| `areAtestatProducator` | `boolean` | `@Column(name = "are_atestat_producator", nullable = false)` |
| `areCarnetComercializare` | `boolean` | `@Column(name = "are_carnet_comercializare", nullable = false)` |
| `createdAt` | `LocalDateTime` | `@Column(name = "created_at", updatable = false)` |

### PublicUat

[Source](../../src/backend/src/main/java/com/multitenant/model/core/PublicUat.java)

Table declaration: `name = "uats", schema = "public"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `codSiruta` | `String` | `@Column(name = "cod_siruta", nullable = false, length = 50)` |
| `denumire` | `String` | `@Column(nullable = false, length = 255)` |
| `judet` | `String` | `@Column(nullable = false, length = 100)` |
| `tipUat` | `String` | `@Column(name = "tip_uat", nullable = false, length = 50)` |
| `isActive` | `Boolean` | `@Column(name = "is_active", nullable = false)` |
| `tenantId` | `String` | `@Column(name = "tenant_id")` |

### Tenant

[Source](../../src/backend/src/main/java/com/multitenant/model/core/Tenant.java)

Table declaration: `name = "tenants", schema = "public"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `String` | `@Column(name = "id")` |
| `name` | `String` | `@Column(nullable = false)` |
| `schemaName` | `String` | `@Column(name = "schema_name", nullable = false, unique = true)` |
| `createdAt` | `LocalDateTime` | `@Column(name = "created_at", updatable = false)` |
| `isActive` | `boolean` | `@Column(name = "is_active", nullable = false)` |

### TipPersoanaCetatean

[Source](../../src/backend/src/main/java/com/multitenant/model/core/TipPersoanaCetatean.java)

Values: `FIZICA`, `JURIDICA`.

### Uat

[Source](../../src/backend/src/main/java/com/multitenant/model/core/Uat.java)

Table declaration: `name = "uats"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `codSiruta` | `String` | `@Column(name = "cod_siruta", nullable = false, length = 50)` |
| `denumire` | `String` | `@Column(nullable = false, length = 255)` |
| `judet` | `String` | `@Column(nullable = false, length = 100)` |
| `tipUat` | `String` | `@Column(name = "tip_uat", nullable = false, length = 50)` |
| `isActive` | `Boolean` | `@Column(name = "is_active", nullable = false)` |

### User

[Source](../../src/backend/src/main/java/com/multitenant/model/core/User.java)

Table declaration: `name = "users", schema = "public"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `username` | `String` | `@Column(nullable = false, unique = true)` |
| `password` | `String` | `@Column(nullable = false)` |
| `role` | `String` | `@Column(nullable = false)` |
| `tenantId` | `String` | `@Column(name = "tenant_id")` |
| `nume` | `String` | `@Column(length = 255)` |
| `email` | `String` | `@Column(length = 255)` |
| `activ` | `boolean` | `@Column(nullable = false)` |
| `uatId` | `Long` | `@Column(name = "uat_id")` |

### ActIdentitate

[Source](../../src/backend/src/main/java/com/multitenant/model/persoana/ActIdentitate.java)

Table declaration: `name = "identity_documents"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `documentType` | `IdentityCardType` | `@Enumerated(EnumType.STRING); @Column(name = "document_type")` |
| `series` | `String` | See source/service |
| `number` | `String` | `@Column(name = "document_number")` |
| `issuedBy` | `String` | `@Column(name = "issued_by")` |
| `issueDate` | `LocalDate` | `@Column(name = "issue_date")` |
| `expirationDate` | `LocalDate` | `@Column(name = "expiration_date")` |
| `tenantId` | `String` | `@Column(name = "tenant_id")` |
| `persoana` | `PersoanaFizica` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "person_id"); @JsonIgnore` |

Nested enum `IdentityCardType`: `IDENTITY_CARD`, `BIRTH_CERTIFICATE`, `PASSPORT`, `DRIVER_LICENSE`.

### Persoana

[Source](../../src/backend/src/main/java/com/multitenant/model/persoana/Persoana.java)

Table declaration: `name = "persons", indexes = { @Index(name = "idx_persons_cnp_hash", columnList = "cnp_hash"), @Index(name = "idx_persons_cui_hash", columnList = "cui_hash") }`.

Declared mechanisms: `@Audited`, `@DiscriminatorColumn`, `@Inheritance`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `personType` | `String` | `@Column(name = "person_type", insertable = false, updatable = false)` |
| `id` | `Long` | See source/service |
| `adresa` | `Adresa` | `@Embedded` |
| `phoneNumber` | `String` | `@Column(name = "phone_number")` |
| `email` | `String` | See source/service |
| `registerVolume` | `String` | `@Column(name = "register_volume")` |
| `registerPosition` | `String` | `@Column(name = "register_position")` |
| `notes` | `String` | `@Column(name = "notes", columnDefinition = "TEXT")` |
| `tenantId` | `String` | `@Column(name = "tenant_id")` |
| `relations` | `List<RelatieRudenie>` | `@OneToMany(fetch = FetchType.LAZY, mappedBy = "persoana", cascade = CascadeType.ALL, orphanRemoval = true)` |
| `gospodarii` | `List<Gospodarie>` | `@ManyToMany(fetch = FetchType.LAZY); @JoinColumn(name = "persoana_id"); @JoinColumn(name = "gospodarie_id")` |

### PersoanaFizica

[Source](../../src/backend/src/main/java/com/multitenant/model/persoana/PersoanaFizica.java)

Extends `Persoana`.

Declared mechanisms: `@Audited`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `firstName` | `String` | `@Column(name = "first_name")` |
| `lastName` | `String` | `@Column(name = "last_name")` |
| `cnp` | `String` | `@Column(name = "cnp", length = 255); @Convert(converter = AesCryptoConverter.class)` |
| `cnpHash` | `String` | `@Column(name = "cnp_hash", length = 64)` |
| `dateOfBirth` | `LocalDate` | `@Column(name = "date_of_birth")` |
| `esteDecedat` | `Boolean` | `@Column(name = "este_decedat")` |
| `dataDecesului` | `LocalDate` | `@Column(name = "data_decesului")` |
| `numarCertificatDeces` | `String` | `@Column(name = "numar_certificat_deces")` |
| `identityDocuments` | `List<ActIdentitate>` | `@OneToMany(fetch = FetchType.LAZY, mappedBy = "persoana", cascade = CascadeType.ALL, orphanRemoval = true)` |

### PersoanaJuridica

[Source](../../src/backend/src/main/java/com/multitenant/model/persoana/PersoanaJuridica.java)

Extends `Persoana`.

Declared mechanisms: `@Audited`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `companyName` | `String` | `@Column(name = "company_name")` |
| `cui` | `String` | `@Column(name = "cui", length = 255); @Convert(converter = AesCryptoConverter.class)` |
| `cuiHash` | `String` | `@Column(name = "cui_hash", length = 64)` |
| `registrationNumber` | `String` | `@Column(name = "registration_number")` |
| `legalRepresentative` | `String` | `@Column(name = "legal_representative")` |

### RelatieRudenie

[Source](../../src/backend/src/main/java/com/multitenant/model/persoana/RelatieRudenie.java)

Table declaration: `name = "person_relations"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `persoana` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "person_id"); @JsonIgnore` |
| `relatedPerson` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "related_person_id")` |
| `relationType` | `KinshipType` | `@Enumerated(EnumType.STRING); @Column(name = "relation_type")` |

Nested enum `KinshipType`: `PARENT`, `CHILD`, `SPOUSE`, `SIBLING`, `GRANDPARENT`, `GRANDCHILD`, `OTHER`.

### AtestatProducator

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/AtestatProducator.java)

Table declaration: `name = "atestate_producator"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `numarAtestat` | `String` | `@Column(name = "numar_atestat", unique = true, nullable = false, length = 50)` |
| `seria` | `String` | `@Column(nullable = false, length = 10)` |
| `persoana` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "persoana_id", nullable = false)` |
| `dataEliberare` | `LocalDate` | `@Column(name = "data_eliberare", nullable = false)` |
| `valabilitateLuni` | `Integer` | `@Column(name = "valabilitate_luni", nullable = false)` |
| `observatii` | `String` | `@Column(columnDefinition = "TEXT")` |
| `deleted` | `boolean` | `@Column(nullable = false)` |
| `createdAt` | `LocalDateTime` | `@Column(name = "created_at", updatable = false)` |

### CarnetComercializare

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/CarnetComercializare.java)

Table declaration: `name = "carnete_comercializare"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `numarCarnet` | `String` | `@Column(name = "numar_carnet", unique = true, nullable = false, length = 50)` |
| `seria` | `String` | `@Column(nullable = false, length = 10)` |
| `atestat` | `AtestatProducator` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "atestat_id", nullable = false)` |
| `persoana` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "persoana_id", nullable = false)` |
| `dataEliberare` | `LocalDate` | `@Column(name = "data_eliberare", nullable = false)` |
| `deleted` | `boolean` | `@Column(nullable = false)` |
| `createdAt` | `LocalDateTime` | `@Column(name = "created_at", updatable = false)` |

### CarteFunciara

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/CarteFunciara.java)

Table declaration: `name = "carti_funciare"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `teren` | `Teren` | `@OneToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "teren_id", nullable = false, unique = true)` |
| `numarCf` | `String` | `@Column(name = "numar_cf", length = 100)` |
| `numarTopografic` | `String` | `@Column(name = "numar_topografic", length = 100)` |
| `suprafataTotalaIntabulata` | `Double` | `@Column(name = "suprafata_totala_intabulata")` |
| `createdAt` | `LocalDateTime` | `@Column(name = "created_at", nullable = false, updatable = false)` |
| `updatedAt` | `LocalDateTime` | `@Column(name = "updated_at", nullable = false)` |

### CatalogIngrasaminte

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/CatalogIngrasaminte.java)

Table declaration: `name = "catalog_ingrasaminte"`.

Declared mechanisms: `@Audited`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `denumire` | `String` | `@Column(nullable = false, length = 255)` |
| `tip` | `String` | `@Column(nullable = false, length = 50)` |
| `procentAzot` | `Double` | `@Column(name = "procent_azot", nullable = false)` |
| `procentFosfor` | `Double` | `@Column(name = "procent_fosfor", nullable = false)` |
| `procentPotasiu` | `Double` | `@Column(name = "procent_potasiu", nullable = false)` |

### CatalogPpp

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/CatalogPpp.java)

Table declaration: `name = "catalog_ppp"`.

Declared mechanisms: `@Audited`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `denumireComerciala` | `String` | `@Column(name = "denumire_comerciala", nullable = false, length = 255)` |
| `tip` | `String` | `@Column(nullable = false, length = 100)` |
| `daunatorVizat` | `String` | `@Column(name = "daunator_vizat", length = 255)` |
| `dozaOmologata` | `Double` | `@Column(name = "doza_omologata", nullable = false)` |
| `timpPauza` | `Integer` | `@Column(name = "timp_pauza", nullable = false)` |

### CategorieFolosinta

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/CategorieFolosinta.java)

Table declaration: `name = "categorii_folosinta"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `denumire` | `String` | `@Column(nullable = false, length = 255)` |
| `descriere` | `String` | `@Column(columnDefinition = "TEXT")` |
| `teren` | `Teren` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "teren_id", nullable = false)` |

### Cerere

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Cerere.java)

Table declaration: `name = "cereri", indexes = { @Index(name = "idx_cereri_cnp_cui_hash", columnList = "cnp_cui_hash") }`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `nume` | `String` | `@NotBlank(message = "Numele este obligatoriu."); @Column(nullable = false, length = 255)` |
| `domiciliu` | `String` | `@NotBlank(message = "Domiciliul este obligatoriu."); @Column(nullable = false, columnDefinition = "TEXT")` |
| `telefon` | `String` | `@Column(length = 20)` |
| `email` | `String` | `@Column(length = 255)` |
| `numarCarteFunciara` | `String` | `@Column(name = "numar_carte_funciara", length = 50)` |
| `numarCadastral` | `String` | `@Column(name = "numar_cadastral", length = 50)` |
| `codCerere` | `String` | `@Column(name = "cod_cerere", unique = true, nullable = false, length = 50)` |
| `cnpCui` | `String` | `@Column(name = "cnp_cui", length = 255); @Convert(converter = AesCryptoConverter.class)` |
| `cnpCuiHash` | `String` | `@Column(name = "cnp_cui_hash", length = 64)` |
| `status` | `StatusCerere` | `@Enumerated(EnumType.STRING); @Column(nullable = false, length = 20)` |
| `tipCerere` | `TipCerere` | `@Enumerated(EnumType.STRING); @Column(name = "tip_cerere", nullable = false, length = 50)` |
| `userId` | `Long` | `@Column(name = "user_id")` |
| `uatId` | `Long` | `@Column(name = "uat_id", nullable = false)` |
| `createdAt` | `LocalDateTime` | `@Column(name = "created_at", updatable = false)` |

### CicluProductie

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/CicluProductie.java)

Table declaration: `name = "cicluri_productie"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | `@Column(nullable = false)` |
| `id` | `Long` | See source/service |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |
| `cultura` | `String` | `@Column(nullable = false, length = 100)` |
| `dataInfiintare` | `LocalDate` | `@Column(name = "data_infiintare", nullable = false)` |
| `dataDefisare` | `LocalDate` | `@Column(name = "data_defisare")` |
| `status` | `CicluStatus` | `@Enumerated(EnumType.STRING); @Column(nullable = false, length = 20)` |
| `programSprijin` | `boolean` | `@Column(name = "program_sprijin", nullable = false)` |

### CicluStatus

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/CicluStatus.java)

Values: `ACTIV`, `FINALIZAT`.

### Cladire

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Cladire.java)

Table declaration: `name = "cladiri"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `destinatie` | `String` | `@Column(nullable = false, length = 255)` |
| `suprafataConstruita` | `Double` | `@Column(name = "suprafata_construita", nullable = false)` |
| `anTerminare` | `Integer` | `@Column(name = "an_terminare")` |
| `materiale` | `String` | `@Column(length = 255)` |
| `adresaSauParcela` | `String` | `@Column(name = "adresa_sau_parcela", length = 255)` |
| `gospodarie` | `Gospodarie` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "gospodarie_id", nullable = false)` |
| `teren` | `Teren` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "teren_id")` |

### ContractUtilizare

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/ContractUtilizare.java)

Table declaration: `name = "contracte_utilizare"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "parcela_id", nullable = false)` |
| `locatorProprietar` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "locator_proprietar_id")` |
| `locatorUtilizator` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "locator_utilizator_id")` |
| `tipContract` | `TipContractUtilizare` | `@Enumerated(EnumType.STRING); @Column(name = "tip_contract", nullable = false, length = 50)` |
| `numarContract` | `String` | `@Column(name = "numar_contract", nullable = false, length = 100)` |
| `dataSemnare` | `LocalDate` | `@Column(name = "data_semnare")` |
| `dataInceput` | `LocalDate` | `@Column(name = "data_inceput")` |
| `dataSfarsit` | `LocalDate` | `@Column(name = "data_sfarsit")` |
| `pretArendaRonAn` | `Double` | `@Column(name = "pret_arenda_ron_an")` |
| `pretArendaGrauKgHa` | `Double` | `@Column(name = "pret_arenda_grau_kg_ha")` |
| `indexarePret` | `boolean` | `@Column(name = "indexare_pret")` |
| `statusContract` | `StatusContractUtilizare` | `@Enumerated(EnumType.STRING); @Column(name = "status_contract", length = 50)` |
| `motivIncetare` | `String` | `@Column(name = "motiv_incetare", columnDefinition = "TEXT")` |
| `dataOperare` | `LocalDate` | `@Column(name = "data_operare")` |
| `utilizatorOperareId` | `Long` | `@Column(name = "utilizator_operare_id")` |
| `esteActiv` | `boolean` | `@Column(name = "este_activ")` |
| `semnatElectronic` | `boolean` | `@Column(name = "semnat_electronic")` |
| `dataSemnaturiiElectronice` | `java.time.LocalDateTime` | `@Column(name = "data_semnaturii_electronice")` |
| `caleDocumentSemnat` | `String` | `@Column(name = "cale_document_semnat", length = 500)` |
| `hashDocumentSemnat` | `String` | `@Column(name = "hash_document_semnat", length = 128)` |
| `semnatDeUtilizatorId` | `Long` | `@Column(name = "semnat_de_utilizator_id")` |
| `signNowDocumentId` | `String` | `@Column(name = "signnow_document_id", length = 100)` |
| `signNowStatus` | `String` | `@Column(name = "signnow_status", length = 30)` |
| `signNowTrimisLa` | `java.time.LocalDateTime` | `@Column(name = "signnow_trimis_la")` |
| `signNowEmailSemnatar` | `String` | `@Column(name = "signnow_email_semnatar", length = 255)` |

### CulturaParcela

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/CulturaParcela.java)

Table declaration: `name = "culturi_parcele"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `anAgricol` | `Integer` | `@Column(name = "an_agricol", nullable = false)` |
| `specieCultura` | `String` | `@Column(name = "specie_cultura", nullable = false, length = 100)` |
| `suprafataCultivataHa` | `Double` | `@Column(name = "suprafata_cultivata_ha", nullable = false)` |
| `dataInsamantare` | `LocalDate` | `@Column(name = "data_insamantare")` |
| `dataRecoltare` | `LocalDate` | `@Column(name = "data_recoltare")` |
| `productieHectarKg` | `Double` | `@Column(name = "productie_hectar_kg")` |
| `productieTotalaTone` | `Double` | `@Column(name = "productie_totala_tone")` |
| `sistemIrigare` | `String` | `@Column(name = "sistem_irigare", length = 100)` |
| `tipSol` | `String` | `@Column(name = "tip_sol", length = 100)` |
| `culturaPrecedenta` | `String` | `@Column(name = "cultura_precedenta", length = 100)` |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |

### Document

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Document.java)

Table declaration: `name = "documente"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `gospodarie` | `Gospodarie` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "gospodarie_id", nullable = false)` |
| `tipDocumentId` | `Integer` | `@Column(name = "tip_document_id", nullable = false)` |
| `numeFisier` | `String` | `@Column(name = "nume_fisier", nullable = false, length = 255)` |
| `caleStocare` | `String` | `@Column(name = "cale_stocare", nullable = false, length = 500)` |
| `mimeType` | `String` | `@Column(name = "mime_type", nullable = false, length = 100)` |
| `dimensiuneKb` | `Integer` | `@Column(name = "dimensiune_kb")` |
| `dataEmitere` | `LocalDate` | `@Column(name = "data_emitere")` |
| `dataExpirare` | `LocalDate` | `@Column(name = "data_expirare")` |
| `uploadedById` | `Long` | `@Column(name = "uploaded_by_id")` |
| `dataIncarcare` | `LocalDateTime` | `@Column(name = "data_incarcare")` |
| `observatii` | `String` | `@Column(name = "observatii", columnDefinition = "TEXT")` |
| `esteActiv` | `boolean` | `@Column(name = "este_activ")` |

### FactoriMediu

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/FactoriMediu.java)

Table declaration: `name = "factori_mediu"`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |
| `temperatura` | `Double` | `@Column(name = "temperatura")` |
| `umiditateRelativa` | `Double` | `@Column(name = "umiditate_relativa")` |
| `dataInregistrare` | `LocalDateTime` | `@Column(name = "data_inregistrare", nullable = false)` |

### Fertilizare

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Fertilizare.java)

Table declaration: `name = "fertilizari"`.

Declared mechanisms: `@Audited`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `dataAplicarii` | `LocalDate` | `@Column(name = "data_aplicarii", nullable = false)` |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "parcela_id", nullable = false)` |
| `catalogIngrasaminte` | `CatalogIngrasaminte` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "catalog_ingrasaminte_id", nullable = false)` |
| `cantitateBruta` | `Double` | `@Column(name = "cantitate_bruta", nullable = false)` |
| `unitateMasura` | `String` | `@Column(name = "unitate_masura", nullable = false, length = 20)` |
| `aportAzot` | `Double` | `@Column(name = "aport_azot", nullable = false)` |
| `aportFosfor` | `Double` | `@Column(name = "aport_fosfor", nullable = false)` |
| `aportPotasiu` | `Double` | `@Column(name = "aport_potasiu", nullable = false)` |
| `cicluProductie` | `CicluProductie` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "ciclu_productie_id")` |

### Gospodarie

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Gospodarie.java)

Table declaration: `name = "gospodarii"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `codGospodarie` | `String` | `@Column(name = "cod_gospodarie", nullable = false, length = 100)` |
| `adresa` | `Adresa` | `@Embedded` |
| `tipGospodarie` | `TipGospodarie` | `@Enumerated(EnumType.STRING); @Column(name = "tip_gospodarie", nullable = false, length = 50)` |
| `activa` | `boolean` | `@Column(nullable = false)` |
| `uat` | `Uat` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "uat_id")` |
| `capGospodarie` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "cap_gospodarie_id")` |

### IstoricMembruGospodarie

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/IstoricMembruGospodarie.java)

Table declaration: `name = "istoric_membri_gospodarie"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `gospodarie` | `Gospodarie` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "gospodarie_id", nullable = false)` |
| `persoana` | `Persoana` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "persoana_id", nullable = false)` |
| `tipEveniment` | `TipEvenimentMembru` | `@Enumerated(EnumType.STRING); @Column(name = "tip_eveniment", nullable = false, length = 50)` |
| `document` | `Document` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "document_id")` |
| `dataEveniment` | `LocalDate` | `@Column(name = "data_eveniment", nullable = false)` |
| `observatii` | `String` | `@Column(name = "observatii", columnDefinition = "TEXT")` |
| `createdAt` | `LocalDateTime` | `@Column(name = "created_at", insertable = false, updatable = false)` |

### Machinery

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Machinery.java)

Table declaration: `name = "utilaje"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `tipUtilaj` | `String` | `@Column(name = "tip_utilaj", nullable = false, length = 50)` |
| `marca` | `String` | `@Column(nullable = false, length = 100)` |
| `model` | `String` | `@Column(nullable = false, length = 100)` |
| `anFabricatie` | `Integer` | `@Column(name = "an_fabricatie")` |
| `numarInmatriculare` | `String` | `@Column(name = "numar_inmatriculare", length = 50)` |
| `gospodarie` | `Gospodarie` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "gospodarie_id", nullable = false)` |

### NotificareSuccesiune

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/NotificareSuccesiune.java)

Table declaration: `name = "notificari_succesiuni"`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `defunct` | `PersoanaFizica` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "defunct_id", nullable = false)` |
| `defunctCnpHash` | `String` | `@Column(name = "defunct_cnp_hash", nullable = false, length = 64)` |
| `numeNotarSpnBin` | `String` | `@Column(name = "nume_notar_spn_bin")` |
| `numarAdresaOficiala` | `String` | `@Column(name = "numar_adresa_oficiala", length = 100)` |
| `dataTrimitere` | `LocalDate` | `@Column(name = "data_trimitere")` |
| `stadiuNotificare` | `String` | `@Column(name = "stadiu_notificare", nullable = false, length = 50)` |
| `observatii` | `String` | `@Column(columnDefinition = "TEXT")` |
| `utilizatorOperare` | `String` | `@Column(name = "utilizator_operare")` |
| `dataInregistrare` | `LocalDateTime` | `@Column(name = "data_inregistrare")` |

### Padure

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Padure.java)

Table declaration: `name = "paduri"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `tipVegetatie` | `String` | `@Column(name = "tip_vegetatie", nullable = false, length = 100)` |
| `speciePredominanta` | `String` | `@Column(name = "specie_predominanta", length = 100)` |
| `suprafataHa` | `Double` | `@Column(name = "suprafata_ha")` |
| `anPlantare` | `Integer` | `@Column(name = "an_plantare")` |
| `stareVegetatie` | `String` | `@Column(name = "stare_vegetatie", length = 50)` |
| `observatii` | `String` | `@Column(name = "observatii", length = 500)` |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |

### Parcela

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Parcela.java)

Table declaration: `name = "parcele"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `denumire` | `String` | `@NotBlank(message = "Denumirea parcelei este obligatorie."); @Column(nullable = false, length = 255)` |
| `suprafata` | `Double` | `@NotNull(message = "Suprafata este obligatorie."); @Positive(message = "Suprafata trebuie sa fie pozitiva."); @Column(nullable = false)` |
| `categorieFolosinta` | `String` | `@Column(name = "categorie_folosinta", length = 100)` |
| `numarCadastral` | `String` | `@Column(name = "numar_cadastral", length = 100)` |
| `tipZona` | `TipZona` | `@Enumerated(EnumType.STRING); @Column(name = "tip_zona", length = 20)` |
| `tipMediu` | `TipMediu` | `@Enumerated(EnumType.STRING); @Column(name = "tip_mediu", nullable = false, length = 30)` |
| `suprafataUtilaMp` | `Double` | `@Column(name = "suprafata_utila_mp")` |
| `titularDreptFolosinta` | `String` | `@Column(name = "titular_drept_folosinta", length = 255)` |
| `polygon` | `JsonNode` | `@Column(columnDefinition = "jsonb")` |
| `stereo70Coordinates` | `String` | `@Transient` |
| `teren` | `Teren` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "teren_id", nullable = false)` |

### PasuneFaneata

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/PasuneFaneata.java)

Table declaration: `name = "pasuni_fanete"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `tipFolosinta` | `TipFolosintaPasune` | `@Enumerated(EnumType.STRING); @Column(name = "tip_folosinta", nullable = false, length = 20)` |
| `suprafataHa` | `Double` | `@Column(name = "suprafata_ha", nullable = false)` |
| `speciiDominante` | `String` | `@Column(name = "specii_dominante", length = 255)` |
| `numarAnimalePasunat` | `Integer` | `@Column(name = "numar_animale_pasunat")` |
| `numarCosiriAnuale` | `Integer` | `@Column(name = "numar_cosiri_anuale")` |
| `productieEstimataKgHa` | `Double` | `@Column(name = "productie_estimata_kg_ha")` |
| `stareVegetatie` | `String` | `@Column(name = "stare_vegetatie", length = 50)` |
| `sistemIntretinere` | `String` | `@Column(name = "sistem_intretinere", length = 100)` |
| `sistemIrigare` | `String` | `@Column(name = "sistem_irigare", length = 100)` |
| `observatii` | `String` | `@Column(name = "observatii", length = 500)` |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |

### Pom

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Pom.java)

Table declaration: `name = "pomi"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `tipInregistrare` | `TipInregistrarePom` | `@Enumerated(EnumType.STRING); @Column(name = "tip_inregistrare", nullable = false, length = 20)` |
| `specie` | `String` | `@Column(name = "specie", nullable = false, length = 100)` |
| `soi` | `String` | `@Column(name = "soi", length = 100)` |
| `anPlantare` | `Integer` | `@Column(name = "an_plantare")` |
| `numarPomi` | `Integer` | `@Column(name = "numar_pomi")` |
| `suprafataHa` | `Double` | `@Column(name = "suprafata_ha")` |
| `densitatePomiHa` | `Integer` | `@Column(name = "densitate_pomi_ha")` |
| `starePomi` | `String` | `@Column(name = "stare_pomi", length = 50)` |
| `sistemIntretinere` | `String` | `@Column(name = "sistem_intretinere", length = 100)` |
| `sistemIrigare` | `String` | `@Column(name = "sistem_irigare", length = 100)` |
| `productieEstimataKg` | `Double` | `@Column(name = "productie_estimata_kg")` |
| `observatii` | `String` | `@Column(name = "observatii", length = 500)` |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |

### Recoltare

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Recoltare.java)

Table declaration: `name = "recoltari"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | `@Column(nullable = false)` |
| `id` | `Long` | See source/service |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |
| `cicluProductie` | `CicluProductie` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "ciclu_productie_id")` |
| `cultura` | `String` | `@Column(nullable = false, length = 100)` |
| `dataRecoltare` | `LocalDate` | `@Column(name = "data_recoltare", nullable = false)` |
| `cantitateKg` | `Double` | `@Column(name = "cantitate_kg", nullable = false)` |

### StatusCerere

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/StatusCerere.java)

Values: `PENDING`, `ACCEPTED`, `DECLINED`.

### StatusContractUtilizare

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/StatusContractUtilizare.java)

Values: `ACTIV`, `EXPIRAT`, `REZILIAT`, `SUSPENDAT`.

### SursaApa

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/SursaApa.java)

Table declaration: `name = "surse_apa"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `tipSursa` | `String` | `@Column(name = "tip_sursa", length = 100)` |
| `debitMcOra` | `Double` | `@Column(name = "debit_mc_ora")` |
| `stareFunctionare` | `boolean` | `@Column(name = "stare_functionare", nullable = false)` |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |

### Teren

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/Teren.java)

Table declaration: `name = "terenuri"`.

Declared mechanisms: `@Audited`, `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `denumire` | `String` | `@NotBlank(message = "Denumirea terenului este obligatorie."); @Column(nullable = false, length = 255)` |
| `tipTeren` | `String` | `@Column(name = "tip_teren", length = 100)` |
| `stereo70Coordinates` | `String` | `@Column(name = "stereo70_coordinates", columnDefinition = "TEXT")` |
| `polygon` | `com.fasterxml.jackson.databind.JsonNode` | `@Column(columnDefinition = "jsonb")` |
| `gospodarie` | `Gospodarie` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "gospodarie_id", nullable = false)` |

### TipCerere

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipCerere.java)

Values: `ELIBERARE_ATESTAT_PRODUCATOR`, `ELIBERARE_CARNET_COMERCIALIZARE`, `ADEVERINTA_ROL`, `SESIZARE_AMBROZIA`, `ADEVERINTA_AVIZ_CONSULTATIV`, `ADEVERINTA_TEREN_PF`, `ADEVERINTA_TEREN_PJ`, `COPIE_REGISTRU_1959_1963`, `EXTRAS_REGISTRU_PF`, `EXTRAS_REGISTRU_PJ`, `ADEVERINTA_DETINERE_TEREN`.

### TipContractUtilizare

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipContractUtilizare.java)

Values: `ARENDA`, `COMODAT`, `CONCESIUNE`, `INCHIRIERE`, `ALTELE`.

### TipEvenimentMembru

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipEvenimentMembru.java)

Values: `INTRARE_NASTERE`, `INTRARE_CASATORIE`, `INTRARE_MUTARE`, `IESIRE_DECES`, `IESIRE_DIVORT`, `IESIRE_MUTARE`, `ALTELE`.

### TipFolosintaPasune

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipFolosintaPasune.java)

Values: `PASUNAT`, `COSIT`, `MIXT`.

### TipGospodarie

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipGospodarie.java)

Values: `INDIVIDUALA`, `COLECTIVA`, `ASOCIATIE`.

### TipInregistrarePom

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipInregistrarePom.java)

Values: `IZOLAT`, `PLANTATIE`.

### TipInregistrareVita

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipInregistrareVita.java)

Values: `IZOLAT`, `PLANTATIE`.

### TipMediu

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipMediu.java)

Values: `CAMP_DESCHIS`, `SOLAR`, `SERA_INCALZITA`.

### TipSursaApa

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipSursaApa.java)

Values: `PUT_FORAT`, `FANTANA`, `RETEA_IRIGATII`, `RAU_CANAL`, `ACUMULARE`.

### TipZona

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TipZona.java)

Values: `INTRAVILAN`, `EXTRAVILAN`.

### TratamentFitosanitar

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/TratamentFitosanitar.java)

Table declaration: `name = "tratamente_fitosanitare"`.

Declared mechanisms: `@Audited`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `dataEfectuarii` | `LocalDateTime` | `@Column(name = "data_efectuarii", nullable = false)` |
| `fenofaza` | `String` | `@Column(nullable = false, length = 100)` |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "parcela_id", nullable = false)` |
| `agentDaunator` | `String` | `@Column(name = "agent_daunator", nullable = false, length = 255)` |
| `catalogPpp` | `CatalogPpp` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "catalog_ppp_id", nullable = false)` |
| `dozaUtilizata` | `Double` | `@Column(name = "doza_utilizata", nullable = false)` |
| `suprafataTratata` | `Double` | `@Column(name = "suprafata_tratata", nullable = false)` |
| `cantitateTotala` | `Double` | `@Column(name = "cantitate_totala", nullable = false)` |
| `responsabil` | `String` | `@Column(nullable = false, length = 255)` |
| `semnaturaElectronica` | `String` | `@Column(name = "semnatura_electronica", columnDefinition = "TEXT")` |
| `dataIncepereRecoltare` | `LocalDate` | `@Column(name = "data_incepere_recoltare")` |
| `documentDareConsum` | `String` | `@Column(name = "document_dare_consum", length = 100)` |
| `dozaDepasita` | `Boolean` | `@Column(name = "doza_depasita", nullable = false)` |
| `justificareSupradozaj` | `String` | `@Column(name = "justificare_supradozaj", columnDefinition = "TEXT")` |
| `cicluProductie` | `CicluProductie` | `@ManyToOne(fetch = FetchType.LAZY); @JoinColumn(name = "ciclu_productie_id")` |
| `unitateMasuraDoza` | `String` | `@Column(name = "unitate_masura_doza", length = 50)` |
| `dataLansarii` | `LocalDate` | `@Column(name = "data_lansarii")` |
| `numarCutiiIndivizi` | `Integer` | `@Column(name = "numar_cutii_indivizi")` |

### VitaDeVie

[Source](../../src/backend/src/main/java/com/multitenant/model/registru/VitaDeVie.java)

Table declaration: `name = "vita_de_vie"`.

Declared mechanisms: `@SQLDelete`, `@SQLRestriction`.

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `deleted` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `tipInregistrare` | `TipInregistrareVita` | `@Enumerated(EnumType.STRING); @Column(name = "tip_inregistrare", nullable = false, length = 20)` |
| `specie` | `String` | `@Column(name = "specie", nullable = false, length = 100)` |
| `soi` | `String` | `@Column(name = "soi", length = 100)` |
| `anPlantare` | `Integer` | `@Column(name = "an_plantare")` |
| `numarVite` | `Integer` | `@Column(name = "numar_vite")` |
| `suprafataHa` | `Double` | `@Column(name = "suprafata_ha")` |
| `densitateViteHa` | `Integer` | `@Column(name = "densitate_vite_ha")` |
| `stareVita` | `String` | `@Column(name = "stare_vita", length = 50)` |
| `sistemIntretinere` | `String` | `@Column(name = "sistem_intretinere", length = 100)` |
| `sistemIrigare` | `String` | `@Column(name = "sistem_irigare", length = 100)` |
| `productieEstimataKg` | `Double` | `@Column(name = "productie_estimata_kg")` |
| `observatii` | `String` | `@Column(name = "observatii", length = 500)` |
| `parcela` | `Parcela` | `@ManyToOne(fetch = FetchType.LAZY, optional = false); @JoinColumn(name = "parcela_id", nullable = false)` |

## Dto

### AnimalIndividualDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/AnimalIndividualDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `gospodarie` | `GospodarieDTO` | See source/service |
| `gospodarieId` | `Long` | See source/service |
| `proprietar` | `PersoanaDTO` | See source/service |
| `proprietarId` | `Long` | See source/service |
| `numarCrotal` | `String` | See source/service |
| `specie` | `SpecieAnimal` | See source/service |
| `rasa` | `String` | See source/service |
| `sex` | `SexAnimal` | See source/service |
| `dataNastere` | `LocalDate` | See source/service |
| `greutateKg` | `Double` | See source/service |
| `stareActiva` | `boolean` | See source/service |
| `tenantId` | `String` | See source/service |

### AtestatStatusDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/AtestatStatusDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `areAtestat` | `boolean` | See source/service |
| `numarAtestat` | `String` | See source/service |
| `atestatValabilPanaLa` | `LocalDate` | See source/service |
| `areCarnet` | `boolean` | See source/service |
| `numarCarnet` | `String` | See source/service |
| `carnetDataEliberare` | `LocalDate` | See source/service |
| `stareCerereAtestat` | `String` | See source/service |
| `stareCerereCarnet` | `String` | See source/service |

### CarteFunciaraDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/CarteFunciaraDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `numarCf` | `String` | See source/service |
| `numarTopografic` | `String` | See source/service |

### CatalogIngrasaminteDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/CatalogIngrasaminteDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `denumire` | `String` | See source/service |
| `tip` | `String` | See source/service |
| `procentAzot` | `Double` | See source/service |
| `procentFosfor` | `Double` | See source/service |
| `procentPotasiu` | `Double` | See source/service |

### CatalogPppDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/CatalogPppDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `denumireComerciala` | `String` | See source/service |
| `tip` | `String` | See source/service |
| `daunatorVizat` | `String` | See source/service |
| `dozaOmologata` | `Double` | See source/service |
| `timpPauza` | `Integer` | See source/service |

### CentralizatorRecoltareDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/CentralizatorRecoltareDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `cultura` | `String` | See source/service |
| `tipMediu` | `String` | See source/service |
| `cantitateTotalaKg` | `Double` | See source/service |
| `suprafataTotalaMp` | `Double` | See source/service |
| `randamentKgMp` | `Double` | See source/service |

### CerereDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/CerereDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `nume` | `String` | See source/service |
| `domiciliu` | `String` | See source/service |
| `telefon` | `String` | See source/service |
| `email` | `String` | See source/service |
| `numarCarteFunciara` | `String` | See source/service |
| `numarCadastral` | `String` | See source/service |
| `cnpCui` | `String` | See source/service |
| `codCerere` | `String` | See source/service |
| `status` | `StatusCerere` | See source/service |
| `tipCerere` | `String` | See source/service |
| `userId` | `Long` | See source/service |
| `uatId` | `Long` | See source/service |
| `createdAt` | `LocalDateTime` | See source/service |

### CicluProductieDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/CicluProductieDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `parcelaId` | `Long` | See source/service |
| `parcelaDenumire` | `String` | See source/service |
| `cultura` | `String` | See source/service |
| `dataInfiintare` | `LocalDate` | See source/service |
| `dataDefisare` | `LocalDate` | See source/service |
| `status` | `CicluStatus` | See source/service |
| `programSprijin` | `boolean` | See source/service |
| `warning` | `String` | See source/service |

### CladireDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/CladireDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `destinatie` | `String` | See source/service |
| `suprafataConstruita` | `Double` | See source/service |
| `anTerminare` | `Integer` | See source/service |
| `materiale` | `String` | See source/service |
| `adresaSauParcela` | `String` | See source/service |
| `gospodarieId` | `Long` | See source/service |
| `terenId` | `Long` | See source/service |

### ContractUtilizareDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/ContractUtilizareDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `parcelaId` | `Long` | See source/service |
| `locatorProprietarId` | `Long` | See source/service |
| `locatorUtilizatorId` | `Long` | See source/service |
| `tipContract` | `TipContractUtilizare` | See source/service |
| `numarContract` | `String` | See source/service |
| `dataSemnare` | `LocalDate` | See source/service |
| `dataInceput` | `LocalDate` | See source/service |
| `dataSfarsit` | `LocalDate` | See source/service |
| `pretArendaRonAn` | `Double` | See source/service |
| `pretArendaGrauKgHa` | `Double` | See source/service |
| `indexarePret` | `boolean` | See source/service |
| `statusContract` | `StatusContractUtilizare` | See source/service |
| `motivIncetare` | `String` | See source/service |
| `dataOperare` | `LocalDate` | See source/service |
| `esteActiv` | `boolean` | See source/service |

### ContractUtilizareResponseDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/ContractUtilizareResponseDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `parcela` | `ParcelaRef` | See source/service |
| `locatorProprietar` | `PersoanaRef` | See source/service |
| `locatorUtilizator` | `PersoanaRef` | See source/service |
| `utilizatorOperare` | `PersoanaRef` | See source/service |
| `tipContract` | `TipContractUtilizare` | See source/service |
| `numarContract` | `String` | See source/service |
| `dataSemnare` | `LocalDate` | See source/service |
| `dataInceput` | `LocalDate` | See source/service |
| `dataSfarsit` | `LocalDate` | See source/service |
| `pretArendaRonAn` | `Double` | See source/service |
| `pretArendaGrauKgHa` | `Double` | See source/service |
| `indexarePret` | `boolean` | See source/service |
| `statusContract` | `StatusContractUtilizare` | See source/service |
| `motivIncetare` | `String` | See source/service |
| `dataOperare` | `LocalDate` | See source/service |
| `esteActiv` | `boolean` | See source/service |
| `id` | `Long` | See source/service |
| `denumire` | `String` | See source/service |
| `id` | `Long` | See source/service |

### CulturaParcelaDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/CulturaParcelaDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `anAgricol` | `Integer` | See source/service |
| `specieCultura` | `String` | See source/service |
| `suprafataCultivataHa` | `Double` | See source/service |
| `dataInsamantare` | `LocalDate` | See source/service |
| `dataRecoltare` | `LocalDate` | See source/service |
| `productieHectarKg` | `Double` | See source/service |
| `productieTotalaTone` | `Double` | See source/service |
| `sistemIrigare` | `String` | See source/service |
| `tipSol` | `String` | See source/service |
| `culturaPrecedenta` | `String` | See source/service |
| `parcelaId` | `Long` | See source/service |

### DocumentDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/DocumentDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `gospodarieId` | `Long` | See source/service |
| `tipDocumentId` | `Integer` | See source/service |
| `numeFisier` | `String` | See source/service |
| `dataEmitere` | `LocalDate` | See source/service |
| `dataExpirare` | `LocalDate` | See source/service |
| `observatii` | `String` | See source/service |
| `esteActiv` | `boolean` | See source/service |

### EfectivGrupDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/EfectivGrupDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `gospodarie` | `GospodarieDTO` | See source/service |
| `gospodarieId` | `Long` | See source/service |
| `proprietar` | `PersoanaDTO` | See source/service |
| `proprietarId` | `Long` | See source/service |
| `specie` | `SpecieAnimal` | See source/service |
| `numarCapeteFamilii` | `Integer` | See source/service |
| `dataInregistrare` | `LocalDate` | See source/service |
| `detalii` | `String` | See source/service |
| `tenantId` | `String` | See source/service |

### EvenimentAnimalDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/EvenimentAnimalDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `animal` | `AnimalIndividualDTO` | See source/service |
| `tipEveniment` | `TipEvenimentAnimal` | See source/service |
| `dataEveniment` | `LocalDate` | See source/service |
| `detalii` | `String` | See source/service |
| `destinatarTenantId` | `String` | See source/service |
| `tenantId` | `String` | See source/service |

### FactoriMediuDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/FactoriMediuDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `parcelaId` | `Long` | See source/service |
| `parcelaDenumire` | `String` | See source/service |
| `temperatura` | `Double` | See source/service |
| `umiditateRelativa` | `Double` | See source/service |
| `dataInregistrare` | `LocalDateTime` | See source/service |

### FertilizareDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/FertilizareDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `dataAplicarii` | `LocalDate` | See source/service |
| `parcelaId` | `Long` | See source/service |
| `parcelaDenumire` | `String` | See source/service |
| `catalogIngrasaminteId` | `Long` | See source/service |
| `catalogIngrasaminteDenumire` | `String` | See source/service |
| `catalogIngrasaminteTip` | `String` | See source/service |
| `procentAzot` | `Double` | See source/service |
| `procentFosfor` | `Double` | See source/service |
| `procentPotasiu` | `Double` | See source/service |
| `cantitateBruta` | `Double` | See source/service |
| `unitateMasura` | `String` | See source/service |
| `aportAzot` | `Double` | See source/service |
| `aportFosfor` | `Double` | See source/service |
| `aportPotasiu` | `Double` | See source/service |
| `cicluProductieId` | `Long` | See source/service |
| `cicluProductieCultura` | `String` | See source/service |

### FieldDiff

[Source](../../src/backend/src/main/java/com/multitenant/dto/FieldDiff.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `oldValue` | `Object` | See source/service |
| `newValue` | `Object` | See source/service |

### FilaParceleiDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/FilaParceleiDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `data` | `LocalDate` | See source/service |
| `tipInterventie` | `String` | See source/service |
| `denumireProdus` | `String` | See source/service |
| `tipProdus` | `String` | See source/service |
| `dozaCantitate` | `Double` | See source/service |
| `unitateMasura` | `String` | See source/service |
| `suprafataTratata` | `Double` | See source/service |
| `detaliiTinta` | `String` | See source/service |
| `responsabil` | `String` | See source/service |
| `statusAlerta` | `String` | See source/service |

### GospodarieDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/GospodarieDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `codGospodarie` | `String` | See source/service |
| `adresa` | `Adresa` | See source/service |
| `tipGospodarie` | `TipGospodarie` | See source/service |
| `activa` | `boolean` | See source/service |
| `uat` | `UatRef` | See source/service |
| `capGospodarie` | `PersoanaDTO` | See source/service |
| `id` | `Long` | See source/service |
| `codSiruta` | `String` | See source/service |
| `denumire` | `String` | See source/service |
| `judet` | `String` | See source/service |

### IstoricMembruDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/IstoricMembruDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `gospodarieId` | `Long` | See source/service |
| `persoanaId` | `Long` | See source/service |
| `numeCompletPersoana` | `String` | See source/service |
| `tipEveniment` | `TipEvenimentMembru` | See source/service |
| `dataEveniment` | `LocalDate` | See source/service |
| `observatii` | `String` | See source/service |
| `documentId` | `Long` | See source/service |
| `numeFisierDocument` | `String` | See source/service |
| `createdAt` | `LocalDateTime` | See source/service |

### MachineryDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/MachineryDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `tipUtilaj` | `String` | See source/service |
| `marca` | `String` | See source/service |
| `model` | `String` | See source/service |
| `anFabricatie` | `Integer` | See source/service |
| `numarInmatriculare` | `String` | See source/service |
| `gospodarieId` | `Long` | See source/service |

### NotificareSuccesiuneDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/NotificareSuccesiuneDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `defunctId` | `Long` | See source/service |
| `defunctNume` | `String` | See source/service |
| `defunctCnpHash` | `String` | See source/service |
| `numeNotarSpnBin` | `String` | See source/service |
| `numarAdresaOficiala` | `String` | See source/service |
| `dataTrimitere` | `LocalDate` | See source/service |
| `stadiuNotificare` | `String` | See source/service |
| `observatii` | `String` | See source/service |
| `utilizatorOperare` | `String` | See source/service |
| `dataInregistrare` | `LocalDateTime` | See source/service |
| `dataDecesului` | `LocalDate` | See source/service |
| `numarCertificatDeces` | `String` | See source/service |

### PadureDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/PadureDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `tipVegetatie` | `String` | `@NotBlank(message = "Tipul de vegetație este obligatoriu")` |
| `speciePredominanta` | `String` | See source/service |
| `suprafataHa` | `Double` | `@NotNull(message = "Suprafața este obligatorie"); @Positive(message = "Suprafața trebuie să fie pozitivă")` |
| `anPlantare` | `Integer` | See source/service |
| `stareVegetatie` | `String` | See source/service |
| `observatii` | `String` | See source/service |
| `parcelaId` | `Long` | See source/service |

### ParcelaRevisionDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/ParcelaRevisionDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `revisionId` | `int` | See source/service |
| `timestamp` | `Instant` | See source/service |
| `author` | `String` | See source/service |
| `actionType` | `String` | See source/service |
| `diffs` | `Map<String, FieldDiff>` | See source/service |

### PasuneFaneataDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/PasuneFaneataDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `tipFolosinta` | `TipFolosintaPasune` | `@NotNull(message = "Tipul de folosință este obligatoriu")` |
| `suprafataHa` | `Double` | `@NotNull(message = "Suprafața este obligatorie"); @Positive(message = "Suprafața trebuie să fie pozitivă")` |
| `speciiDominante` | `String` | See source/service |
| `numarAnimalePasunat` | `Integer` | `@Positive(message = "Numărul de animale trebuie să fie pozitiv")` |
| `numarCosiriAnuale` | `Integer` | `@Positive(message = "Numărul de cosiri trebuie să fie pozitiv")` |
| `productieEstimataKgHa` | `Double` | See source/service |
| `stareVegetatie` | `String` | See source/service |
| `sistemIntretinere` | `String` | See source/service |
| `sistemIrigare` | `String` | See source/service |
| `observatii` | `String` | See source/service |
| `parcelaId` | `Long` | See source/service |

### PersoanaDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/PersoanaDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `personType` | `String` | See source/service |
| `firstName` | `String` | See source/service |
| `lastName` | `String` | See source/service |
| `cnp` | `String` | See source/service |
| `initialaTatalui` | `String` | See source/service |
| `companyName` | `String` | See source/service |
| `cui` | `String` | See source/service |
| `adresa` | `Adresa` | See source/service |
| `phoneNumber` | `String` | See source/service |
| `email` | `String` | See source/service |
| `gospodarieIds` | `List<Long>` | See source/service |
| `esteDecedat` | `Boolean` | See source/service |
| `dataDecesului` | `LocalDate` | See source/service |
| `numarCertificatDeces` | `String` | See source/service |

### PomDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/PomDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `tipInregistrare` | `TipInregistrarePom` | `@NotNull(message = "Tipul de înregistrare este obligatoriu")` |
| `specie` | `String` | `@NotBlank(message = "Specia este obligatorie")` |
| `soi` | `String` | See source/service |
| `anPlantare` | `Integer` | See source/service |
| `numarPomi` | `Integer` | `@Positive(message = "Numărul de pomi trebuie să fie pozitiv")` |
| `suprafataHa` | `Double` | `@Positive(message = "Suprafața trebuie să fie pozitivă")` |
| `densitatePomiHa` | `Integer` | `@Positive(message = "Densitatea trebuie să fie pozitivă")` |
| `starePomi` | `String` | See source/service |
| `sistemIntretinere` | `String` | See source/service |
| `sistemIrigare` | `String` | See source/service |
| `productieEstimataKg` | `Double` | See source/service |
| `observatii` | `String` | See source/service |
| `parcelaId` | `Long` | See source/service |

### RecoltareDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/RecoltareDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `parcelaId` | `Long` | See source/service |
| `parcelaDenumire` | `String` | See source/service |
| `cicluProductieId` | `Long` | See source/service |
| `cicluProductieCultura` | `String` | See source/service |
| `cultura` | `String` | See source/service |
| `dataRecoltare` | `LocalDate` | See source/service |
| `cantitateKg` | `Double` | See source/service |

### SpecieRefDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/SpecieRefDTO.java)

Support/listener type; see source for behavior.

### StatisticaAnimalDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/StatisticaAnimalDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `specie` | `SpecieAnimal` | See source/service |
| `totalCapete` | `Long` | See source/service |
| `masculi` | `Long` | See source/service |
| `femele` | `Long` | See source/service |

### StatisticaCategorieFolosintaDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/StatisticaCategorieFolosintaDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `categorieFolosinta` | `String` | See source/service |
| `suprafataTotalaHa` | `Double` | See source/service |

### StatisticaCulturaDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/StatisticaCulturaDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `specieCultura` | `String` | See source/service |
| `suprafataTotalaHa` | `Double` | See source/service |
| `productieTotalaTone` | `Double` | See source/service |

### StatisticaEfectivGrupDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/StatisticaEfectivGrupDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `specie` | `SpecieAnimal` | See source/service |
| `totalCapete` | `Long` | See source/service |

### StatisticaUtilajDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/StatisticaUtilajDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `tipUtilaj` | `String` | See source/service |
| `totalUnitati` | `Long` | See source/service |

### StatisticiRaportCompletDto

[Source](../../src/backend/src/main/java/com/multitenant/dto/StatisticiRaportCompletDto.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `culturi` | `List<StatisticaCulturaDto>` | See source/service |
| `categoriiFolosinta` | `List<StatisticaCategorieFolosintaDto>` | See source/service |
| `animaleIndividuale` | `List<StatisticaAnimalDto>` | See source/service |
| `efectiveGrup` | `List<StatisticaEfectivGrupDto>` | See source/service |
| `utilaje` | `List<StatisticaUtilajDto>` | See source/service |

### SursaApaDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/SursaApaDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `parcelaId` | `Long` | See source/service |
| `tipSursa` | `String` | See source/service |
| `debitMcOra` | `Double` | See source/service |
| `stareFunctionare` | `boolean` | See source/service |

### TerenCreateDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/TerenCreateDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `denumire` | `String` | `@NotBlank(message = "Denumirea terenului este obligatorie.")` |
| `tipTeren` | `String` | See source/service |
| `stereo70Coordinates` | `String` | See source/service |
| `polygon` | `JsonNode` | See source/service |
| `gospodarieId` | `Long` | `@NotNull(message = "Gospodaria este obligatorie.")` |

### TerenWithParcelaDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/TerenWithParcelaDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `teren` | `Teren` | See source/service |
| `parcela` | `Parcela` | See source/service |

### TipDocumentDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/TipDocumentDTO.java)

Support/listener type; see source for behavior.

### TratamentFitosanitarDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/TratamentFitosanitarDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `dataEfectuarii` | `LocalDateTime` | See source/service |
| `fenofaza` | `String` | See source/service |
| `parcelaId` | `Long` | See source/service |
| `parcelaDenumire` | `String` | See source/service |
| `agentDaunator` | `String` | See source/service |
| `catalogPppId` | `Long` | See source/service |
| `catalogPppDenumire` | `String` | See source/service |
| `catalogPppDozaOmologata` | `Double` | See source/service |
| `catalogPppTimpPauza` | `Integer` | See source/service |
| `dozaUtilizata` | `Double` | See source/service |
| `suprafataTratata` | `Double` | See source/service |
| `cantitateTotala` | `Double` | See source/service |
| `responsabil` | `String` | See source/service |
| `semnaturaElectronica` | `String` | See source/service |
| `dataIncepereRecoltare` | `LocalDate` | See source/service |
| `documentDareConsum` | `String` | See source/service |
| `dozaDepasita` | `Boolean` | See source/service |
| `justificareSupradozaj` | `String` | See source/service |
| `cicluProductieId` | `Long` | See source/service |
| `cicluProductieCultura` | `String` | See source/service |
| `unitateMasuraDoza` | `String` | See source/service |
| `dataLansarii` | `LocalDate` | See source/service |
| `numarCutiiIndivizi` | `Integer` | See source/service |

### TrimiteSpreSemnareRequest

[Source](../../src/backend/src/main/java/com/multitenant/dto/TrimiteSpreSemnareRequest.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `emailSemnatar` | `String` | See source/service |

### UserDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/UserDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `username` | `String` | See source/service |
| `role` | `String` | See source/service |
| `tenantId` | `String` | See source/service |
| `nume` | `String` | See source/service |
| `email` | `String` | See source/service |
| `activ` | `boolean` | See source/service |
| `uatId` | `Long` | See source/service |

### VitaDeVieDTO

[Source](../../src/backend/src/main/java/com/multitenant/dto/VitaDeVieDTO.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `tipInregistrare` | `TipInregistrareVita` | `@NotNull(message = "Tipul de înregistrare este obligatoriu")` |
| `specie` | `String` | `@NotBlank(message = "Specia este obligatorie")` |
| `soi` | `String` | See source/service |
| `anPlantare` | `Integer` | See source/service |
| `numarVite` | `Integer` | `@Positive(message = "Numărul de vițe trebuie să fie pozitiv")` |
| `suprafataHa` | `Double` | `@Positive(message = "Suprafața trebuie să fie pozitivă")` |
| `densitateViteHa` | `Integer` | `@Positive(message = "Densitatea trebuie să fie pozitivă")` |
| `stareVita` | `String` | See source/service |
| `sistemIntretinere` | `String` | See source/service |
| `sistemIrigare` | `String` | See source/service |
| `productieEstimataKg` | `Double` | See source/service |
| `observatii` | `String` | See source/service |
| `parcelaId` | `Long` | See source/service |

## Payload

### CetateanLoginRequest

[Source](../../src/backend/src/main/java/com/multitenant/payload/CetateanLoginRequest.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `email` | `String` | `@NotBlank` |
| `parola` | `String` | `@NotBlank` |

### CetateanSignupRequest

[Source](../../src/backend/src/main/java/com/multitenant/payload/CetateanSignupRequest.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `nume` | `String` | `@NotBlank` |
| `prenume` | `String` | See source/service |
| `tipPersoana` | `String` | See source/service |
| `cnp` | `String` | `@NotBlank` |
| `email` | `String` | `@NotBlank; @Email` |
| `parola` | `String` | `@NotBlank` |
| `telefon` | `String` | `@NotBlank` |
| `judet` | `String` | `@NotBlank` |
| `localitate` | `String` | `@NotBlank` |
| `strada` | `String` | `@NotBlank` |
| `numar` | `String` | `@NotBlank` |
| `bloc` | `String` | See source/service |
| `scara` | `String` | See source/service |
| `etaj` | `String` | See source/service |
| `apartament` | `String` | See source/service |

### CetateanUpdateRequest

[Source](../../src/backend/src/main/java/com/multitenant/payload/CetateanUpdateRequest.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `nume` | `String` | `@NotBlank` |
| `prenume` | `String` | See source/service |
| `telefon` | `String` | `@NotBlank` |
| `judet` | `String` | `@NotBlank` |
| `localitate` | `String` | `@NotBlank` |
| `strada` | `String` | `@NotBlank` |
| `numar` | `String` | `@NotBlank` |
| `bloc` | `String` | See source/service |
| `scara` | `String` | See source/service |
| `etaj` | `String` | See source/service |
| `apartament` | `String` | See source/service |

### ImpersonateRequest

[Source](../../src/backend/src/main/java/com/multitenant/payload/ImpersonateRequest.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `tenantId` | `String` | See source/service |

### LoginRequest

[Source](../../src/backend/src/main/java/com/multitenant/payload/LoginRequest.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `username` | `String` | See source/service |
| `password` | `String` | See source/service |

### TenantCreateRequest

[Source](../../src/backend/src/main/java/com/multitenant/payload/TenantCreateRequest.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `tenantId` | `String` | See source/service |
| `name` | `String` | See source/service |

### UserInfoResponse

[Source](../../src/backend/src/main/java/com/multitenant/payload/UserInfoResponse.java)

| Field | Java type | Nearby declared constraints / mapping |
| --- | --- | --- |
| `id` | `Long` | See source/service |
| `username` | `String` | See source/service |
| `role` | `String` | See source/service |
| `tenantId` | `String` | See source/service |
| `uatId` | `Long` | See source/service |

## Service-defined transfer payload

`CrossTenantTransferService.TransferRequest` is a Java record declared with its service rather than under `dto`/`payload`:

| Field | Type | Meaning |
| --- | --- | --- |
| `destinatarTenantId` | `String` | Destination tenant/schema context |
| `destinatarGospodarieId` | `Long` | Destination-local household |
| `destinatarProprietarId` | `Long` | Destination-local owner/person |
| `detaliiTransfer` | `String` | Optional transfer details |

[Source](../../src/backend/src/main/java/com/multitenant/service/CrossTenantTransferService.java).
