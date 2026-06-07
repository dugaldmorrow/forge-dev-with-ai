
# Generic Sample App Requirements

This document outlines the requirements that are common to all sample apps.

### Functional Requirements

The app must be an Atlassian Forge app and thus must have a manifest.yml file and a package.json file.

### Non-functional Requirements

If the ID of the app is not known, specify the app ID in manifest.yml as `ari:cloud:ecosystem::app/{app-id}`.

If the ID of the app is known (e.g. it is already specified in manifest.yml), do not change it.

The app's source code must be defined in TypeScript unless JavaScript is requested when creating the app.

If the app source code is TypeScript, TyepScript dependencies and configuration must be defined.

The major Node.js version must be 24.

The app's source must be stored using the following directory structure:

/src/frontend/: The source for the app's frontend. This may contain subdirectories.
/src/backend/: The source for the app's backend. This may contain subdirectories.
/src/shared/: The source for the app's code that is shared between the frontend and backend. This may contain subdirectories.
/src/index.js: The main entry points to varous parts of the app.

## App Dependencies

The dependencies section of the package.json file must include all dependencies required for the app to function.

## App Development Requirements

When changes are made to the app's manifest.yml file, the app must be deployed to the development environment.

No changes must be made to .gitignore.

### Documentation Requirements

A file named Usage.md must contain markdown content that explains how to use the app.
