# Integration Policy

**Status:** Authoritative protocol\
**Authority:** Normative within its stated scope\
**Audience:** Platform integrators, editor, validation, publication\
**Owner:** Integration policy area\
**Related:** [Specifications index](./README.md)\

## Purpose

A policy narrows an effective commerce contract for one platform. It cannot add
undeclared semantics or weaken protected tasks.

~~~ts
type IntegrationPolicy = {
  id: string;
  version: number;
  contractHash: string;
  sections: {
    allow?: string[];
    deny?: string[];
    required: RequiredPlacement[];
  };
  controls: Record<FieldPath, ControlConstraint>;
  tokens: Record<TokenKey, TokenConstraint>;
  assets: AssetPolicy;
  localization: LocalizationPolicy;
  publication: PublicationPolicy;
  limits: ResourceLimits;
};
~~~

## Layering

The effective permission is the intersection of contract support, renderer
support, integration policy, site role, and current resource state. A lower
layer cannot re-enable an item denied by a higher layer.

Policies may provide defaults, bounds, allowed values, locks, required
placements, asset-source permissions, locale completeness, approval rules,
warning rules, and active-target requirements.

## Upgrades

A policy version is immutable. A site draft pins one version. Upgrade runs a
dry validation and any declared normalization commands, shows the resulting
changes and new findings, then requires an editor to accept. Published versions
remain bound to the prior policy evidence.

## Invalid policy

Registration rejects a policy that removes a protected task, creates
contradictory cardinality, sets an invalid default, expands beyond the
contract, references missing modules, or exceeds installation security limits.
