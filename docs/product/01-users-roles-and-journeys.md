# Users, Roles, and Journeys

**Status:** Authoritative  
**Audience:** Product, UX, API, authorization, QA  
**Owner:** Product maintainers

## Actors

- An installation administrator configures identity, storage, signing, and
  organization creation.
- An organization administrator manages members and integrations.
- A platform integrator registers contracts, policies, targets, and templates.
- A merchant viewer inspects drafts, versions, comments, and readiness.
- A merchant editor holds the lease and modifies the active draft.
- A publisher approves and promotes an exact version.
- A renderer service fetches signed maps using scoped service credentials.

## Roles

The standard roles are viewer, editor, publisher, and administrator.
Permissions are additive and scoped to organization, integration, or site.
A viewer MAY comment. An editor MUST NOT publish unless also granted publisher
authority. An administrator MAY configure whether production requires an
approver different from the last editor.

## Integration journey

The platform team registers a base-contract version, selected modules, an
integration policy, privacy-safe preview scenarios, and renderer releases. Each
release passes conformance before it can become a target. The platform then
creates sites or authorizes its backend to create them through scoped APIs.

## Merchant creation journey

1. The host exchanges its authenticated merchant identity for a short-lived
   embedded Studio session.
2. The merchant opens a site and selects a compatible starter kit.
3. Studio copies the kit, records provenance, validates policy, and creates the
   active draft.
4. The editor acquires a lease and works through the outline, canvas, and
   inspector.
5. Every change autosaves as a typed command.
6. The merchant previews declared pages, scenarios, locales, view modes, and
   renderer targets.
7. Readiness identifies blockers and warnings before publication.

## Publication journey

An authorized publisher selects an environment and exact draft revision.
Studio runs structural, contract, policy, accessibility, and target preflight
checks. Required warnings are acknowledged. If approval policy requires a
second person, the request waits without changing the environment. Successful
publication creates one immutable version and atomically advances the entire
target set.

## Recovery journeys

- Undo applies inverse data as a new command.
- Restore copies a prior immutable version into the active draft.
- Rollback changes an environment pointer to a prior compatible version.
- Lease takeover invalidates the previous fencing token.
- A disconnected editor stops accepting new mutations until reconciliation.
- A renderer outage leaves the old environment version authoritative.
