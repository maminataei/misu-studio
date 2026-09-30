# Security Policy

**Status:** Active\
**Authority:** Normative vulnerability disclosure policy\
**Audience:** Users, operators, security researchers, and maintainers\
**Owner:** Security maintainers\
**Related:** [Security specifications](./docs/security/README.md)\

## Reporting

Do not report suspected vulnerabilities in public issues. Use GitHub private
vulnerability reporting for this repository. If that facility is unavailable,
contact the repository owner through a private verified channel and include the
affected version, reproduction, impact, and any known mitigation.

## Supported versions

Before the first stable release, only the latest tagged prerelease is supported.
After stability, the current major release and the documented security support
window receive fixes. Renderer contract compatibility is independent of
control-plane security support.

## Response

Maintainers MUST acknowledge a credible report, establish severity, protect
reporter confidentiality, prepare coordinated fixes, rotate exposed trust
material where necessary, and publish an advisory after users can remediate.

## Security boundaries

The security specification covers tenant isolation, embedded sessions, preview
sandboxing, service credentials, signing keys, webhooks, assets, manifests, and
supply-chain provenance. Self-hosted operators remain responsible for network,
host, database, object-storage, identity-provider, and backup security.
