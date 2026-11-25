# Citizens Portal

This is the independent Angular 21 citizen-facing application: account registration/login, profile, administrative service applications, personal history, public tracking, and live alerts. Institutional record management and super-administration belong to the separate sibling `frontend` application.

[Full functional guide and screenshots](../../Docs/Applications/Citizens-Portal.md) · [Setup](../../Docs/Development.md) · [Tests and limits](../../Docs/Testing.md)

Run commands in this directory. The development proxy targets the shared backend at localhost:8080. Use port 4202 when the Institutions Portal runs on 4200:

```powershell
npm ci
npm start -- --port 4202
```

The configured test builder uses Vitest/jsdom. Existing tests are largely generated smoke tests; no e2e runner is configured. The CLI examples below are retained as scaffolding guidance, not proof that every command/test is configured or passes. Full pre-expansion text is also preserved in `Docs/Historical/pre-expansion/`.

This project was generated using [Angular CLI](https://github.com/angular/angular-cli) version 21.2.18.

## Development server

To start a local development server, run:

```bash
ng serve
```

Once the server is running, open your browser and navigate to `http://localhost:4200/`. The application will automatically reload whenever you modify any of the source files.

## Code scaffolding

Angular CLI includes powerful code scaffolding tools. To generate a new component, run:

```bash
ng generate component component-name
```

For a complete list of available schematics (such as `components`, `directives`, or `pipes`), run:

```bash
ng generate --help
```

## Building

To build the project run:

```bash
ng build
```

This will compile your project and store the build artifacts in the `dist/` directory. By default, the production build optimizes your application for performance and speed.

## Running unit tests

To execute unit tests with the [Vitest](https://vitest.dev/) test runner, use the following command:

```bash
ng test
```

## Running end-to-end tests

For end-to-end (e2e) testing, run:

```bash
ng e2e
```

Angular CLI does not come with an end-to-end testing framework by default. You can choose one that suits your needs.

## Additional Resources

For more information on using the Angular CLI, including detailed command references, visit the [Angular CLI Overview and Command Reference](https://angular.dev/tools/cli) page.
