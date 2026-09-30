# Product Charter

**Status:** Authoritative  
**Audience:** All contributors and integrators  
**Owner:** Product maintainers  
**Related:** [System architecture](../architecture/00-system-architecture.md)

## Purpose

Commerce Studio enables a commerce platform to offer merchants a complete,
guarded template builder without coupling the builder to the platform's
frontend framework or operational data model.

Studio authors a semantic map. A host renderer interprets that map and combines
it with live commerce data and actions. Studio never generates a storefront,
executes merchant code, calculates commercial truth, or becomes a checkout
backend.

## Product promise

A platform integrates one versioned commerce contract and one or more
conforming renderers. Its merchants can then create, preview, refine, publish,
and roll back coherent storefront templates across the full customer journey.

## Primary audiences

- Commerce-platform teams integrating Studio for many merchant sites.
- Merchant editors configuring approved templates without source-code access.
- Designers creating starter kits, page templates, and section presets.
- Renderer developers implementing a shared semantic contract.
- Operators deploying and governing a self-hosted installation.

## Goals

Studio MUST:

1. keep maps portable across conforming renderers;
2. provide a complete non-AI authoring workflow;
3. protect required commerce tasks and authoritative live values;
4. publish immutable versions atomically across active targets;
5. support multi-locale, direction-aware, responsive presentation;
6. preserve audit, history, rollback, and tenant isolation;
7. remain self-hostable without a proprietary license service; and
8. make third-party extensions declarative to Studio and executable only in
   host-controlled renderers.

## Non-goals

The beta does not provide a freeform pixel canvas, arbitrary nested application
construction, custom runtime code, a generic form backend, collaborative CRDTs,
offline authoring, source-code generation, managed hosting, AI generation, or a
public marketplace.

## Product boundary

Studio owns authoring intent, presentation content, assets, versions, policies,
readiness evidence, and publication pointers. Hosts own URLs, domain resources,
prices, stock, discounts, delivery, identity, payment, orders, entitlements,
customer information, mutations, and the production renderer.

## Licensing and distribution

Commerce Studio is Apache-2.0 software distributed as source, synchronized
packages under the @commerce-studio scope, and signed OCI deployment artifacts.
It is self-hosted only. Nothing in the core requires outbound telemetry or a
commercial license server.
