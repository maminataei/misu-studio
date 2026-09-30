# Deployment Topology

**Status:** Authoritative  
**Audience:** Operators, platform engineers, security  
**Owner:** Operations architecture area

## Supported topology

~~~mermaid
flowchart TB
  Proxy[Ingress or reverse proxy]
  Proxy --> Editor[Static editor]
  Proxy --> API1[API replica]
  Proxy --> API2[API replica]
  API1 --> PG[(PostgreSQL)]
  API2 --> PG
  Worker1[Worker replica] --> PG
  Worker2[Worker replica] --> PG
  API1 --> S3[(S3-compatible storage)]
  API2 --> S3
  Worker1 --> S3
  Worker2 --> S3
  API1 --> OIDC[OIDC provider]
  Worker1 --> Hosts[Renderer and webhook targets]
~~~

The editor is static. API and worker replicas are stateless apart from bounded
in-memory caches. PostgreSQL coordinates drafts, leases, jobs, idempotency, and
publication. Object storage contains assets and portable bundles. Redis is not
required.

## Packaging

Official releases provide signed multi-architecture OCI images, a Docker
Compose profile, and a Helm chart. Compose may run bundled PostgreSQL and local
S3-compatible storage for evaluation. Production guidance uses operator-owned
PostgreSQL and object storage with independent backup.

## Availability

API replicas may scale horizontally. Worker concurrency is bounded by queue and
database capacity. Migrations run as an exclusive pre-deployment job. Readiness
fails until required schema is current and signing/storage dependencies are
available.

## Network

Public ingress exposes editor, authentication callbacks, API, SSE, and runtime
map reads according to route policy. PostgreSQL and object storage are private.
Outbound allowlists cover configured OIDC, preview/preflight, webhook, registry,
and storage endpoints. The editor and preview SHOULD use distinct origins.

## Self-hosting

An installation performs no mandatory call to a Commerce Studio vendor.
Central marketplace connectivity is optional. Disabling it does not reduce
core authoring, publication, export, or renderer functionality.
