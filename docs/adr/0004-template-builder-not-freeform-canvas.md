# ADR-0004: Guarded Template Builder

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Template-builder experience](../product/02-template-builder-experience.md)\
**Date:** 2026-09-30\

## Context

Freeform layout and application builders require arbitrary nesting, logic,
responsive constraints, and code-like behavior that conflict with portable
commerce semantics and protected customer tasks.

## Decision

Studio is a template builder. Users arrange and configure approved sections
within declared regions. Styling uses semantic tokens and declared controls.
Contracts and policies limit operations.

## Consequences

The editor can be complete and powerful without exposing raw layout internals.
Absolute positioning, arbitrary DOM trees, custom code, and generic workflow
construction remain outside the beta.

## Rejected alternatives

- Webflow-style pixel canvas.
- Section toggles without drag-and-drop or deep configuration.
- General application builder.
