# Upgrades and Schema Migrations

**Status:** Authoritative  
**Audience:** Release engineering and operators  
**Owner:** Release operations area

## Release inputs

Every release publishes notes covering package/API compatibility, database
migrations, map/contract support, configuration changes, security fixes,
resource changes, required operator action, rollback limits, and removed
deprecations.

## Preflight

The upgrade command verifies current and target versions, database state,
backup freshness, storage access, available disk, key availability, required
configuration, referenced historical map support, and incompatible renderer
targets.

## Expand and contract

Breaking database evolution uses:

1. expand schema compatibly;
2. deploy code capable of old and new representation;
3. backfill through observable restart-safe jobs;
4. verify invariants;
5. switch reads/writes; and
6. contract only in a later release after rollback window.

Map and contract migrations never rewrite immutable versions.

## Rolling upgrade

API versions overlap only when the release explicitly declares wire and schema
compatibility. Workers identify supported payload versions and refuse unknown
jobs without discarding them. Migration runs once before new readiness.

## Rollback

Application rollback is permitted only while the database remains compatible.
Otherwise recovery uses the documented forward fix or restore procedure.
Operators never reverse production SQL migrations ad hoc.
