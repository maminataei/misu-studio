# Commerce Pages and Protected Tasks

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Product, contract authors, renderer developers, QA\
**Owner:** Commerce contract area\
**Related:** [Product index](./README.md)\

## Full-journey scope

Contracts may define home, navigation, search, catalog, category, product,
cart, checkout, payment outcome, authentication, account, address, order,
fulfillment, entitlement, wishlist, review, question, ticket, policy, contact,
empty, error, unavailable, and lifecycle page types.

Actual routes belong to the host. Maps refer to semantic page keys only.

## Protected tasks

The base contract MUST preserve:

- navigation, search, and discovery feedback;
- product identity, current price, availability, options, fulfillment meaning,
  quantity, and purchase action;
- cart line identity, authoritative totals, validation, and checkout action;
- checkout identity, required inputs, delivery selection, final review, total,
  and confirmation action;
- truthful payment, order, fulfillment, refund, and entitlement states;
- authentication and customer-rights paths; and
- understandable failure, empty, restricted, and unavailable states.

Modules may add protected tasks but cannot weaken the base.

## Truth boundary

Maps may control composition and treatment. They MUST NOT contain editable
lookalikes for price, discount, stock, tax, shipping, payment success, order
state, delivery state, or entitlement validity. Those values arrive through
typed host bindings and are revalidated by host actions.

## Required and optional regions

Contracts declare page regions, section cardinality, allowed order, and
protected task coverage. Optional sections may be hidden or removed. Required
regions may change approved variant but remain present. Readiness MUST identify
the exact missing customer task, not only a schema path.

## Scenario coverage

Every protected task MUST have privacy-safe fixtures for materially different
states. At minimum this includes unavailable products, option requirements,
empty and changed carts, incomplete checkout, payment outcomes, unauthenticated
accounts, empty order history, restricted access, and renderer failure.
