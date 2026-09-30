# Performance and Capacity

**Status:** Authoritative beta target\
**Authority:** Normative within its stated scope\
**Audience:** Engineering, QA, operators\
**Owner:** Performance area\
**Related:** [Delivery index](./README.md)\

## Workload

The beta target per installation is 1,000 sites and 25 concurrent editor
sessions. Test data includes complete full-journey maps, history, assets,
comments, multiple locales, three environments, and multiple targets.

## User-facing objectives

- Optimistic local command application completes within one animation frame for
  a representative map.
- Server command acknowledgement p95 is below 300 ms under target load.
- Editor bootstrap p95 is below two seconds excluding host-preview latency.
- Presence and lease SSE reaches connected clients p95 within one second.
- Environment pointer resolution p95 is below 150 ms from the control plane,
  though production renderers primarily use cache.

Readiness and asset processing are asynchronous and report progress; each has
scenario-specific service objectives rather than blocking HTTP.

## Resource bounds

Schemas bound map size, sections per page/site, locales, rich-text nodes, list
items, controls, command size, batch size, manifest size, fixture size, upload
size, bundle expansion, comments, and SSE backlog. Defaults are published with
implementation and may be tightened by installation or policy.

## Load tests

Exercise bootstrap bursts, sustained commands, lease renewal, SSE reconnect,
asset upload, readiness fan-out, publication contention, pointer reads,
webhook retry, and retention jobs. Measure database pool, lock wait, query
plans, worker queue age, memory, event-loop delay, and object throughput.

## Scaling

API and workers scale horizontally until PostgreSQL or storage becomes the
bottleneck. The beta does not add sharding or distributed caches. Optimization
must preserve transaction, signature, and isolation invariants.
