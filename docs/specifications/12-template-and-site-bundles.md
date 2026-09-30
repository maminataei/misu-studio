# Template and Site Bundles

**Status:** Authoritative protocol  
**Audience:** CLI, API, template authors, operators  
**Owner:** Portability area

## Template artifacts

Starter kits, page templates, and section presets contain canonical semantic
content, compatible contract/policy declarations, referenced portable assets,
author, license, version, and source signature. Applying one creates a copy and
provenance record.

## Site export

A signed site bundle may contain:

- site metadata without installation identity;
- active draft and retained immutable versions;
- contract/module/policy requirements;
- environment names without credentials;
- templates and provenance;
- owned asset metadata and objects;
- comments and history according to export policy; and
- bundle manifest, hashes, and signature.

It MUST exclude users, password/session data, service credentials, encryption
keys, webhook secrets, OIDC configuration, audit actor private data, external
customer data, and installation signing keys.

## Import

Import unpacks into quarantine, validates paths, sizes, digests, signatures,
schemas, compatibility, licenses, and assets before creating records. Existing
IDs are mapped to new installation IDs. Import never overwrites a site; it
creates a new site or explicit new draft through a reviewed operation.

## Portability limits

External asset and host resource references require the destination
integration to resolve them. Missing requirements are reported before commit.
Published environments are not activated automatically after import.

## Archive safety

Bundles have bounded file count, expanded size, nesting, and compression ratio.
Paths are normalized and cannot escape extraction root. Parsing never executes
bundle content.
