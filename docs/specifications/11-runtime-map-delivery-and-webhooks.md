# Runtime Map Delivery and Webhooks

**Status:** Authoritative protocol  
**Audience:** API, renderer, integration, operations  
**Owner:** Runtime delivery area

## Authentication

Each renderer target has rotatable scoped service credentials. Credentials
grant runtime reads only for declared integration, sites, and environments.
Secrets are stored hashed where comparison is sufficient. Rotation supports a
bounded overlap and is audited.

## Resolution

The runtime API exposes:

- environment resolution returning generation, version ID, contract identity,
  map hash, signature metadata, and cache validators; and
- immutable version retrieval returning canonical bytes and signature.

Clients use If-None-Match and cache by version ID and hash. Pointer responses
are short-lived; immutable version responses are long-lived.

## Verification and fallback

A renderer verifies version identity, SHA-256 hash, installation signature,
contract compatibility, and retained signing-key trust before activation. It
persists the last verified map locally. On timeout, authentication failure, or
invalid new data, it continues serving the last verified map and alerts rather
than serving an unverified version.

## Webhooks

Publication outbox creates a signed event containing event ID, type, issued
time, delivery attempt, site, environment, generation, version ID, hash, and
key ID. The signature covers canonical body and selected headers. Timestamps
and event IDs prevent replay.

Delivery is at least once with exponential backoff and jitter. Consumers
deduplicate by event ID and ignore older generations. Webhook success is not
part of the publication transaction; renderers can discover the pointer by
polling after missed delivery.

## Signing keys

Version and webhook signing use separate purposes. Key records have ID,
algorithm, activation, retirement, and revocation state. Public verification
material remains available through a cacheable key set during the support
window.
