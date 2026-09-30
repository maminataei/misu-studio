# Testing Strategy

**Status:** Authoritative  
**Audience:** Engineering, QA, security, release  
**Owner:** Quality maintainers

## Test pyramid

- Pure unit and property tests cover schemas, canonicalization, commands,
  inverses, migrations, contract composition, policies, hashes, and signatures.
- PostgreSQL integration tests cover repositories, RLS, transactions, locks,
  idempotency, worker jobs, retention, and outbox.
- API contract tests validate every OpenAPI request, response, error, auth, and
  generated client.
- Browser E2E covers editor, iframe preview, accessibility, sessions, SSE, and
  supported browsers.
- Conformance tests run against reference and Misu renderers.
- Deployment tests exercise Compose and disposable Kubernetes.

## Required scenarios

### Commands and concurrency

Duplicate requests, lost responses, stale revision, invalid inverse, expired
lease, takeover fencing, concurrent publish/edit, policy upgrade, and restore
across schema versions.

### Publication and runtime

Changed draft after readiness, changed target set, expired evidence, preflight
outage, one target failure, warning acknowledgement, approval separation,
transaction fault injection, webhook duplicates/out-of-order delivery,
signature tampering, key rotation, Studio outage, and rollback.

### Security

Cross-organization/site access, guessed nested IDs, CSRF, session fixation,
OIDC mix-up, embed/preview replay, origin spoofing, XSS-rich text, URL schemes,
archive traversal/bombs, media parser limits, external asset authorization,
SSRF controls, webhook timing/replay, and malicious manifests.

### Full commerce journey

Discovery, product variants, physical/digital/hybrid fulfillment, cart changes,
checkout requirements, payment outcomes, account states, orders, entitlements,
reviews, Q&A, wishlist, support, empty/error/unavailable/lifecycle conditions,
locales, RTL, and view modes.

## Determinism

Golden fixtures run in supported Node environments and browser builds.
Canonical bytes and hashes must match. Property tests generate bounded valid
maps and command sequences; fuzz tests target parsers with strict resource
limits.

## Accessibility

Automated axe-style checks run for editor and scenario matrix. Keyboard and
screen-reader manual plans cover drag alternatives, focus recovery, dialogs,
errors, live progress, preview selection, and publication.

## Release evidence

CI stores test summaries, coverage by invariant, conformance reports, SBOM,
provenance, migration results, browser matrix, performance output, and
deployment smoke results for the release.
