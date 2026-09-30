# Self-Hosting Requirements

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** Operators and platform engineers\
**Owner:** Operations maintainers\
**Related:** [Operations index](./README.md)\

## Required services

- PostgreSQL supported by the current release.
- S3-compatible object storage for production.
- HTTPS ingress for editor and API.
- SMTP or equivalent adapter where local-account verification/recovery is used.
- DNS and an accurate time source.

The beta does not require Redis, RabbitMQ, a managed vendor connection, or a
marketplace connection.

## Processes

Run the static editor, one or more API replicas, one or more worker replicas,
and an exclusive migration job. API and worker images share a release version.
Mixed versions are permitted only during a documented rolling-upgrade window.

## Capacity baseline

The supported beta target is 1,000 sites and 25 concurrent editors. Operators
size PostgreSQL connections across API and workers, keep headroom for
migrations and administration, and apply bounded worker concurrency.

## Durability

PostgreSQL and object storage require independent encrypted backups.
Installation signing and encryption keys require separately protected backup;
losing them can make retained maps unverifiable or secrets unrecoverable.

## Security baseline

Use least-privilege service identities, private database/storage networks,
TLS, non-root containers, read-only root filesystems where supported, current
base images, external secret management, and restricted outbound destinations.

## Unsupported production modes

Filesystem object storage, SQLite, a single shared superuser database account,
HTTP without TLS, floating container tags, and ephemeral PostgreSQL volumes are
development-only or unsupported.
