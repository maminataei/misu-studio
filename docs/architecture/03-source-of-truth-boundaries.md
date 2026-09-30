# Source-of-Truth Boundaries

**Status:** Authoritative  
**Audience:** Product, platform, renderer, security  
**Owner:** Architecture maintainers

| Concern | Authority | Version behavior |
| --- | --- | --- |
| Map structure, tokens, map-owned copy | Studio map | Immutable per version |
| Contract vocabulary and rules | Contract/module artifacts | Immutable and pinned |
| Allowed merchant surface | Integration policy | Immutable and pinned |
| Routes and URLs | Host platform | Resolved live |
| Catalog identity and descriptions | Host domain or typed binding | Resolved live |
| Price, stock, discounts, tax, delivery | Host commerce services | Resolved and revalidated live |
| Customer, cart, order, entitlement | Host customer/commerce services | Scoped and resolved live |
| Component markup and behavior | Host renderer release | Deployment controlled |
| Drafts, history, versions, readiness | Studio control plane | Audited and site scoped |
| Studio-managed asset objects | Studio storage adapter | Immutable object by digest |
| External assets | Host asset adapter | Stable external reference |
| Authentication | Studio identity or trusted host exchange | Session scoped |
| Authorization and publication | Studio RBAC and policy | Rechecked at action time |

## Composition rule

A renderer receives a signed map and obtains live host projections through its
own trusted services. Studio does not proxy production commerce data. The map
may select or filter through typed binding parameters, but the host decides
what resources are eligible and what actions succeed.

## Restore rule

Restoring a Studio version restores only presentation and map-owned content.
It never restores catalog, inventory, price, customer, order, or entitlement
state. An external resource missing at render time follows the binding's
declared empty or unavailable behavior.

## Preview rule

Preview fixtures are deterministic examples, not authorities. They contain no
real customer records and cannot be reused as production responses.
