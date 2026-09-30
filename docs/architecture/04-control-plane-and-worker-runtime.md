# Control Plane and Worker Runtime

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Backend and operations engineers\
**Owner:** Control-plane area\
**Related:** [Architecture index](./README.md)\

## API

The Fastify API is a modular monolith. Modules own route registration,
application services, repository interfaces, authorization, and schemas for
one domain. Route handlers validate transport, establish actor and tenant
context, call application services, and serialize declared responses. They do
not contain persistence or domain decisions.

OpenAPI 3.1 is generated from trusted TypeBox schemas and committed for drift
review. Third-party manifest data is interpreted after validation; it is never
compiled into server code.

## Transactions

Application services define transaction boundaries. Kysely uses one acquired
connection for every transaction. Publication, lease takeover, idempotency
claim, and command application use row locks or compare-and-swap predicates as
specified. SQL migrations are reviewed, forward-only in deployed environments,
and separate schema change from destructive cleanup.

## Worker

Graphile Worker shares PostgreSQL but runs as a separate process in production.
Jobs cover asset processing, readiness orchestration, webhook delivery,
retention, export/import preparation, registry synchronization, and later AI.

Every job:

- has a versioned payload schema;
- is safe under at-least-once execution;
- records terminal outcome and diagnostic category;
- uses bounded retries with backoff and jitter;
- separates retryable provider failure from permanent validation failure; and
- avoids storing secrets or sensitive payloads in logs.

## Outbox

Transactions that require external effects write an outbox record atomically.
A worker converts outbox records into signed deliveries. The domain transaction
does not wait on a host endpoint. Delivery ordering is preserved per
environment where order is meaningful, while consumers remain idempotent.

## Degradation

Worker outage leaves draft commands available but pauses asset derivatives,
full readiness, webhooks, exports, and AI. API or database outage blocks
authoring and publication but does not affect cached storefront maps.
