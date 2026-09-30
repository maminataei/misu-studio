# ADR-0003: Shared Renderer Contracts

**Status:** Accepted  
**Date:** 2026-09-30

## Context

A map tied to one renderer manifest is reusable only by that implementation.
Separate maps per framework fragment templates and publication history.

## Decision

Maps target immutable semantic commerce contracts. Multiple renderer releases
may claim and certify conformance to the same contract. Sites select preview
targets, and environments publish one map atomically to all active targets.

## Consequences

A formal conformance suite and exact compatibility claims are required.
Target-specific visual differences are allowed only within semantic and
accessibility invariants.

## Rejected alternatives

- One renderer per site.
- Renderer-specific map shapes.
- Unverified self-declared compatibility.
