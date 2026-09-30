# ADR-0014: Atomic Publication and Last Known Good

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Readiness and publication](../specifications/10-readiness-approval-and-publication.md)\
**Date:** 2026-09-30\

## Context

Multiple renderers may serve one site. Partial rollout creates inconsistent
customer experiences, while runtime dependence on Studio threatens storefront
availability.

## Decision

An environment points atomically to one immutable version across its active
target set. Every target preflights the exact map. Renderers cache and continue
serving the last signature-verified version during Studio outage.

## Consequences

One unhealthy target blocks promotion. Rollback is a pointer operation. Hosts
must implement durable cache and signature verification.

## Rejected alternatives

- Per-renderer independent publication.
- Live Studio lookup for every storefront request.
- Publication based only on contract certification.
