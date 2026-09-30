# Docker Compose Deployment

**Status:** Authoritative beta packaging  
**Audience:** Evaluators and small-installation operators  
**Owner:** Operations maintainers

## Profiles

The Compose distribution provides:

- an evaluation profile with PostgreSQL and S3-compatible storage;
- a production-like profile accepting external PostgreSQL, S3, SMTP, and OIDC;
- an initialization job for migrations and first administrator creation; and
- separate editor, API, and worker services.

Evaluation defaults are not production credentials and MUST require explicit
replacement before a production mode starts.

## Startup order

1. Validate configuration without revealing secrets.
2. Confirm PostgreSQL and storage connectivity.
3. Acquire the migration lock and migrate.
4. Start API and worker at the same release.
5. Serve editor assets only after API compatibility health succeeds.

Health dependencies improve startup behavior but do not replace retry logic.

## Volumes

Only database and local evaluation object storage use persistent volumes.
Application containers are replaceable. Operators test backup and restore
outside the Compose lifecycle.

## Upgrades

Pull images by immutable digest, read release notes, back up state, run the
preflight command, apply migrations, replace services, verify health and worker
queues, then test editor bootstrap and runtime map reads. Rollback follows the
release's declared database compatibility.

## Exposure

Only the reverse proxy publishes ports. PostgreSQL and object storage consoles
remain private. Local development may relax this on loopback only.
