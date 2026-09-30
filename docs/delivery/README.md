# Delivery

**Status:** Authoritative implementation plan\
**Authority:** Normative within its stated scope\
**Audience:** Engineering, QA, release, operations\
**Owner:** Delivery maintainers\
**Related:** [Documentation index](../README.md)\

1. [Implementation roadmap](./00-implementation-roadmap.md)
2. [Beta scope and gates](./01-beta-scope-and-exit-gates.md)
3. [Testing strategy](./02-testing-strategy.md)
4. [Performance and capacity](./03-performance-and-capacity.md)
5. [Release and compatibility](./04-release-versioning-and-compatibility.md)

## Requirement traceability

This matrix is the release-audit entry point. Every implementation change MUST
preserve the linked product outcome, architecture boundary, protocol, test
evidence, and delivery phase.

| Product requirement | Architecture and protocol | Verification | Roadmap |
| --- | --- | --- | --- |
| [Portable semantic maps](../product/00-product-charter.md) | [Renderer ecosystem](../architecture/06-renderer-ecosystem.md), [map](../specifications/00-template-map.md), and [conformance](../specifications/06-renderer-conformance-protocol.md) | [Determinism and conformance](./02-testing-strategy.md) | [Phases 0, 1, and 5](./00-implementation-roadmap.md) |
| [Protected full commerce journey](../product/03-commerce-pages-and-protected-tasks.md) | [Truth boundaries](../architecture/03-source-of-truth-boundaries.md) and [bindings/actions](../specifications/07-data-binding-and-action-model.md) | [Full commerce journey](./02-testing-strategy.md) | [Phases 1, 3, and 5](./00-implementation-roadmap.md) |
| [Guarded editing and collaboration](../product/06-collaboration-history-and-publication.md) | [Editor architecture](../architecture/05-editor-and-preview-architecture.md) and [commands](../specifications/04-command-and-changeset-protocol.md) | [Commands and concurrency](./02-testing-strategy.md) | [Phases 2 and 3](./00-implementation-roadmap.md) |
| [Assets, localization, responsive modes, and SEO](../product/04-content-assets-localization-and-seo.md) | [Asset protocol](../specifications/08-assets-fonts-and-media.md) and [presentation semantics](../specifications/09-localization-responsive-and-seo.md) | [Journey and security suites](./02-testing-strategy.md) | [Phases 1 and 3](./00-implementation-roadmap.md) |
| [Tenant-safe identity and roles](../product/01-users-roles-and-journeys.md) | [Tenancy](../architecture/02-domain-and-tenancy-model.md), [authentication](../security/01-authentication-sessions-and-embedding.md), and [authorization](../security/02-authorization-tenancy-and-rls.md) | [Security suites](./02-testing-strategy.md) | [Phase 2](./00-implementation-roadmap.md) |
| [Atomic publication and rollback](../product/06-collaboration-history-and-publication.md) | [Publication](../specifications/10-readiness-approval-and-publication.md) and [runtime delivery](../specifications/11-runtime-map-delivery-and-webhooks.md) | [Publication and runtime](./02-testing-strategy.md) | [Phase 4](./00-implementation-roadmap.md) |
| [Self-hosted operation](../product/00-product-charter.md) | [Deployment topology](../architecture/09-deployment-topology.md) and [operations](../operations/README.md) | [Deployment and recovery suites](./02-testing-strategy.md) | [Phase 6](./00-implementation-roadmap.md) |
| [Misu plus independent renderer proof](../product/08-success-metrics-and-acceptance.md) | [Reference renderer](../integrations/02-reference-renderer.md) and [Misu integration](../integrations/03-misu-integration.md) | [Beta exit gates](./01-beta-scope-and-exit-gates.md) | [Phase 5](./00-implementation-roadmap.md) |
| [Post-beta AI and marketplace](../product/07-marketplace-and-ai-evolution.md) | [Supply-chain trust](../security/04-supply-chain-and-plugin-trust.md) and [package authoring](../integrations/05-marketplace-package-authoring.md) | [Security suites](./02-testing-strategy.md) | [Later phases](./00-implementation-roadmap.md) |
