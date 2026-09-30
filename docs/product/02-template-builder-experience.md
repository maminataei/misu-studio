# Template-Builder Experience

**Status:** Authoritative  
**Audience:** Product design, editor engineering, accessibility, QA  
**Owner:** Editor product area

## Model

Studio is a structured template builder. It exposes the semantic vocabulary
declared by the site's pinned contract and policy. It is not a document-object
model inspector and does not expose renderer implementation details.

## Workspace

The workspace MUST provide:

- page, scenario, locale, semantic view-mode, and renderer-target selectors;
- a searchable outline showing regions and section order;
- a sandboxed live preview with selectable section boundaries;
- a declarative inspector for content, variants, controls, bindings, actions,
  visibility, and local token overrides;
- global design-token and asset surfaces;
- synchronized status, history, comments, readiness, and publication access;
- keyboard-operable alternatives to every drag operation; and
- clear distinction between draft, environment versions, and unsynchronized
  local intent.

## Allowed operations

Subject to contract and policy, an editor MAY add, remove, reorder, duplicate,
show, hide, and change approved section variants. An editor MAY edit map-owned
content, choose assets, configure typed bindings and actions, apply semantic
tokens, and set supported differences by view mode.

Studio MUST explain why an operation is forbidden and identify a supported
alternative when one exists. Required sections and customer tasks cannot be
removed or visually disabled.

## Inspector controls

Renderer manifests compose Studio-owned control types: text, rich text,
number-with-range, select, toggle, color/token reference, asset, binding,
action, localized field, ordered list, and conditional group. Plugin-provided
native UI does not execute inside Studio.

## Responsive editing

Contracts declare semantic modes such as compact, regular, and wide. Renderers
map modes to their own layout rules. Maps MUST NOT contain pixel breakpoint
definitions. A contract may permit per-mode visibility, order, density, media
treatment, or variant changes, but required commerce information must remain
available in every supported mode.

## Saving and connectivity

Commands apply optimistically in the browser and autosave immediately.
Pending, acknowledged, rejected, retrying, and lease-lost states MUST be
visible. If connectivity is lost, Studio retains unacknowledged commands for
recovery but disables further mutations until the server revision and lease
are reconciled.

## Device support

Full editing targets current desktop browsers and suitable landscape tablets.
Phones MAY support preview, comments, status, and approval but are not required
to support structural editing.
