# System Architecture

**Status:** Authoritative  
**Audience:** All technical contributors  
**Owner:** Architecture maintainers  
**Related:** [Product charter](../product/00-product-charter.md)

## Architectural thesis

Commerce Studio is a control plane for semantic presentation intent. It is not
in the storefront request path, a renderer host, a commerce database, or a
code generator. The canonical map engine is browser-portable and deterministic;
the control plane supplies persistence, authorization, validation, readiness,
and distribution around it.

~~~mermaid
flowchart LR
  User[Merchant editor] --> Host[Commerce platform]
  Host -->|embed grant| Editor[Studio editor]
  Editor --> API[Studio API]
  API --> DB[(PostgreSQL)]
  API --> Assets[(S3-compatible storage)]
  API --> Jobs[PostgreSQL job queue]
  Jobs --> Worker[Studio worker]
  Editor <-->|preview protocol| Preview[Host preview adapter]
  API -->|signed pointer and map| Renderer[Host renderer targets]
  API -->|signed event| Host
  Renderer --> Commerce[Live commerce services]
  Customer[Storefront customer] --> Renderer
~~~

## Core invariants

1. The same canonical schemas, command semantics, migrations, serialization,
   and hashes apply in browser tooling and server validation.
2. No renderer implementation is imported by Studio.
3. No map contains executable code or live operational truth.
4. Every mutable draft write is authorized, leased, revision-checked,
   idempotent, validated, and audited.
5. Every published version is immutable, signed, and independently fetchable.
6. An environment points to exactly one version for all active targets.
7. Storefront availability does not depend on a live Studio request.
8. A contract or policy upgrade is explicit; it never silently mutates a map.

## Runtime planes

The authoring plane includes the editor, API, worker, PostgreSQL, and object
storage. The integration plane includes embed exchange, preview, preflight,
runtime map fetch, and webhooks. The storefront plane belongs entirely to host
renderers and commerce services.

Compromise or outage of one plane MUST have bounded effects. In particular,
authoring failure does not invalidate an already verified map in the storefront
plane.

## Technology baseline

The repository uses strict TypeScript, pnpm workspaces, and Turborepo. The
editor uses React and Vite. The control plane uses Fastify and OpenAPI, schemas
use TypeBox and JSON Schema, PostgreSQL access uses Kysely plus reviewed SQL
migrations, asynchronous jobs use Graphile Worker, identity is behind a Better
Auth adapter, and media uses S3-compatible storage.
