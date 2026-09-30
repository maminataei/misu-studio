# Threat Model

**Status:** Authoritative  
**Audience:** Security reviewers and all implementers  
**Owner:** Security maintainers

## Protected assets

Protect unpublished maps, assets, comments, identities, organization and site
membership, service credentials, OIDC material, signing keys, audit history,
publication authority, and integrity of published versions.

Operational customer and commerce data should not enter Studio. If an
integration violates that boundary, Studio still treats it as sensitive and
must not log or expose it.

## Adversaries

- unauthenticated internet clients;
- authenticated users crossing organization or site scope;
- malicious or compromised host integrations;
- malicious manifests, bundles, assets, rich text, or marketplace packages;
- compromised preview or renderer targets;
- replaying webhook, embed, preview, or service tokens;
- dependency and build-chain compromise; and
- operators with infrastructure access exceeding application authorization.

## Principal threats and controls

| Threat | Required control |
| --- | --- |
| Cross-tenant read/write | Explicit context, repository predicates, RLS, scoped storage |
| Stale editor write | Revision compare, fenced lease, idempotency |
| Preview escape | Separate origin, iframe sandbox, CSP, MessageChannel validation |
| Executable map content | Strict schemas, semantic bindings/actions, sanitized rich text |
| Malicious archive/media | Quarantine, bounded parsing, digest validation, derivative pipeline |
| Publication forgery | RBAC, readiness fingerprints, database transaction, signatures |
| Runtime tampering | Hash/signature verification and last-known-good cache |
| Webhook replay | Timestamp, event ID, signature, generation ordering |
| Plugin compromise | Host execution only, dual signatures, provenance, permissions |
| Secret disclosure | Encryption, hashing where possible, redaction, rotation, purpose separation |

## Trust assumptions

TLS termination, host security, PostgreSQL, object storage, OIDC provider, and
backup custody are operator responsibilities. Studio MUST document required
settings, fail safely when dependencies are untrusted, and never assume a
private network replaces authentication.

## Review cadence

Threat review is required for new public protocols, executable dependencies,
asset types, authentication methods, marketplace permissions, or data classes.
Security tests map directly to these threats.
