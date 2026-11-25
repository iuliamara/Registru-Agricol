# Installation, configuration, and local development

[Documentation index](README.md) · [Testing](Testing.md) · [Multi-tenancy](Multi-Tenancy.md)

The repository has three build roots: two independent Angular workspaces and one Maven backend. Run package commands inside the relevant application directory. A root `node_modules` directory is not a shared frontend workspace configuration.

## Prerequisites and configuration sources

| Component | Requirement established by the repository |
| --- | --- |
| Backend | JDK 21 and Maven; Docker builds use Maven 3.9.7 / Eclipse Temurin 21 |
| Citizens Portal | Node/npm compatible with Angular 21.2 and its lockfile package engines; TypeScript 5.9; package manager declaration npm 11.6.2 |
| Institutions Portal | Node/npm compatible with Angular 18.2 and its lockfile package engines; TypeScript 5.5 |
| Container workflow | Docker Engine/Desktop with Compose; frontend Dockerfiles use Node 20 Alpine and Nginx |
| Database | PostgreSQL; Compose uses PostgreSQL 15 with PostGIS 3.3 image |
| Events | Kafka; Compose also starts ZooKeeper |

Use each application's lockfile and supported Node engine range; an arbitrarily old Node 20 installation may not meet the citizen toolchain's minimum. There is no requirement to install Angular CLI globally: npm scripts resolve the workspace CLI.

Read [`.env.example`](../.env.example), [`docker-compose.yml`](../docker-compose.yml), and [`application.yml`](../src/backend/src/main/resources/application.yml) together. Spring optionally imports `../../.env` as properties **relative to the backend working directory**. Docker Compose interpolation and Spring environment loading are different mechanisms.

## Environment variables

| Variable | Consumer / default / practical meaning |
| --- | --- |
| `POSTGRES_DB` | Compose database name, default `multi_tenant_db` |
| `POSTGRES_USER` / `POSTGRES_PASSWORD` | Compose PostgreSQL account; set password locally |
| `SPRING_DATASOURCE_URL` | Backend JDBC URL; native YAML default localhost:5432, Compose default `db:5432` only when not overridden by `.env` |
| `SPRING_DATASOURCE_USERNAME` / `SPRING_DATASOURCE_PASSWORD` | Backend database credentials; match the database |
| `SPRING_JPA_HIBERNATE_DDL_AUTO` | Default `none`; migrations govern schema |
| `SPRING_KAFKA_BOOTSTRAP_SERVERS` | Native default localhost:9092; Compose explicitly kafka:29092 |
| `JWT_SECRET` | JWT signing material; local example is a development value |
| `APP_CRYPTO_AES_KEY` | Input to identifier encryption key derivation; keep consistent with stored records |
| `APP_CRYPTO_SALT` | Salt for exact-match identifier hashes; required and must remain consistent with stored indexes |
| `SPRING_MAIL_HOST` / `SPRING_MAIL_PORT` | SMTP; defaults sandbox.smtp.mailtrap.io / 2525 |
| `SPRING_MAIL_USERNAME` / `SPRING_MAIL_PASSWORD` | SMTP credentials; current Compose forwards these two mail variables |
| `APP_MAIL_FROM` | Sender address; YAML default `test@test.ro` |
| `APP_DOCUMENTS_STORAGE_PATH` | Household files; YAML default `/data/documents` |
| `APP_SIGNATURE_STORAGE_PATH` | Signed contracts; default `/data/signed-contracts` |
| `SIGNNOW_BASE_URL` | Default `https://api.signnow.com` |
| `SIGNNOW_BASIC_TOKEN`, `SIGNNOW_USERNAME`, `SIGNNOW_PASSWORD` | Remote signing credentials; defaults blank |

Current Compose explicitly forwards database/JWT/crypto, Kafka, and SMTP username/password, but **not** every mail host/from, signing, or storage override. Adding a variable to the root `.env` does not automatically forward it into the backend container. Use an explicit environment override when those settings are needed. Do not copy credential values out of historical documentation.

