# Beta Scope and Exit Gates

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Product, engineering, QA, release\
**Owner:** Delivery maintainers\
**Related:** [Delivery index](./README.md)\

## Included

- Self-hosted organization/integration/site platform.
- Local and OIDC identity plus embedded sessions.
- Base commerce contract and Misu-required modules.
- Complete template builder with maps, templates, assets, localization,
  responsive modes, typed bindings/actions, history, comments, and leases.
- Host preview, conformance, readiness, approval, multi-target publication,
  rollback, runtime API, signed webhooks, bundles, Compose, and Helm.
- Misu and independent reference renderer.

## Excluded

AI, public marketplace UI/registry, CRDT multiplayer, offline editing, managed
cloud, freeform layouts, custom code, generic forms, code export, analytics-
driven optimization, and mobile structural authoring.

## Exit gates

| Gate | Evidence |
| --- | --- |
| Product completeness | Full merchant journey from starter kit through rollback |
| Portability | Identical map passes Misu and reference conformance |
| Safety | Protected tasks and live truth cannot be removed or forged |
| Security | Threat-mapped suites and independent review findings resolved |
| Accessibility | Editor and required rendered scenarios meet blocker policy |
| Durability | Command, publish, restore, rollback, backup/restore chaos tests |
| Operations | Compose and Helm clean install, upgrade, and recovery |
| Performance | Published capacity targets met with representative data |
| Compatibility | Migration fixtures cover every persisted prerelease version |
| Cleanup | Misu legacy Appearance authority removed |

No beta label is granted with waived blockers. A gate may document an accepted
warning only where the governing specification classifies it as non-blocking.
