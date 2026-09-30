# Configuration Reference

**Status:** Authoritative  
**Audience:** Operators, release engineering, security  
**Owner:** Operations maintainers

## Rules

Configuration uses validated environment variables or mounted files. Startup
fails on unknown security-critical values, missing required values, malformed
URLs, insecure production origins, incompatible feature combinations, or
placeholder secrets.

## Configuration groups

| Group | Required behavior |
| --- | --- |
| Runtime | Environment name, public editor/API origins, log level |
| Database | URL or discrete secret reference, pool bounds, statement timeouts |
| Storage | Endpoint, region, bucket, path style, credentials, signed URL TTL |
| Identity | Local-auth enablement, OIDC issuers, redirects, session lifetime |
| Crypto | Encryption master key reference, map/webhook signing keys |
| Email | Verification/recovery adapter and sender |
| Preview | Allowed origin policy and grant lifetime |
| Runtime API | Credential lifetime, cache headers, key-set publication |
| Jobs | Concurrency, retry bounds, schedules, retention |
| Limits | Map, manifest, bundle, upload, rich text, API, and SSE limits |
| Observability | OTLP endpoint, metrics bind, sampling, redaction |
| Marketplace | Disabled by default; registry URL and trust root when enabled |

## Defaults

Security-sensitive production values have no universal secret default. Local
development may generate ephemeral values and label them unusable for retained
data. Outbound telemetry and marketplace synchronization default off.

## Reload

Log level and selected non-security operational limits MAY reload. Origins,
identity issuers, keys, database, storage, and trust roots require a controlled
restart and audit.

## Precedence

Mounted secret files override non-secret environment references only where
explicitly documented. Duplicate contradictory sources fail startup rather
than choose silently.
