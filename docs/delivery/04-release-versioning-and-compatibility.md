# Release, Versioning, and Compatibility

**Status:** Authoritative  
**Audience:** Maintainers, release engineering, integrators, operators  
**Owner:** Release maintainers

## Version train

Official @commerce-studio packages use synchronized SemVer. Editor, API,
worker, CLI, schemas, core, web SDK, manifest SDK, conformance, and generated
client share a release version even when some package content does not change.

OCI images and Helm charts use the same release tag and immutable digest.
Prereleases use explicit beta identifiers.

## Compatibility

Persisted and public artifacts have independent explicit versions. A release
publishes a compatibility matrix for map schemas, contract/module versions,
renderer manifests, preview protocol, conformance suites, API clients, bundles,
database schema, and browser support.

Minor releases cannot invalidate a valid retained map or remove a public API
without the documented deprecation window. Major releases include migrations
and operational rollout.

## Publication

npm uses trusted publishing and provenance. OCI artifacts, SBOMs, release
archives, and checksums are signed. Source tags are protected and map exactly
to generated artifacts. Release notes identify security, configuration,
migration, compatibility, and rollback impact.

## Support

Before 1.0, only the latest prerelease line is operationally supported, but
persisted-format migrations cover every version introduced into retained test
fixtures. After 1.0, the project declares a security window and renderer/map
compatibility window separately.

## Deprecation

Deprecation starts with warnings and replacement guidance, records telemetry
locally, and names the earliest removal release. Operators can inventory use.
Removal never orphans an active environment without a migration path.