## Docker Compose workflow

From the repository root, copy `.env.example` only if there is no local `.env` to preserve:

```powershell
Copy-Item .env.example .env
```

Edit the local file. For this workflow the JDBC value must target the database service:

```dotenv
SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/multi_tenant_db
```

The example file currently supplies localhost:5432, which overrides the Compose expression's fallback. Leaving it unchanged makes the backend attempt to reach PostgreSQL inside its own container. Set matching database credentials and choose local JWT/crypto values before initial data creation.

```powershell
docker compose up --build
```

| Service | Host port | Container port / address |
| --- | --- | --- |
| Institutions Portal | 80 | Nginx 80; localized `/ro/` and `/en/` |
| Citizens Portal | 4202 | Nginx 80 |
| Backend | 8080 | Spring Boot 8080 |
| Database | 5433 | PostgreSQL 5432 at `db:5432` |
| Kafka | 9092 | Host listener localhost:9092; internal listener kafka:29092 |
| ZooKeeper | 2181 | 2181 |

The institution root redirects according to language cookie/Accept-Language, defaulting to Romanian. Citizen routing serves the SPA fallback. Both Nginx configurations proxy `/api/` to `backend:8080`, including WebSocket upgrade headers. These same-origin proxies are part of the intended local authentication setup; cookie names are distinct but cookies are scoped by host/path rather than application port.

Compose has `depends_on` and restart policies but no service health checks. Initial database/Kafka readiness may lag container startup; inspect logs instead of treating container creation as completed application readiness.

```powershell
docker compose ps
docker compose logs --tail 100 backend
docker compose logs --tail 100 db kafka
```

Ordinary stop preserves the named database volume:

```powershell
docker compose down
```

Volume deletion is not required for routine startup or documentation review. This documentation task did not reset databases or run the application stack.

## Native backend with container infrastructure

Start only dependencies if desired:

```powershell
docker compose up -d db kafka zookeeper
```

From a backend terminal, target the **host** database port and Kafka listener:

```powershell
Set-Location src/backend
$env:SPRING_DATASOURCE_URL = 'jdbc:postgresql://localhost:5433/multi_tenant_db'
$env:SPRING_KAFKA_BOOTSTRAP_SERVERS = 'localhost:9092'
$env:APP_DOCUMENTS_STORAGE_PATH = 'C:/practica/Registru-Agricol/uploads'
$env:APP_SIGNATURE_STORAGE_PATH = 'C:/practica/Registru-Agricol/uploads/signed-contracts'
mvn spring-boot:run
```

Supply matching credentials/JWT/crypto values through the local `.env` import or environment. With a native PostgreSQL server on 5432, use that server's host port instead. Avoid starting a second backend when Compose already publishes 8080.

Backend package build:

```powershell
# From src/backend
mvn package
```

The Dockerfile uses `mvn clean package -DskipTests`; an image build is not evidence of a passing test suite.

## Independent frontend development

Start each app in a separate terminal with the backend listening on 8080. Angular CLI is scoped to the local dependency install.

```powershell
# Repository root, terminal A
Set-Location src/frontend
npm ci
npm start -- --port 4200
```

```powershell
# Repository root, terminal B
Set-Location src/portal-cetateni
npm ci
npm start -- --port 4202
```

The institutional proxy targets `127.0.0.1:8080`, with explicit `/api/ws` WebSocket handling; the citizen proxy targets `localhost:8080` and enables WebSocket proxying. Both are configured as serve options in their own `angular.json`. No backend URL is injected from the institutional environment templates; those currently contain only the `production` flag.

Local institution language configurations:

```powershell
# src/frontend
npm start -- --configuration=ro --port 4200
# Use configuration=en for English in a separate invocation.
```

Production builds:

```powershell
# Run in each application's directory
npm run build
```

