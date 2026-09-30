# ADR-0001: Standalone Self-Hosted Product

**Status:** Accepted  
**Date:** 2026-09-30

## Context

A builder embedded directly in Misu would inherit Misu identity, persistence,
commerce models, release cadence, and frontend assumptions. Other commerce
platforms could not adopt it without extracting those dependencies.

## Decision

Commerce Studio is an independent repository, deployment, database, API, and
package family. It provides a standalone editor application and an iframe SDK.
Misu is an external integration and first production-quality consumer.

## Consequences

Studio needs explicit integration, preview, runtime-map, and identity-exchange
protocols. It cannot import Misu packages or query Misu databases. This cost is
accepted in exchange for a real product boundary and independent releases.

## Rejected alternatives

- Permanent residence in the Misu monorepo.
- Embedded SDK without a standalone application.
- Standalone application without an embedding protocol.
