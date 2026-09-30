# ADR-0002: Semantic Maps, Not Generated Websites

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Template-map specification](../specifications/00-template-map.md)\
**Date:** 2026-09-30\

## Context

Code or HTML generation makes round-trip editing, live data safety, framework
portability, and migration difficult. Studio's purpose is to describe approved
presentation intent for different renderers.

## Decision

The canonical output is strict, versioned, renderer-independent JSON. Studio
does not generate application source, host production HTML, or own storefront
rendering. Host renderers interpret maps and resolve live data and actions.

## Consequences

The map vocabulary must remain semantic and constrained. Production output can
differ in implementation while conformance preserves meaning. Code export is
not a beta capability.

## Rejected alternatives

- Generated React or Next.js source.
- Static HTML/CSS export.
- Studio-hosted storefront runtime.
