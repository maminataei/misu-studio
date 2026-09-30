# API Errors, Events, and Idempotency

**Status:** Authoritative protocol\
**Authority:** Normative within its stated scope\
**Audience:** API, SDK, editor, integration developers\
**Owner:** API protocol area\
**Related:** [Specifications index](./README.md)\

## API envelope

Successful responses return declared resource data and request metadata.
Errors use:

~~~ts
type ApiError = {
  code: string;
  message: string;
  requestId: string;
  details?: JsonValue;
  retryable: boolean;
};
~~~

Messages are safe for the intended audience. Internal exceptions, SQL,
credentials, raw provider payloads, and tenant identifiers outside scope never
appear.

## Status semantics

- 400: structurally invalid request.
- 401: missing or invalid authentication.
- 403: authenticated but unauthorized.
- 404: resource unavailable within authorized scope.
- 409: revision, lease, idempotency, compatibility, or state conflict.
- 422: valid transport that violates semantic rules.
- 429: explicit bounded rate or quota.
- 503: required dependency unavailable.

Stable error codes, not English messages, drive client behavior.

## Idempotency

All externally retryable mutations require an idempotency key. The server
hashes canonical input and records outcome inside the relevant transaction.
Same key and same hash replay the outcome; same key with another hash returns
conflict. In-progress claims return a retryable response with bounded guidance.

## SSE

SSE events carry monotonic installation-scoped event IDs, type, resource scope,
occurred time, and typed payload. Clients resume with Last-Event-ID. If retained
history no longer covers the cursor, the server emits reset-required and the
client refreshes authoritative queries.

Events are hints, never authorization or state authority.
