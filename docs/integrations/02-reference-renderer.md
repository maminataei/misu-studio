# Reference Renderer

**Status:** Authoritative beta proof\
**Authority:** Normative within its stated scope\
**Audience:** Renderer developers, QA, maintainers\
**Owner:** Reference integration area\
**Related:** [Integrations index](./README.md)\

## Purpose

The reference renderer proves that contracts and maps are not accidentally
coupled to Misu, React, Next.js, Persian, or one commerce model. It is a
conformance and documentation example, not a production storefront product.

## Technology

The initial reference uses Vue and Vite, a deterministic in-memory commerce
adapter, and the public JSON Schema/OpenAPI artifacts. It MUST NOT import
Studio's React editor, Misu packages, or private control-plane modules.

## Coverage

It implements the complete base commerce contract and the minimum module set
shared with the beta Misu map. It supplies:

- LTR and RTL locales;
- compact, regular, and wide modes;
- every protected customer-journey scenario;
- preview annotations and MessageChannel adapter;
- typed binding/action simulations;
- signed host preflight; and
- runtime pointer fetch, signature verification, caching, and fallback.

## Fixture storefront

The example catalog includes physical, digital, and hybrid products, options,
discounted and unavailable states, carts and checkout conditions, payment
outcomes, orders, entitlements, reviews, questions, wishlist, and support.
All identities are synthetic and stable.

## Acceptance role

The same canonical map and scenario inputs used by Misu must pass reference
conformance. A change that succeeds only in Misu does not satisfy beta
portability.
