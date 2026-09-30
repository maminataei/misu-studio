# Assets, Fonts, and Media

**Status:** Authoritative protocol\
**Authority:** Normative within its stated scope\
**Audience:** Asset service, editor, renderer, operations, security\
**Owner:** Asset area\
**Related:** [Specifications index](./README.md)\

## Asset identity

An asset record contains site ownership, stable ID, content digest, declared
purpose, detected media type, byte length, dimensions/duration where relevant,
processing status, accessibility metadata, source provenance, and immutable
object/derivative references.

Maps reference asset ID and semantic intent such as original, thumbnail,
card, hero, or social. Storage URLs and internal bucket keys are excluded.

## Upload flow

1. Editor requests a bounded upload intent.
2. API authorizes site and media purpose and returns a short-lived upload.
3. Client uploads to quarantine.
4. Worker validates magic bytes, size, decode limits, metadata, and policy.
5. Worker strips unsafe metadata, sanitizes supported SVG or rejects it,
   generates configured derivatives, and moves verified objects by digest.
6. Asset becomes selectable only after successful processing.

Failures retain a safe diagnostic record and expire quarantined bytes.

## External sources

An integration may register an asset adapter with typed search and selection.
Studio stores a stable external reference plus preview metadata. The host owns
authorization and delivery. An external reference unavailable at readiness is
a blocker when used by a required section.

## Fonts

Font records identify family, weights, styles, WOFF2 objects, license
declaration, source, and renderer support. Policy controls who may upload.
Renderers map the semantic font ID to verified delivery; arbitrary font URLs
are rejected.

## Garbage collection

Objects are content-addressed and may be deduplicated without crossing access
control. Collection follows reference reachability, retention, export locks,
and a grace period.
