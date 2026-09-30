# Glossary

**Status:** Authoritative\
**Authority:** Normative terminology for all Commerce Studio documents\
**Audience:** All contributors, integrators, and operators\
**Owner:** Commerce Studio maintainers\
**Related:** [Documentation index](./README.md)\

| Term | Meaning |
| --- | --- |
| Commerce Studio | The self-hosted authoring and publication control plane. |
| Semantic map | Renderer-independent, canonical JSON describing presentation intent. |
| Commerce contract | Versioned vocabulary of page types, sections, bindings, actions, scenarios, and invariants. |
| Base contract | Universal commerce capabilities governed by Studio. |
| Contract module | Namespaced optional vocabulary such as reviews or digital entitlements. |
| Renderer | Host-deployed implementation that interprets a semantic map. |
| Renderer release | Immutable implementation declaration for exact contract versions. |
| Renderer target | A configured deployment that previews and consumes maps. |
| Conformance | Automated proof that a renderer implements its declared contract. |
| Integration | A commerce platform's contracts, policies, renderer releases, and shared templates. |
| Integration policy | Versioned limits and defaults imposed on sites by a platform. |
| Site | Isolated merchant-owned authoring unit under an integration. |
| Environment | Named publication channel such as preview, staging, or production. |
| Draft | The one mutable semantic map for a site. |
| Version | Immutable signed snapshot created from an exact draft revision. |
| Command | Typed semantic mutation applied to a draft. |
| Changeset | Durable command result with summary, inverse data, and affected paths. |
| Lease | Exclusive, fenced permission to modify a draft. |
| Binding | Typed reference resolved by a host to current commerce data. |
| Action | Typed interaction executed by the host, such as add-to-cart. |
| Scenario | Privacy-safe representative state used by preview and conformance. |
| View mode | Semantic responsive context such as compact, regular, or wide. |
| Readiness | Evidence that a precise draft may be published safely. |
| Host preflight | Signed renderer-target validation of a precise map hash. |
| Starter kit | Full-site template copied into a site with provenance. |
| Preset | Reusable page or section template copied with provenance. |
| Last known good | Most recent verified map retained by a renderer during outages. |
