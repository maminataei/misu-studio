# Content, Assets, Localization, and SEO

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Product, content design, asset services, renderer developers\
**Owner:** Content platform area\
**Related:** [Product index](./README.md)\

## Content ownership

Presentation headings, banners, stories, FAQ entries, and similar authored
copy live in the map. Catalog descriptions, policies with domain authority,
price, availability, customer, and transaction data remain external bindings.
A field's owner MUST be declared; Studio cannot silently copy an external field
into map ownership.

Rich text uses a limited semantic AST. Scripts, styles, event handlers, raw
HTML, iframes, unknown nodes, unsafe URLs, and unbounded nesting are rejected.

## Localization

A site declares one required default locale and zero or more additional
locales. Every locale declares direction. Localized fields use explicit locale
keys and a declared fallback chain. Missing default-locale content is a
blocker. Missing secondary content is a warning unless policy requires
completeness.

Renderer releases MUST declare supported locales and directions. Changing the
default locale is an explicit command and triggers full readiness.

## Assets

Studio manages a site asset library and may expose external host asset sources.
Maps store stable asset references and semantic variant intent, never expiring
storage URLs. Upload processing validates signatures and limits, removes
unsafe metadata, extracts dimensions, and produces approved derivatives.

Integrations declare an approved font catalog. Authorized users may upload
licensed font assets with family, weight, style, format, and license metadata.
Arbitrary remote font URLs are forbidden.

## SEO

Maps may store localized title and description defaults, social-image asset
references, and page-type overrides. Hosts own canonical URLs, route-specific
metadata, robots policy, live product metadata, and structured commerce data.
Studio MUST label previews as advisory rather than final route output.
