# Editor and Preview Architecture

**Status:** Authoritative  
**Audience:** Editor, SDK, renderer, and security engineers  
**Owner:** Editor architecture area

## Editor state

The editor keeps four explicit layers:

1. authoritative acknowledged draft and revision;
2. at most one optimistic pending command chain;
3. UI-only selection, panels, viewport, and target state; and
4. server events for lease, presence, jobs, comments, and invalidation.

The core command engine derives optimistic state. Rejection discards dependent
optimistic state and reconciles from the authoritative server result.

## Preview handshake

~~~mermaid
sequenceDiagram
  participant E as Studio editor
  participant P as Host preview
  participant A as Studio API
  E->>P: load allowlisted sandbox URL
  P->>E: hello(protocol, nonce, origin)
  E->>A: request preview grant(target, draft, revision)
  A-->>E: short-lived read grant
  E->>P: MessageChannel + grant + selection context
  P->>A: fetch validated preview payload
  A-->>P: map, fixtures, asset capabilities
  P-->>E: ready(render hash)
  P-->>E: bounds, selection, diagnostics
  E-->>P: page/scenario/locale/mode/selection changes
~~~

The editor verifies origin, protocol range, nonce, target, and render hash.
The grant is single-purpose, short-lived, audience-bound, and cannot mutate.
Preview navigation cannot escape the sandbox or replace the parent page.

## Selection

Preview renderers annotate semantic section IDs and report geometry rather than
exposing a component tree. Studio draws selection and drag affordances in its
own overlay. Reordering is also available in the outline so iframe pointer
behavior is not the only path.

## Multi-target preview

Switching targets preserves semantic page, scenario, locale, view mode, and
selection when supported. Unsupported context is explained and does not mutate
the map. Differences are renderer diagnostics, not automatically rewritten map
content.

## Accessibility

The editor itself meets WCAG 2.2 AA goals. Preview accessibility checks inspect
rendered target output across required scenarios. Critical and serious
findings block publication; lesser findings are acknowledged warnings.
