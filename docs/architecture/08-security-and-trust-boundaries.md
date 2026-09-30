# Security and Trust Boundaries

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Security, platform, editor, renderer, operations\
**Owner:** Security maintainers\
**Related:** [Architecture index](./README.md)\

## Trust domains

- Browser input, maps, manifests, assets, fixtures, and comments are untrusted.
- Studio API and worker code are trusted only within their declared capability.
- Renderer targets are external services authenticated per target.
- Marketplace metadata is untrusted until signatures and policy are verified.
- Host identity assertions are trusted only after service authentication,
  audience validation, replay prevention, and scoped exchange.

## Defense requirements

Every data access MUST carry explicit organization and site context.
Application predicates and PostgreSQL RLS provide independent isolation.
Authorization occurs before resource existence is disclosed. Object-storage
keys do not contain user-provided paths.

The iframe uses sandbox and CSP restrictions, an exact origin allowlist, and a
versioned MessageChannel. Preview tokens cannot be used as editor sessions or
production service credentials.

Secrets are encrypted at rest where application retrieval is necessary,
redacted from output, rotated with overlap, and referenced by key version.
Passwords and sessions remain behind the reviewed identity adapter.

## Map safety

Maps and rich text contain no executable code. URLs use allowlisted schemes and
purpose-specific validation. Bindings and actions select registered semantic
capabilities; they cannot choose arbitrary endpoints, headers, queries, or
credentials.

## Supply chain

Official npm publishing uses OIDC trusted publishing and provenance. OCI and
release artifacts use Sigstore/Cosign. Marketplace packages require publisher
and registry signatures. Deployments verify immutable digests rather than tags
where supported.

Detailed threats and controls are defined in the
[security documentation](../security/README.md).
