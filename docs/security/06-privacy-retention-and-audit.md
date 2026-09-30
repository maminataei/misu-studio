# Privacy, Retention, and Audit

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Security, product, operations, compliance\
**Owner:** Data governance area\
**Related:** [Security index](./README.md)\

## Data minimization

Studio stores account and authorization data, merchant-authored presentation,
assets, comments, history, readiness evidence, configuration, and audit.
Integrations MUST NOT send customer, order, payment, fulfillment, entitlement,
or private catalog records. Fixtures are synthetic or explicitly sanitized.

## Logs and observability

Logs and traces contain request/event identifiers, resource type, scoped opaque
IDs, operation, outcome, duration, and error category. They exclude map content,
rich text, asset bodies, credentials, tokens, comments, and provider payloads.

No telemetry leaves an installation by default. Opt-in telemetry is documented,
aggregate, revocable, and contains no site content or stable merchant identity.

## Retention

Administrators configure history, audit, readiness, failed job, export, and
unreferenced asset retention within safe minimums. Active environment versions,
rollback-protected versions, unresolved audit requirements, and referenced
assets cannot be deleted.

## Audit

Audit records are append-only and include actor type and ID, authenticated
method, scope, action, target, reason where required, request ID, old/new
semantic summaries or hashes, time, and result. Sensitive values are represented
by classification and digest, not plaintext.

Audit covers membership, identity configuration, service credentials, contract
and renderer activation, policy changes, lease takeover, commands, restore,
readiness, approval, publication, rollback, export/import, retention override,
and signing-key lifecycle.

## Export and deletion

Site export excludes identities and secrets as specified by the bundle
protocol. Deletion is a confirmed asynchronous workflow that respects legal or
operator holds, records tombstones needed for audit, revokes credentials, and
removes objects after grace.