The institutional production configuration localizes both languages below `dist/frontend/browser/`; the citizen build targets `dist/portal-cetateni/browser/`. These paths are consumed by the respective Dockerfiles. If `npm ci` reports a peer/lock conflict, retain the actual error for investigation; do not assume the Dockerfile's institutional `npm install --legacy-peer-deps` is a reproducible equivalent to a passing clean install.

## Development data and accounts

Public migrations seed initial tenant/UAT data. `DatabaseSeeder` migrates all registered tenants, ensures institutional and citizen demo accounts, and populates varied persons, households, land/parcels, crops, animals, buildings, machinery, and chemical records in demo tenants. Individual sections often check existence/count, but the runner is **not guarded by a development profile** and is not a general controlled data-import system.

| Account | Credential behavior in current source | Intended interface |
| --- | --- | --- |
| `cluj_admin` | Seeder password `password123`, if created by the runner | Institutions tenant administrator |
| `cluj_user` | Seeder password `password123`, if created by the runner | Institutions operational user |
| `buc_admin` | Seeder password `password123`, if created by the runner | Institutions tenant administrator |
| `cetatean@registru.ro` | Seeder password `password123`, if created by the runner | Citizens Portal |
| `superadmin` | Public V1/V2 migrations supply the normal initialized account; runner fallback uses `superadmin` only if the user is absent | Institutions super-administrator |

Existing databases can have changed passwords, so source seed values do not guarantee current credentials. Use the migration/account source or authorized database administration when the initialized super-admin password is unknown. This guide does not reset existing accounts. Seed identity/contact records are demonstration data, not evidence of production users.

## Files, email, and signing

Compose mounts `./uploads` to `/data/documents`; metadata lives in PostgreSQL. Back up files and database together if preserving document links. Signed contracts default to another container directory that is **not mounted** by current Compose, so container replacement can lose those PDFs. Contract filenames also omit tenant ID. These limitations are documented, not changed here.

SMTP credentials enable confirmation email; blank/unavailable credentials may produce logged send failures while a application is saved. SignNow requires explicit container/environment forwarding and valid remote credentials. Do not test invitation actions against real recipients as a routine local smoke test. No email or signing invitation was sent during this documentation task.

## Troubleshooting

| Symptom | First source-based check |
| --- | --- |
| Backend cannot connect to DB in Compose | `.env` JDBC host must be `db:5432`, not localhost; credentials must match initialized volume |
| Native backend cannot connect | Compose exposes 5433; native PostgreSQL may use 5432; check which database is running |
| Citizen application fails for a listed locality | Static UAT ID must exist globally and have an assigned/provisioned tenant |
| Domain endpoint returns public-context error | Institutional token needs a tenant; active-UAT UI selection alone does not reissue tenant JWT |
| Super-admin tenant view gets 403 on UAT/application API | Endpoint role expressions omit SUPER_ADMIN on specific routes, even during impersonation |
| Tenant detail assignment fails | Frontend calls a tenant-UAT path with no matching backend controller |
| Login state appears stale | Local identity metadata and cookie state can diverge; institution app does not automatically revalidate `/me` |
| Opaque CNP/CUI appears or search misses old data | Check encryption key/salt consistency and historical SQL backfills; converter can return undecryptable stored values |
| Live updates absent | Backend/Kafka status, `/api/ws` proxy, current app subscription; no durable delivery replay |
| Contract alerts repeat | Current scheduler runs every minute without notification deduplication |
| Upload fails below advertised 10 MiB | Spring multipart limits can be smaller than service validation; MIME allowlist also applies |
| Accepted PDF fails or opens wrong lookup context | Tenant-local numeric-ID collision and PDF-role asymmetry are known integration limits |

## Contribution workflow

Keep the applications' independent dependencies/build instructions separate. Verify a claimed feature against its Angular binding, backend endpoint/service, entity, and migration; record partial integration honestly. Preserve historical specifications in [Historical](Historical/README.md) rather than rewriting them into current guarantees. Run focused relevant tests when changing application behavior; [Testing](Testing.md) describes actual coverage and configuration issues.
