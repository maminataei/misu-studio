# Renderer Conformance Protocol

**Status:** Authoritative protocol  
**Audience:** Renderer developers, CLI, registry, QA  
**Owner:** Conformance area

## Certification input

The conformance kit accepts an immutable renderer artifact, claimed effective
contract, test endpoint, and signed publisher identity. It supplies canonical
map fixtures and typed scenario data for every required combination.

## Assertions

Certification verifies:

- every page, region, section, variant, binding, action, mode, locale
  direction, and protected task claimed by the renderer;
- stable semantic annotations used by preview selection;
- required empty, loading, unavailable, error, and authenticated states;
- action descriptors rather than invented operational results;
- keyboard, focus, landmark, name, role, state, and serious automated
  accessibility requirements;
- rejection of unknown or incompatible map input; and
- deterministic observation output for the same artifact and fixture.

## Report

~~~ts
type ConformanceReport = {
  protocolVersion: number;
  rendererDigest: string;
  effectiveContractHash: string;
  suiteVersion: string;
  results: ConformanceCaseResult[];
  summary: { passed: number; failed: number; skipped: number };
  generatedAt: string;
  signature: SignatureEnvelope;
};
~~~

Required cases cannot be skipped. A report is invalid if artifact, contract,
suite, or signature differs from registration.

## Certification versus readiness

Certification establishes implementation capability. Target preflight
establishes that a particular deployed target can accept a particular map now.
Both are required for publication.
