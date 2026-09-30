# Secrets, Signatures, and Key Rotation

**Status:** Authoritative  
**Audience:** Security, API, operations, renderer integrators  
**Owner:** Cryptographic operations area

## Secret classes

- Local password verifiers and recovery tokens.
- OIDC client secrets.
- Integration and renderer service credentials.
- Webhook signing material.
- Map/version signing material.
- Object-storage credentials.
- Database credentials and application encryption keys.

Secrets are never included in maps, bundles, manifests, logs, traces, metrics,
errors, job payloads, or browser-readable configuration.

## Storage

Use one-way hashes for bearer credentials that require comparison only.
Encrypt retrievable secrets with authenticated encryption under a versioned
installation master key. Production keys come from an operator secret manager
or mounted secret, not database rows alone.

## Purpose separation

Map signatures, webhook signatures, preview grants, embed grants, and sessions
use separate keys or derived purposes and separate audiences. Compromise of one
purpose must not authorize another.

## Rotation

Rotation creates a new key ID, publishes verification material if applicable,
activates it for new signatures, preserves the old key for a bounded verification
window, and then retires it. Emergency revocation is distinct from scheduled
retirement and triggers alerts and renderer action.

## Map verification

Signatures cover canonical map bytes and immutable envelope fields including
version ID, hash, contract identity, and issued time. Renderers pin installation
trust roots through configuration and refresh public keys with cache validation.

## Logging

Logs may include key IDs, credential IDs, rotation state, and failure category.
They never include private keys, bearer values, ciphertext payloads, or raw
authorization headers.
