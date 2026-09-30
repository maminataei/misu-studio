# Platform Integration Guide

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Commerce-platform engineers\
**Owner:** Integration maintainers\
**Related:** [Integrations index](./README.md)\

## Integration responsibilities

A platform MUST provide:

- a versioned contract composition or adopt existing compatible modules;
- integration policy versions;
- one or more certified renderer releases and deployed targets;
- sandboxed preview and signed preflight endpoints;
- privacy-safe scenario fixtures;
- typed binding and action adapters;
- host-to-Studio identity exchange;
- site provisioning and membership mapping;
- runtime map cache and verification; and
- signed webhook consumption.

Studio provides authoring, assets, history, readiness orchestration, immutable
versions, environment pointers, runtime delivery, and audit.

## Onboarding sequence

1. Create organization and integration.
2. Register contract base/modules and effective composition.
3. Register and activate an integration policy.
4. Build renderer against the manifest SDK.
5. Run the conformance kit and sign the report.
6. Register renderer release and create preview/staging/production targets.
7. Configure allowed origins, service credentials, preflight, and webhooks.
8. Register starter kits and shared templates.
9. Provision a test site and execute the acceptance suite.
10. Enable merchant embed after security review.

## Site provisioning

The host uses a scoped service credential and stable external site reference.
Create is idempotent. The request selects integration, initial policy, locales,
starter kit, environments, target sets, and owner membership. Studio returns
its opaque site ID and embed/runtime references.

## Runtime integration

The host renderer resolves the environment pointer server-side, verifies and
caches the immutable version, then combines it with live domain projections.
The renderer does not call Studio for each customer request. Binding/action
adapters enforce tenant, customer, and commerce authorization independently.

## Production checklist

Validate origin separation, credential rotation, webhook replay handling,
last-known-good persistence, scenario privacy, serious accessibility blockers,
target fail-closed readiness, backup/restore, and complete renderer/module
compatibility before onboarding merchants.
