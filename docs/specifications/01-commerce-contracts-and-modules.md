# Commerce Contracts and Modules

**Status:** Authoritative protocol  
**Audience:** Contract authors, renderer developers, integrators  
**Owner:** Contract protocol area

## Contract contents

A contract version declares semantic page types, regions, section schemas,
variants, controls, binding and action slots, view modes, scenario definitions,
protected tasks, required-state rules, and migrations from its predecessor.

The base contract provides universal commerce semantics. A module uses a
globally namespaced ID, exact version, declared dependencies, and no ability to
override a base definition.

~~~ts
type CommerceContract = {
  id: string;
  version: string;
  mapSchemaRange: string;
  dependencies: VersionRef[];
  pageTypes: PageTypeDefinition[];
  sections: SectionDefinition[];
  bindings: BindingDefinition[];
  actions: ActionDefinition[];
  scenarios: ScenarioDefinition[];
  viewModes: ViewModeDefinition[];
  invariants: InvariantDefinition[];
  migrations: MigrationDescriptor[];
};
~~~

## Composition

Composition sorts a dependency graph, rejects cycles and duplicate ownership,
checks exact compatibility, and produces one canonical effective contract
hash. Two maps are contract-compatible only when their effective contract
identity matches or a registered migration establishes compatibility.

## Definition rules

Every field has a stable machine key, bounded schema, ownership, localization
behavior, default semantics, editor control, and renderer expectation.
Human labels are localized metadata and cannot become identifiers.

Protected tasks identify required semantic outcomes such as current total or
purchase action. A renderer may choose markup and layout but must expose the
declared task under every required scenario and mode.

## Evolution

Published versions are immutable. Compatible additions require a new minor
contract version; meaning changes, removal, stricter required behavior, or
wire incompatibility require a major version and migration. Contracts do not
use floating dependency ranges inside a published effective composition.

## Ownership

Studio maintainers govern the base. Integration or ecosystem publishers govern
modules within their namespace. Registration verifies namespace authority,
signatures, dependency closure, schema safety, and migration completeness.
