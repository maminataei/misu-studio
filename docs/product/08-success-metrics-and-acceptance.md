# Success Metrics and Acceptance

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Product, engineering, QA, operators\
**Owner:** Product and quality maintainers\
**Related:** [Product index](./README.md)\

## Product success

The beta demonstrates that a commerce platform can integrate once, provision
isolated merchant sites, offer complete manual authoring, and publish one map
that behaves coherently in Misu and an independent reference renderer.

Measure:

- successful editor bootstrap, command, readiness, and publication rates;
- time from starter kit to a readiness-passing draft;
- renderer conformance failure categories;
- undo, restore, rollback, and recovery success;
- accessibility blocker and warning rates;
- webhook delivery latency and retries; and
- preview-to-production structural parity.

No metric collection leaves a self-hosted installation unless an administrator
explicitly opts in.

## Beta capacity

One installation MUST support 1,000 sites and 25 concurrent editor sessions.
At that load, local editor response remains within a frame, command
acknowledgement p95 is below 300 ms, and editor bootstrap p95 is below two
seconds, excluding host preview latency.

## Exit acceptance

The beta exits only when:

1. the map and command suites pass deterministic cross-runtime fixtures;
2. Misu and a non-React reference renderer pass conformance against the same
   contract and published map;
3. every full-journey protected scenario is previewed and tested;
4. serious accessibility failures block publication;
5. tenant, session, iframe, asset, webhook, and signature security suites pass;
6. publish and rollback are atomic under retries and concurrency;
7. renderers serve their last verified version through Studio outage;
8. Compose and Helm installation, upgrade, backup, and restore are verified;
9. current evergreen Chrome, Edge, Firefox, and Safari pass editor E2E; and
10. the legacy Misu Appearance path is removed without leaving two authorities.
