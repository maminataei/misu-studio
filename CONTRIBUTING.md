# Contributing to Commerce Studio

## Authority

This guide governs contributions to this repository. Normative product and
technical documents take precedence over examples and issue discussion.

## Contribution workflow

1. Read the relevant product requirement, technical specification, and ADR.
2. Open or reference an issue that states the customer outcome and affected
   invariant.
3. For a breaking or architectural change, update the governing document and
   add or supersede an ADR before implementation.
4. Keep commits focused and include tests or acceptance evidence appropriate to
   the change.
5. Run formatting, type, unit, integration, security, and documentation checks.
6. Request review from the documented owner of every affected authority area.

## Normative language

The words MUST, MUST NOT, SHOULD, SHOULD NOT, and MAY are interpreted as
normative requirements. A proposal cannot weaken a MUST by changing only an
implementation note or example.

## Compatibility

Published map schemas, commerce contracts, module versions, renderer manifests,
and public APIs are compatibility surfaces. A breaking change MUST include a
new version, migration, conformance fixtures, rollout notes, and rollback
evidence.

## Security

Do not include credentials, customer information, private prompts, or real
commerce data in issues, fixtures, traces, or commits. Report vulnerabilities
through [SECURITY.md](./SECURITY.md), not a public issue.

## Documentation quality

Documentation changes MUST keep relative links valid, use terminology from the
glossary, identify authority and audience, and avoid unresolved placeholders.
Mermaid diagrams MUST reflect the surrounding normative text; diagrams are not
an independent source of truth.
