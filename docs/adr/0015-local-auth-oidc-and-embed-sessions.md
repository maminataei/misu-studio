# ADR-0015: Local, OIDC, and Embedded Identity

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Authentication and embedding](../security/01-authentication-sessions-and-embedding.md)\
**Date:** 2026-09-30\

## Context

Small self-hosted installations need local accounts. Platform deployments need
SSO. Embedded merchants should not sign in twice or give Studio host cookies.

## Decision

Use Better Auth behind a Studio-owned adapter for local accounts and generic
OIDC. Trusted host backends exchange scoped identity assertions for short-lived
embedded Studio sessions. Authorization remains Studio-owned RBAC.

## Consequences

Identity implementation is replaceable and version-pinned. Embed exchange
requires per-integration credentials, origin policy, replay prevention, and
explicit membership mapping.

## Rejected alternatives

- Bundled Keycloak.
- Host identity only.
- Studio accounts only.
- Custom authentication primitives.

## References

- [Better Auth generic OAuth](https://better-auth.com/docs/plugins/generic-oauth)
- [OpenID Connect Core](https://openid.net/specs/openid-connect-core-1_0.html)
