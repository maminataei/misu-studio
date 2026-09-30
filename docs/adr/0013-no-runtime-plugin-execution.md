# ADR-0013: No Runtime Plugin Execution in Studio

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Supply-chain trust](../security/04-supply-chain-and-plugin-trust.md)\
**Date:** 2026-09-30\

## Context

Loading third-party code into the editor or control plane creates dependency,
tenant, CSP, supply-chain, and lifecycle risks.

## Decision

Studio accepts declarative signed manifests only. Marketplace packages are
installed and executed by host developers in renderer-controlled deployments.
Inspector controls use Studio-owned declarative primitives.

## Consequences

Studio cannot offer arbitrary custom inspector UI. Advanced behavior belongs
behind typed bindings, actions, and host components.

## Rejected alternatives

- Native React plugin loading.
- Studio-hosted plugin sandboxes in the beta.
- Arbitrary merchant scripts or embeds.
