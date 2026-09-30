# Data Binding and Action Model

**Status:** Authoritative protocol  
**Audience:** Contract, renderer, integration, security  
**Owner:** Host interaction area

## Bindings

A binding is a typed semantic request for host-owned read data.

~~~ts
type BindingReference = {
  type: NamespacedBindingType;
  version: number;
  parameters: Record<string, JsonValue>;
  emptyBehavior: DeclaredEmptyBehavior;
};
~~~

Definitions constrain parameters such as selected resource IDs, sort choices,
approved filters, result limits, and merchandising mode. A binding cannot
contain a URL, query language, header, credential, script, or arbitrary field
projection.

The host resolves current eligibility, identity, content, price, availability,
and customer scope. A map selection narrows presentation; it never makes an
ineligible resource public.

## Actions

An action reference configures a host-declared interaction.

~~~ts
type ActionReference = {
  type: NamespacedActionType;
  version: number;
  parameters: Record<string, JsonValue>;
  presentation?: ActionPresentation;
};
~~~

Examples include navigate-semantic-route, open-search, select-option,
add-to-cart, begin-checkout, authenticate, download-entitlement, or
submit-declared-form. The renderer invokes its trusted adapter, which
reauthorizes and revalidates all operational input.

## Links and forms

External links use a dedicated action with approved schemes, target policy,
and rel behavior. Forms are manifest-defined components; Studio may configure
allowed labels, ordering, visibility, and presentation but cannot invent
backend fields or destinations.

## Failures

Binding and action failures map to typed customer-safe states. The renderer
must not infer success, retain stale authoritative values, or substitute a
different resource silently.
