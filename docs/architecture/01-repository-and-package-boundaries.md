# Repository and Package Boundaries

**Status:** Authoritative  
**Audience:** Maintainers and implementers  
**Owner:** Architecture maintainers

## Workspace

The repository MUST contain independently deployable applications and
independently publishable packages. Packages may not import applications.

~~~mermaid
flowchart TD
  Schemas["@commerce-studio/schemas"] --> Core["@commerce-studio/core"]
  Schemas --> Manifest["@commerce-studio/manifest-sdk"]
  Core --> Editor["apps/editor"]
  Core --> API["apps/api"]
  Core --> CLI["apps/cli"]
  Manifest --> Conformance["@commerce-studio/conformance"]
  Manifest --> Editor
  WebSDK["@commerce-studio/web-sdk"] --> Editor
  APIClient["@commerce-studio/api-client"] --> Editor
  APIClient --> CLI
  UI["@commerce-studio/ui"] --> Editor
  API --> Worker["apps/worker"]
~~~

## Applications

- apps/editor is a static React/Vite SPA usable standalone or in an iframe.
- apps/api is the Fastify control-plane process.
- apps/worker runs Graphile Worker tasks without exposing public HTTP.
- apps/cli validates, certifies, imports, exports, and administers.
- examples/reference-renderer proves framework and Misu independence.

## Packages

- schemas owns TypeBox definitions and published JSON Schema.
- core owns canonicalization, hashes, migrations, commands, diffs, inverses,
  validation, and policy evaluation.
- manifest-sdk authors commerce contracts, modules, policies, controls, and
  renderer manifests.
- conformance owns portable fixtures and certification reports.
- web-sdk owns iframe embedding and preview messaging.
- api-client is generated from the committed OpenAPI contract.
- ui owns editor presentation primitives, not renderer components.

## Dependency rules

Core and schema packages MUST NOT import React, Fastify, PostgreSQL clients,
object storage, identity libraries, browser globals, or host code. Infrastructure
adapters implement interfaces at application boundaries. Generated artifacts
are checked for drift in CI.

Official packages release on synchronized SemVer. A package may declare a
compatibility range, but the release train keeps examples, schemas, protocols,
and clients coherent.
