# Collaboration, History, and Publication

**Status:** Authoritative  
**Audience:** Product, editor, API, audit, QA  
**Owner:** Authoring lifecycle area

## Collaboration model

The beta permits one active editor per site draft. Other authorized users may
observe presence, inspect synchronized state, comment, and request takeover.
The lease has an expiry and monotonically changing fencing token. A stale
holder cannot write after renewal failure or takeover.

## History

Every accepted command creates an append-only changeset containing actor,
time, base and result revisions, affected paths, semantic summary, map hash,
and inverse data. Undo submits an inverse command; it does not erase history.
Restore copies a selected immutable version into the active draft and creates
one audited changeset.

Comments anchor to stable semantic entities and retain context when a section
moves. Deleting an anchor resolves it as historical rather than deleting the
discussion.

## Readiness

Readiness belongs to an exact draft revision and hash. It combines Studio
structure and safety, contract/module rules, integration policy, accessibility
audit, asset state, and signed target preflights. New commands invalidate the
report. Serious accessibility findings and any blocker prevent publication.

## Approval and publication

Organizations may allow self-publication or require a different authorized
publisher. Publication names an environment, draft revision, readiness run,
warning acknowledgements, target set, and idempotency key.

All target preflights MUST succeed. The database transaction creates one
immutable version, advances the environment pointer, records audit, and writes
an outbox event. Partial target promotion is forbidden.

Rollback moves the pointer to a retained compatible version. It does not
rewrite the active draft. Publishing also leaves the active draft open for
later work.
