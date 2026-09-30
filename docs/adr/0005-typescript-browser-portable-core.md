# ADR-0005: TypeScript Browser-Portable Core

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Package boundaries](../architecture/01-repository-and-package-boundaries.md)\
**Date:** 2026-09-30\

## Context

Schemas, commands, optimistic edits, migrations, and hashes must behave
identically in the browser, CLI, tests, and server. Separate language
implementations would create parity risk at the most important boundary.

## Decision

The canonical core is strict ESM TypeScript with no framework or runtime
dependencies. It publishes JSON Schema for other languages.

## Consequences

Browser and server reuse the same executable semantics. TypeScript does not
dictate renderer framework or host backend language.

## Rejected alternatives

- Python core duplicated in TypeScript for the browser.
- Rust/WASM core, due to contributor and toolchain complexity.
- Server-only command application with weak optimistic behavior.

## References

- [TypeScript](https://www.typescriptlang.org/docs/)
