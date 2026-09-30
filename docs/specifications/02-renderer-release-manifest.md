# Renderer Release Manifest

**Status:** Authoritative protocol\
**Authority:** Normative within its stated scope\
**Audience:** Renderer and registry developers\
**Owner:** Renderer protocol area\
**Related:** [Specifications index](./README.md)\

## Purpose

The manifest describes a renderer implementation without exposing or executing
its code in Studio.

~~~ts
type RendererReleaseManifest = {
  manifestVersion: number;
  renderer: { id: string; version: string; publisher: PublisherRef };
  contracts: { base: VersionRef; modules: VersionRef[] };
  implementation: { framework?: string; artifactDigest: string };
  capabilities: {
    locales: string[];
    directions: Array<"ltr" | "rtl">;
    viewModes: string[];
    scenarios: string[];
    previewProtocolRange: string;
    preflightProtocolRange: string;
  };
  controls: DeclarativeControlManifest[];
  endpoints: EndpointRequirements;
  conformance: ConformanceEvidenceRef;
  provenance: ArtifactProvenance;
  signature: SignatureEnvelope;
};
~~~

## Immutability

Renderer ID and version identify immutable content. Reusing a version with a
different digest is rejected. Endpoint deployments belong to renderer targets,
not release manifests, so the same release may run in multiple environments.

## Controls

Controls refer only to fields already declared by the effective contract. They
compose Studio primitives and may add labels, grouping, safe conditional
visibility, help text, and preview hints. They cannot broaden schema, execute
logic, fetch data, or hide a contract-required field.

## Registration

Registration validates publisher authority, signature, artifact provenance,
contract existence, capability completeness, protocol compatibility, and
conformance evidence. Activation requires an integration administrator.

## Retirement

A release may become unavailable for new targets while remaining retained.
Deletion is blocked while any target, environment, version evidence, or
rollback window references it.
