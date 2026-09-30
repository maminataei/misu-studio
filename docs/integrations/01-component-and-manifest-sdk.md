# Component and Manifest SDK

**Status:** Authoritative SDK contract\
**Authority:** Normative within its stated scope\
**Audience:** Contract, component, and renderer developers\
**Owner:** SDK maintainers\
**Related:** [Integrations index](./README.md)\

## Purpose

The @commerce-studio/manifest-sdk creates declarative commerce contracts,
modules, renderer release manifests, policies, and fixtures. It does not render
components or load application code.

## Authoring model

~~~ts
const productGrid = defineSection({
  type: "example.catalog.product-grid",
  version: 1,
  allowedPages: ["catalog", "category", "home"],
  variants: ["cards", "compact-list"],
  content: { heading: localizedText({ maxLength: 120 }) },
  bindings: {
    products: bindingSlot("commerce.product-collection", { required: true })
  },
  actions: {
    product: actionSlot("commerce.navigate-product")
  },
  controls: {
    density: enumControl(["comfortable", "compact"])
  },
  protectedTasks: ["discovery.results", "discovery.empty-feedback"]
});
~~~

SDK builders produce plain validated JSON and inferred TypeScript types.
Machine IDs are explicit, namespaced, and stable. Labels, descriptions, and
help text are localizable metadata.

## Validation

The SDK rejects unbounded schemas, executable callbacks, arbitrary JSON Schema
extensions, unsafe URL fields, cyclic module dependencies, unknown control
types, undeclared bindings/actions, and attempts to override base semantics.

Only Studio-owned schemas are compiled. A generated manifest is portable to
other languages through published JSON Schema.

## Renderer-side mapping

Renderer packages maintain their own mapping from semantic section/action/
binding keys to implementation code. That mapping is not uploaded to Studio.
The package exposes conformance hooks that render controlled fixtures and
report semantic observations.

## Release

The CLI canonicalizes and hashes manifests, runs schema and compatibility
checks, executes conformance, creates provenance, and signs release metadata.
Changing any semantic field requires a new immutable version.
