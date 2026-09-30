# Governance

**Status:** Active\
**Authority:** Normative project governance policy\
**Audience:** Contributors, maintainers, and users\
**Owner:** Commerce Studio maintainers\
**Related:** [Contributing](./CONTRIBUTING.md)\

## Project model

Commerce Studio is an Apache-2.0 open-source project. Maintainers steward the
repository, releases, security response, compatibility policy, and official
marketplace registry. Governance does not grant a maintainer control over a
self-hosted installation or its data.

## Decision hierarchy

Conflicts are resolved in this order:

1. security policy and published compatibility guarantees;
2. normative product specifications;
3. normative protocol and architecture specifications;
4. accepted ADRs;
5. operations and integration guidance;
6. examples and implementation notes.

Later explicit decisions supersede earlier ones. A superseded ADR remains in
history and links to its replacement.

## Roles

- Maintainers approve releases, governance changes, security fixes, and ADRs.
- Area owners review their product, protocol, security, or operations domain.
- Contributors propose changes and provide acceptance evidence.
- Marketplace publishers control their packages but not Studio policy.

## Change classes

- Editorial changes clarify without changing observable behavior.
- Compatible changes add optional behavior without invalidating existing maps.
- Breaking changes alter a public schema, protocol, invariant, or deployment
  requirement and require a major version or new independently versioned
  contract.

No contributor may merge a breaking change by describing it as editorial.
