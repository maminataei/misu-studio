# Marketplace and AI Evolution

**Status:** Authoritative future direction  
**Audience:** Product, ecosystem, security, architecture  
**Owner:** Ecosystem maintainers

## Beta boundary

The beta supports private contract, renderer, manifest, and template
registration. The public marketplace and AI authoring follow the deterministic
manual platform and MUST NOT delay its exit gate.

## Marketplace

The future central registry distributes metadata and signed host-installable
packages. Studio never downloads executable code into the editor or control
plane. Host developers install and deploy renderer packages, then register
their declarative manifests and conformance results.

Packages include immutable checksums, publisher identity and signature,
registry countersignature, provenance, permissions, contract compatibility,
and license metadata. Open-source and commercial packages are permitted.
Commerce Studio itself remains fully usable under Apache-2.0 without registry
or license-service connectivity.

## AI

AI is an optional producer of the same typed commands available manually. It
cannot create private schema fields, execute code, broaden data access, or
bypass validation, lease, policy, readiness, permission, or publication.

AI work is asynchronous, explicitly scoped, privacy-filtered, locally
validated, all-or-nothing when applied, and separately metered. A provider
failure leaves manual editing available and changes no map.

## Python boundary

Python MAY be introduced for isolated AI, media, or import automation where its
ecosystem provides material value. The canonical browser-portable map engine,
schemas, commands, and migrations remain TypeScript and language-neutral JSON
artifacts.
