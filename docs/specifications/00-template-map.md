# Template Map

**Status:** Authoritative protocol\
**Authority:** Normative within its stated scope\
**Audience:** Core, editor, contract, renderer, SDK\
**Owner:** Map protocol area\
**Related:** [Specifications index](./README.md)\

## Envelope

~~~ts
type TemplateMap = {
  schemaVersion: number;
  contract: {
    base: VersionRef;
    modules: Record<NamespacedModuleId, VersionRef>;
  };
  policyVersionId: string;
  localization: LocalizationConfig;
  tokens: SemanticTokenValues;
  shell: ShellComposition;
  pages: Record<PageKey, PageComposition>;
  sections: Record<SectionId, SectionInstance>;
  seo: SeoDefaults;
};
~~~

Persistence identity, site ID, draft revision, version ID, actor, timestamps,
publication state, signatures, and audit metadata MUST NOT appear in the map.
This makes semantic equality independent of a database row.

## Pages and regions

A page identifies a contract-declared page type and ordered section IDs within
declared regions. Every referenced section exists exactly once in the section
dictionary and is placed according to contract cardinality. A section may
appear in only one location unless its type explicitly supports shared
instances.

## Section

~~~ts
type SectionInstance = {
  id: SectionId;
  type: NamespacedSectionType;
  schemaVersion: number;
  variant: string;
  content: Record<string, LocalizedOrScalarValue>;
  controls: Record<string, JsonValue>;
  bindings: Record<string, BindingReference>;
  actions: Record<string, ActionReference>;
  responsive?: Record<ViewMode, ResponsiveOverride>;
  provenance?: Provenance;
};
~~~

Unknown types, variants, fields, controls, bindings, actions, modes, and
properties are rejected. Section IDs are stable opaque identifiers and never
derived from array position, label, or renderer component name.

## Canonical form

Canonicalization MUST:

1. validate the current schema and pinned contract;
2. normalize strings, locale tags, colors, URLs, and identifiers;
3. omit absent optional properties rather than encoding undefined;
4. sort object keys where order has no semantic meaning;
5. preserve declared arrays where order is meaningful;
6. encode JSON according to RFC 8785 compatible canonical rules; and
7. hash UTF-8 canonical bytes with SHA-256.

Numbers are finite and schema bounded. Assets, rich text, list length, nesting,
and total serialized size have installation-configured upper bounds no weaker
than contract maxima.

## Forbidden content

Maps cannot contain raw HTML, CSS, JavaScript, renderer imports, class names,
arbitrary URLs, secrets, credentials, customer data, operational commerce
facts, executable expressions, or network requests.

## Validation layers

Map-schema validation runs first, contract and module semantics second, policy
constraints third, and site/resource existence last. A published map records
the exact successful versions of all layers.
