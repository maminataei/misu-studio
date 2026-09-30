# ADR-0007: Fastify and OpenAPI Control Plane

**Status:** Accepted  
**Date:** 2026-09-30

## Context

The control plane needs explicit modules, high-quality HTTP behavior,
schema-first validation, streaming SSE, and language-neutral clients without a
decorator-heavy framework.

## Decision

Use Fastify with trusted TypeBox schemas and generate OpenAPI 3.1. Uploaded
manifests are validated data and are never compiled as route validators.

## Consequences

The API stays close to web standards and shares schema artifacts with SDKs.
Application and repository boundaries must be established by project
convention rather than a large framework.

## Rejected alternatives

- NestJS.
- Hono, due to a smaller long-running server ecosystem.
- Effect HTTP, due to a higher contributor learning cost.

## References

- [Fastify validation and serialization](https://fastify.dev/docs/latest/Reference/Validation-and-Serialization/)
- [OpenAPI 3.1](https://spec.openapis.org/oas/v3.1.0)
