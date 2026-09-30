# Renderer Ecosystem

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Contract and renderer authors\
**Owner:** Renderer ecosystem area\
**Related:** [Architecture index](./README.md)\

## Separation of artifacts

A commerce contract defines semantic meaning. A renderer release declares an
implementation of exact contract and module versions. A renderer target
configures a deployed release. A semantic map targets the contract, not a
framework package or deployment.

This separation permits React, Vue, server-rendered, native, or other
implementations to consume one map when their conformance evidence covers the
same contract.

## Contract composition

Studio governs a minimal commerce base. Integrations add immutable namespaced
modules for capabilities such as reviews, subscriptions, digital fulfillment,
loyalty, or support. Module dependency graphs MUST be acyclic and pin exact
compatible versions.

## Renderer registration

A renderer release provides a signed declarative manifest, artifact provenance,
contract claims, supported locale directions, view modes, scenario support,
preview/preflight capabilities, and certification report. Registration does
not upload executable code.

## Certification

The conformance kit supplies canonical maps, expected semantic observations,
interaction probes, error fixtures, accessibility assertions, and deterministic
result hashing. A release that omits a declared feature or produces a serious
finding cannot be activated.

Certification proves contract behavior for controlled fixtures; it does not
replace target health or publication preflight.

## Lifecycle

Renderer releases and contracts are immutable. A new release may declare
compatibility with an existing contract without migrating maps. A new contract
version requires explicit map migration. A release cannot be retired while an
active target or retained rollback version depends on it.
