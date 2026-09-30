# Domain and Tenancy Model

**Status:** Authoritative  
**Audience:** API, persistence, authorization, operations  
**Owner:** Platform architecture area

## Resource hierarchy

~~~mermaid
flowchart TD
  Install[Installation] --> Org[Organization]
  Org --> Members[Memberships]
  Org --> Integration[Integration]
  Integration --> Contract[Contract and modules]
  Integration --> Policy[Policy versions]
  Integration --> Renderer[Renderer releases and targets]
  Integration --> Shared[Shared templates]
  Integration --> Site[Site]
  Site --> Draft[Active draft]
  Site --> Assets[Assets and comments]
  Site --> Versions[Immutable versions]
  Site --> Env[Environments]
  Env --> Targets[Active target set]
  Env --> Pointer[Published version pointer]
~~~

## Installation

An installation owns identity configuration, signing keys, storage, retention,
global limits, and organizations. Installation administrators cannot bypass
audit or map validation. Support impersonation is not a beta capability.

## Organization

An organization is the top authorization and billing-neutral isolation unit.
Membership roles may be narrowed at integration or site level. Deleting an
organization is an asynchronous, explicitly confirmed retention workflow.

## Integration

An integration represents one commerce platform boundary. It owns compatible
contracts, renderer releases, targets, policies, shared templates, host
credentials, allowed preview origins, and site provisioning authority.

## Site

A site is an isolated merchant authoring unit. It owns one active draft,
commands, versions, assets, comments, locale configuration, environment
pointers, and audit scope. A site cannot reference another site's private
assets or content.

## Environment and target

An environment is a named publication channel. Its active target set identifies
renderer deployments that must accept the same version atomically. Targets
have independent service credentials, preview endpoints, preflight endpoints,
webhook subscriptions, and last acknowledged delivery state.

## Referential invariants

Deleting or deactivating a contract, module, policy, renderer release, asset,
or version MUST be blocked while a retained draft, version, environment, or
template references it. Retention operates from reachability, not timestamps
alone.
