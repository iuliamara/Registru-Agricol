# Public Institutions Portal

This is the independent Angular 18 application for institutional agricultural register operations, tenant administration, and super-administration. The citizen-facing Angular application is in the sibling `portal-cetateni` directory. Both use the shared Spring Boot backend.

[Full functional guide](../../Docs/Applications/Public-Institutions-Portal.md) · [Setup and configuration](../../Docs/Development.md) · [Testing limits](../../Docs/Testing.md) · [Source and routes](../../Docs/Reference/Source-Inventory.md)

Run dependency commands in this directory. The dev proxy targets the backend on port 8080. For simultaneous application development use institution port 4200 and citizen port 4202; these are independent dev servers.

```powershell
npm ci
npm start -- --port 4200
```

Production builds generate Romanian and English outputs consumed by this application's Nginx configuration. The route table currently has no route guards; backend role checks remain essential. The test target references a missing `tsconfig.spec.json`, so the test command below is the configured entry point rather than a claim of passing tests. The original CLI guidance is retained below, with its pre-expansion text also preserved in `Docs/Historical/pre-expansion/`.

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 18.2.21.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.dev/tools/cli) page.
