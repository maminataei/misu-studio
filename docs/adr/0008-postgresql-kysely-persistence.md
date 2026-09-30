# ADR-0008: PostgreSQL and Kysely Persistence

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Persistence and versioning](../architecture/07-persistence-and-versioning.md)\
**Date:** 2026-09-30\

## Context

Studio needs relational constraints, JSONB, row locking, idempotency,
tenant-aware queries, immutable versions, row-level security, and precise
publication transactions.

## Decision

Use PostgreSQL as the system of record, Kysely for typed application SQL, and
reviewed SQL migrations for schema evolution and database security.

## Consequences

Database behavior remains visible and controllable. The team owns repository
mapping and migration discipline rather than relying on an active-record ORM.

## Rejected alternatives

- Prisma ORM.
- Document database as the system of record.
- Raw node-postgres without a typed query layer.

## References

- [Kysely](https://kysely.dev/docs/getting-started)
- [PostgreSQL row security](https://www.postgresql.org/docs/current/ddl-rowsecurity.html)
