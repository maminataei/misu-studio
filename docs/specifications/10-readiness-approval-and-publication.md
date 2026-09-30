# Readiness, Approval, and Publication

**Status:** Authoritative protocol  
**Audience:** API, worker, editor, renderer, audit, QA  
**Owner:** Publication area

## Readiness request

A request identifies site, draft revision and hash, policy, effective contract,
environment, exact target set, and scenario matrix. The run is immutable.

~~~mermaid
sequenceDiagram
  participant U as Publisher
  participant A as Studio API
  participant W as Worker
  participant T as Renderer targets
  participant D as PostgreSQL
  U->>A: request readiness(revision, environment)
  A->>D: capture exact fingerprints
  A->>W: enqueue scenario and target checks
  W->>T: signed preflight(map hash, scenarios)
  T-->>W: signed evidence
  W->>D: finalize blockers and warnings
  U->>A: publish(run, acknowledgements, idempotency)
  A->>D: lock and revalidate
  A->>D: insert version, pointer, audit, outbox
~~~

## Findings

A finding has stable ID, source layer, severity, semantic location, customer
impact, evidence, and corrective action. Blockers and critical/serious
accessibility findings prevent publication. Warnings require acknowledgement
when policy says so. Informational findings do not.

## Freshness

Any draft command, policy/contract change, active-target change, fixture
change, asset-state change, or expired target evidence invalidates readiness.
Host preflight failure is fail-closed; no user override exists in the beta.

## Approval

Where independent approval is enabled, an editor submits the exact readiness
run. An authorized different actor approves or rejects it. A changed draft or
invalidated run cancels approval.

## Transaction

Publication locks site draft and environment, rechecks authorization, revision,
hash, pinned versions, findings, acknowledgements, approval, target set, and
cheap target/lifecycle gates. It inserts the immutable signed version, updates
the environment generation and pointer, records audit, and inserts outbox in
one transaction. Any failure rolls back all effects.

## Rollback

Rollback selects a retained version compatible with the current active target
set and policy allowance, runs bounded readiness as configured, then changes
the pointer atomically. It never changes the active draft.
