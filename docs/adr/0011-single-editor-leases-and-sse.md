# ADR-0011: Fenced Lease and SSE

**Status:** Accepted  
**Date:** 2026-09-30

## Context

Simultaneous editing requires CRDT semantics across commands, contracts,
assets, and migrations. The beta needs safe collaboration without silent
overwrites.

## Decision

Permit one active editor through an expiring fenced lease. Use expected
revisions and idempotent HTTP commands. Use resumable SSE for server events.

## Consequences

Others can view, comment, and request takeover. Offline editing and live
multiplayer are excluded. HTTP remains the mutation authority.

## Rejected alternatives

- CRDT multiplayer.
- WebSocket commands.
- Last-write-wins concurrent editing.
