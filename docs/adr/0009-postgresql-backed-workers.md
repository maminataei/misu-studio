# ADR-0009: PostgreSQL-Backed Workers

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Control-plane architecture](../architecture/04-control-plane-and-worker-runtime.md)\
**Date:** 2026-09-30\

## Context

Self-hosted installations need durable background work, retries, schedules,
deduplication, and transactional enqueueing. Mandatory Redis would add an
operational dependency before workload requires it.

## Decision

Use Graphile Worker with separate worker processes. Job handlers are
idempotent, versioned, observable, and compatible with at-least-once delivery.

## Consequences

PostgreSQL is the only required coordination service for the beta. A later
queue change remains possible behind the worker application boundary.

## Rejected alternatives

- BullMQ and mandatory Redis.
- Celery and a Python worker platform.
- A custom polling job table.

## References

- [Graphile Worker](https://worker.graphile.org/docs)
