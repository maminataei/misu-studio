# Misu Integration

**Status:** Authoritative integration specification  
**Audience:** Misu and Commerce Studio implementers  
**Owner:** Misu integration area

## Purpose

Misu is the first full commerce-platform integration and real beta consumer.
Studio remains independent: it imports no Misu code, connects to no Misu
database, and knows no Misu tenancy or commerce entities beyond declared
semantic contracts.

## Resource mapping

- One Misu deployment maps to a Studio organization and integration.
- One Misu store maps to an isolated Studio site through a stable external ref.
- Misu merchant membership maps to scoped viewer/editor/publisher/admin
  capabilities during embedded-session exchange.
- Misu environments configure preview, staging, and production renderer
  targets.

## Contract modules

Misu registers base commerce plus catalog, variants, physical/digital/hybrid
fulfillment, cart, checkout, payment outcomes, accounts, addresses, orders,
entitlements, reviews, Q&A, wishlist, support tickets, policy, and lifecycle
modules. Protected values and actions resolve through Misu's existing domain
services.

## Editor integration

The dashboard Appearance route becomes an iframe host for Studio. Misu's
backend authenticates the merchant, resolves store membership and capabilities,
requests a short-lived site-scoped grant, and renders the web SDK host. Studio
never receives the Misu merchant cookie or broad Misu API credential.

## Preview

Misu exposes a separate preview origin and adapter. It renders the selected map
against deterministic fixtures for every required route and state. Fixtures
contain no real merchant customer, order, payment, or entitlement data.

## Production renderer

Misu's storefront process fetches and verifies the published map server-side,
caches by version, and listens for signed publication events. Route resolution
remains Misu-owned. Page construction combines the map with current,
authorized Misu projections; mutations continue through existing Misu APIs.

## Clean replacement

There are no real merchants, so no compatibility migration or dual-renderer
period is required. After end-to-end acceptance:

- remove the current Appearance editor and client;
- remove platform/admin theme catalog and theme-change endpoints;
- remove the mutable theme-view endpoint and fixed theme shell;
- remove obsolete Theme and ThemeVersion persistence;
- remove only appearance-related StoreSetting fields and contracts;
- preserve operational StoreSetting fields and domain-owned store identity;
- update onboarding to provision a Studio site and apply a starter kit; and
- reseed development data against Studio.

The Misu repository keeps a concise adapter specification and pinned Studio
version. This repository remains authoritative for Studio behavior.

## Exit gate

Misu passes every full-journey scenario, cross-store isolation, embed security,
map cache outage, publication, rollback, accessibility, RTL, and reference-
renderer parity test before legacy removal merges.
