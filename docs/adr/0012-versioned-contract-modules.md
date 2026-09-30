# ADR-0012: Base Contract Plus Versioned Modules

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Commerce contracts and modules](../specifications/01-commerce-contracts-and-modules.md)\
**Date:** 2026-09-30\

## Context

One universal contract would force every renderer to implement unrelated
features. Fully independent vocabularies would destroy template portability.

## Decision

Studio governs a small commerce base. Integrations compose exact versions of
namespaced modules with explicit dependencies and migrations.

## Consequences

Templates declare requirements precisely and can move between renderers that
implement the same module set. Version graphs and compatibility checks become
first-class.

## Rejected alternatives

- One monolithic universal contract.
- Private platform vocabularies without a shared base.
- Unversioned optional fields.
