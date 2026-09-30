# Authentication, Sessions, and Embedding

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Identity, API, SDK, integrators\
**Owner:** Identity security area\
**Related:** [Security index](./README.md)\

## Local and OIDC identity

Better Auth is wrapped behind a Studio-owned interface. Local authentication
requires verified email policy, secure password hashing, rate limiting,
session revocation, recovery-token expiry, and no account enumeration. OIDC
uses authorization code with PKCE, exact issuer and redirect validation, state,
nonce, and controlled account linking.

Session cookies are Secure, HttpOnly, SameSite appropriate to the deployment,
host-only where possible, rotated after privilege change, and backed by
revocable server state. State-changing browser requests require CSRF defense.

## Embedded-session exchange

~~~mermaid
sequenceDiagram
  participant B as Host backend
  participant A as Studio API
  participant H as Host browser
  participant E as Studio editor iframe
  B->>A: signed exchange request(user, site, capabilities, nonce)
  A-->>B: one-time short-lived grant
  B-->>H: editor URL and grant
  H->>E: load editor
  E->>A: redeem grant
  A-->>E: scoped Studio session
~~~

The host backend authenticates with integration-specific credentials. An
exchange includes issuer, audience, subject, organization, site, requested
capabilities, allowed parent origin, issued/expiry time, and unique nonce.
Studio maps the subject to an external identity and intersects requested
capabilities with integration and site authorization.

Grants are single-use and short-lived. They do not contain reusable service
secrets and are not accepted by runtime-map or preview endpoints.

## Framing

Studio allows framing only by configured origins for the integration. The web
SDK validates editor origin and protocol. Parent pages cannot extract Studio
cookies, and Studio does not trust parent messages before the authenticated
channel is established.

## Administrative sessions

Installation-level operations require recent authentication and, where
configured, OIDC assurance or a second factor. Changing identity, signing,
storage, or retention configuration invalidates affected long-lived sessions.
