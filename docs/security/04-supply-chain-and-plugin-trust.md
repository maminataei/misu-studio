# Supply Chain and Plugin Trust

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Release, registry, integrators, security\
**Owner:** Supply-chain security area\
**Related:** [Security index](./README.md)\

## Official releases

CI publishes npm packages through OIDC trusted publishing with provenance.
OCI images are built from tagged source in isolated workflows, referenced by
digest, accompanied by SBOM and provenance, and signed with Sigstore/Cosign.
Release workflows use protected environments and no long-lived publishing
token where federation is available.

## Marketplace trust flow

~~~mermaid
flowchart LR
  Source[Publisher source] --> Build[Publisher build]
  Build --> Pkg[Package + manifest + SBOM]
  Pkg --> PSig[Publisher signature]
  PSig --> Review[Registry validation and policy]
  Review --> RSig[Registry countersignature]
  RSig --> Install[Host developer installation]
  Install --> Deploy[Host-controlled renderer deployment]
  RSig --> Import[Studio imports declarative metadata only]
~~~

The registry verifies publisher namespace, immutable digest, signatures,
provenance, malware results, declared permissions, license metadata, contract
compatibility, and known vulnerability policy. The registry signature attests
reviewed metadata; it does not guarantee package correctness.

## Execution boundary

Marketplace code executes only after a host developer installs and deploys it.
Studio imports the signed manifest and report, not the package executable.
Commercial entitlement may control registry download, but core Studio never
contacts a license server to function.

## Revocation

Registry advisories may mark a release compromised or deprecated. Installations
surface the advisory and may block new activation according to policy.
Existing published maps are not silently rewritten; operators follow a
documented migration and renderer replacement process.

## Dependency policy

Dependencies are pinned through a lockfile, reviewed for maintenance and
license, scanned in CI, and updated through controlled changes. Install scripts
are disabled unless an explicit reviewed dependency requires one.
