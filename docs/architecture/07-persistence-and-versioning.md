# Persistence and Versioning

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Backend, database, migration, and operations engineers\
**Owner:** Persistence area\
**Related:** [Architecture index](./README.md)\

## Storage model

Relational rows own identity, tenancy, status, uniqueness, references,
permissions, revisions, environment pointers, and queryable delivery state.
JSONB owns validated immutable maps, manifests, commands, evidence, reports,
and configuration envelopes with a canonical schema owner.

Large assets are stored by content digest in object storage. PostgreSQL stores
metadata, tenancy, references, derivative state, and integrity hashes.

## Draft

A site has exactly one active draft row. It stores current schema and contract
versions, canonical map, map hash, and monotonically increasing revision.
Each accepted command and its changeset commit in the same transaction as the
draft update.

Expected revision and fencing token appear in the update predicate. Failure
returns typed conflict state rather than retrying a semantic command blindly.

## Immutable version

A version contains the canonical map, hash, signature, exact contract/module
and policy versions, content/asset references, readiness evidence, actor, and
creation time. Application code and database permissions forbid updates.

## Environment pointer

The pointer identifies one immutable version and a generation number.
Publication and rollback lock the environment, validate compatibility, insert
audit and outbox records, and update the pointer in one transaction.

## Idempotency

Mutating public requests claim an idempotency key within actor, operation, and
resource scope. A repeated equivalent request returns the recorded response.
A repeated key with different canonical input returns conflict. Records outlive
the maximum client retry period.

## Retention

Published, environment-referenced, rollback-protected, audit-required, or
bundle-export-referenced data cannot be collected. Policy may prune superseded
draft changes and unreferenced assets only after reachability calculation and
grace period. Deletion is auditable and resumable.
