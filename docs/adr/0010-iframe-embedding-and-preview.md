# ADR-0010: Iframe Embedding and Preview

**Status:** Accepted  
**Date:** 2026-09-30

## Context

Host platforms use different frontend frameworks and dependency versions.
Preview code is host-controlled and must not share the editor's execution
context.

## Decision

Embed the editor and host preview through origin-restricted sandboxed iframes.
Use a framework-neutral web SDK and versioned MessageChannel protocol with
ephemeral scoped grants.

## Consequences

Hosts avoid React dependency conflicts and untrusted renderer code does not
execute in Studio's origin. Cross-frame selection and drag behavior require an
explicit geometry protocol.

## Rejected alternatives

- React component embedding.
- Direct plugin code loading.
- Generic Studio mock preview.
