# Templates, Presets, and Design Policies

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Designers, platform integrators, editor engineering\
**Owner:** Template ecosystem area\
**Related:** [Product index](./README.md)\

## Artifact types

- A starter kit contains a complete site map.
- A page template contains one compatible page composition.
- A section preset contains one section instance and its owned content.

Each artifact pins map schema, contract modules, policy compatibility, locale
requirements, asset references, author, license, and source version.

## Application

Applying an artifact copies validated content into the active draft and records
provenance. The copy becomes independently editable. Later source updates MUST
NOT alter a site automatically. Reapplication is a new explicit command, not
an implicit merge.

An incompatible artifact may be migrated only through registered pure
migrations. Unsupported section types, modules, controls, bindings, actions,
or locales block application.

## Layered policy

An integration policy controls available components, required regions, locked
values, default tokens, control ranges, permitted asset sources, locale rules,
approval requirements, and target requirements. A site may customize only the
remaining surface.

Policies are immutable and versioned. Existing published versions remain
unchanged when a new policy appears. Draft adoption is explicit, migrates and
validates the map, and requires preview before publication.

## Design tokens

Maps use semantic color, typography, spacing-density, shape, emphasis, media,
and interaction tokens. Policies may lock or constrain values. Section
overrides use only controls declared by the contract; raw CSS and framework
classes are never stored.
