# ADR-0006: React and Vite Editor

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Editor and preview architecture](../architecture/05-editor-and-preview-architecture.md)\
**Date:** 2026-09-30\

## Context

The editor is a stateful browser application embedded through an iframe.
Server-side rendering adds no product value and would couple deployment layers.

## Decision

Build the editor as a React SPA with Vite. Standalone and embedded use the same
artifact. The iframe boundary provides framework neutrality to hosts.

## Consequences

Editor UI may use React freely while public SDKs and semantic maps remain
framework-neutral. The API and editor can deploy independently.

## Rejected alternatives

- Next.js full-stack editor.
- Native React component embedded in hosts.
- Editor implemented as custom elements.

## References

- [React](https://react.dev/)
- [Vite](https://vite.dev/guide/)
