# ADR-0017: Self-Hosted-Only Deployment

**Status:** Accepted\
**Authority:** Normative architectural decision\
**Audience:** Contributors, reviewers, and implementers\
**Owner:** Architecture maintainers\
**Related:** [Self-hosting requirements](../operations/00-self-hosting-requirements.md)\
**Date:** 2026-09-30\

## Context

The product is intended for commerce platforms that own their data,
integrations, renderer deployments, and operational controls.

## Decision

The project supplies self-hosted artifacts and no managed Studio SaaS. A
separate public registry may distribute signed marketplace metadata and
packages, but it stores no merchant drafts or site maps.

## Consequences

Operators own availability, upgrades, backups, identity, and security posture.
The project must provide Compose, Helm, runbooks, health signals, and portable
export.

## Rejected alternatives

- Managed cloud only.
- Dual SaaS and self-host product in the beta.
