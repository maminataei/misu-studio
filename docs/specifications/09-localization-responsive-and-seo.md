# Localization, Responsive Behavior, and SEO

**Status:** Authoritative protocol\
**Authority:** Normative within its stated scope\
**Audience:** Core, editor, renderer, content, QA\
**Owner:** Presentation semantics area\
**Related:** [Specifications index](./README.md)\

## Locale configuration

Locale tags use normalized BCP 47 form. Configuration declares default locale,
supported locales, direction, and acyclic fallback order. The contract marks
which fields are localized and whether blank is meaningful.

Default-locale required content MUST be present. A policy may require complete
translations. Otherwise a missing secondary value resolves through the
declared chain and produces a readiness warning.

## Rich text direction

Direction is locale-level unless a rich-text node explicitly declares
bidirectional isolation for content such as identifiers. Renderers preserve
semantic reading and focus order. Layout mirroring cannot reverse ordered data
whose meaning is direction-independent.

## View modes

Contracts define named modes and ordering, not pixels. Renderer releases map
each supported mode to their layout system and preview viewport. Overrides may
select declared variants, visibility, order, alignment, density, or media
treatment. Required tasks remain present.

## SEO

Maps store localized semantic values:

- default title pattern and description;
- page-type title/description overrides;
- social image asset intent; and
- indexability preference where the host permits it.

The host resolves routes, canonical URLs, robots, alternates, live resource
names, social URLs, and structured commerce data. Host values that are
operational or route-specific take precedence. Preview shows the resolved
sample and the ownership of each field.
