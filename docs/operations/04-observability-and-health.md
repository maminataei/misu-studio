# Observability and Health

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Operators, reliability, security\
**Owner:** Observability area\
**Related:** [Operations index](./README.md)\

## Signals

Applications emit structured logs, OpenTelemetry traces, metrics, and health
endpoints. Correlation uses request ID, trace ID, event ID, job ID, and
publication/readiness IDs. Site and actor identifiers are opaque and omitted
where aggregation suffices.

## Required metrics

- HTTP count, latency, size, and error code.
- Active SSE connections and resume resets.
- Command acceptance, conflicts, lease failures, and acknowledgement latency.
- Editor bootstrap service latency.
- Readiness duration and findings by category.
- Publication and rollback outcome.
- Worker queue depth, age, attempts, and terminal failures.
- Webhook latency, retries, and generation lag.
- Asset processing count, duration, and failure.
- Database pool saturation and transaction retries.
- Runtime pointer/map reads and signature failures.

## Health

Liveness reports process progress only. Readiness checks configuration,
database schema, pool acquisition, required storage, and signing availability.
Optional OIDC, SMTP, marketplace, preview, or host dependencies appear in a
diagnostic integration-health endpoint and do not necessarily fail core API
readiness.

## Privacy

Map content, comments, rich text, asset names/bodies, tokens, credentials,
customer fixtures, and raw errors are excluded. Query strings and authorization
headers are redacted before logging.

## Alerts

Alert on sustained command/publication failure, oldest job age, repeated
webhook rejection, signature verification failure, migration mismatch, backup
failure, low storage, key expiry, and last-known-good fallback activation.
