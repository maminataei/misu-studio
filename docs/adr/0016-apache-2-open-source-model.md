# ADR-0016: Apache-2.0 Open-Source Model

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Product charter](../product/00-product-charter.md)\
**Date:** 2026-09-30\

## Context

Commerce platforms need confidence that self-hosted core functionality will
not become license-gated. Contributors and commercial adopters benefit from an
explicit patent grant.

## Decision

License Commerce Studio under Apache-2.0. All self-hosted editor, control-plane,
SDK, governance, and marketplace-client features are open source.

## Consequences

Commercial hosted forks are permitted. Ecosystem revenue may come from support,
services, or marketplace activity, not mandatory core licensing.

## Rejected alternatives

- Proprietary or source-available core.
- AGPL network copyleft.
- Open core with closed governance features.

## References

- [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)
