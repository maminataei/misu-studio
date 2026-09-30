# Implementation Roadmap

**Status:** Authoritative delivery sequence  
**Audience:** Engineering and program leadership  
**Owner:** Delivery maintainers

Each phase exits only with its tests, documentation, and migration evidence.
Slices should remain vertically demonstrable; unfinished later features do not
weaken earlier invariants.

## Phase 0: Repository and protocol proof

- Establish pnpm/Turborepo, strict TypeScript, lint, tests, release tooling,
  security policy, and generated-artifact drift gates.
- Implement a minimal map, canonicalizer, one contract, and one command.
- Render the same hand-authored map in two tiny implementations and prove equal
  semantic observations.
- Exit: no Misu or React type appears in map artifacts.

## Phase 1: Core and SDK

- Implement schemas, canonical JSON, hashes, rich text, contracts/modules,
  policies, typed commands, inverses, migrations, templates, findings, and
  fixture packs.
- Implement manifest SDK, CLI validation, JSON Schema publication, and golden
  cross-runtime tests.
- Exit: deterministic command and migration suites are complete.

## Phase 2: Control plane

- Implement Fastify modules, OpenAPI, PostgreSQL/Kysely migrations, RLS,
  organization/integration/site hierarchy, Better Auth, RBAC, embed exchange,
  service credentials, audit, leases, drafts, history, comments, and SSE.
- Implement assets, Graphile Worker, retention, and site bundles.
- Exit: tenant, concurrency, security, and backup tests pass.

## Phase 3: Editor and preview

- Implement React/Vite shell, outline, canvas overlay, inspector, token and
  asset surfaces, bindings/actions, localization, modes, target switching,
  autosave, history, comments, and accessibility.
- Implement iframe web SDK and preview protocol.
- Exit: editor E2E covers the full manual workflow without AI.

## Phase 4: Conformance and publication

- Implement certification CLI, release registration, target configuration,
  readiness orchestration, accessibility audit, signed preflight, approvals,
  immutable versions, environment publication, rollback, runtime delivery,
  signatures, webhooks, and last-known-good guidance.
- Exit: retries and failures cannot partially publish.

## Phase 5: Reference and Misu

- Complete the Vue reference renderer and fake commerce adapter.
- Register Misu contracts, policies, fixtures, previews, renderer, identity
  exchange, runtime cache, and webhooks.
- Pass one-map cross-renderer acceptance, then remove Misu legacy Appearance.
- Exit: all customer journeys and failure states pass in both renderers.

## Phase 6: Beta hardening

- Complete Compose, Helm, SBOM/provenance/signing, observability, runbooks,
  capacity testing, browser matrix, upgrade/restore drills, and synchronized
  prerelease packages.
- Exit: every beta gate is evidenced in a release candidate.

## Later phases

Add AI command proposals only after core reliability. Add the central
marketplace only after private signed-package workflows are proven.
