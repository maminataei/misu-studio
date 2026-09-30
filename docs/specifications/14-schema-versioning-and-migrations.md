# Schema Versioning and Migrations

**Status:** Authoritative protocol  
**Audience:** Core, contract, persistence, release, renderer  
**Owner:** Compatibility area

## Independent versions

Map schema, base contract, modules, renderer manifest, preview protocol,
conformance suite, API, bundle format, and database schema evolve independently
with explicit compatibility declarations.

Official npm packages use synchronized SemVer, but a package release does not
silently change a persisted artifact's pinned version.

## Map migrations

Migrations are pure sequential functions from one schema/contract composition
to the next. They accept canonical input and return canonical output plus a
human-readable change report. They do not access databases, networks, clocks,
randomness, environment variables, or host data.

Every migration has fixtures for valid input, expected output, idempotent
canonicalization, lost/changed semantics, reverse-restoration behavior, and
all still-supported historical versions.

Original immutable versions are never rewritten. Preview may migrate in memory.
Draft upgrade persists through an explicit audited command. Restore migrates a
copy into the current draft.

## Renderer compatibility

A renderer release declares exact contract/module support and protocol ranges.
An environment may activate only releases that cover the version it serves.
Removing support requires migration and republishing of every referenced map
before release retirement.

## Database migrations

Database migrations are forward-only after release. Expand/contract changes
deploy compatibility code before destructive cleanup. Migration jobs are
exclusive, observable, restart-safe, and backed by restore-tested backups.

## Deprecation

Public deprecation identifies replacement, affected versions, warning start,
last supported release, and migration path. A retained published version cannot
be orphaned by a routine upgrade.
