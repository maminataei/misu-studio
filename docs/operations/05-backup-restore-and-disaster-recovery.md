# Backup, Restore, and Disaster Recovery

**Status:** Authoritative  
**Audience:** Operators and security  
**Owner:** Reliability area

## Backup set

A recoverable installation requires a transactionally consistent PostgreSQL
backup, versioned object-storage backup, encryption master keys, active and
retained signing keys, configuration without ephemeral secrets, and release
version metadata.

Database and object backups alone are insufficient if verification or
encryption keys are lost.

## Schedule and retention

Operators define recovery point and recovery time objectives. The project
provides example daily full plus continuous database recovery and versioned
object-storage policy, but production values are deployment decisions.
Backups are encrypted, access controlled, monitored, and stored outside the
primary failure domain.

## Restore test

At a documented cadence, restore into an isolated environment, verify database
integrity, object digests, signing-key continuity, local/OIDC login, draft
commands, immutable runtime map retrieval, and a renderer verification test.
Record measured recovery time and missing artifacts.

## Disaster recovery

1. Stop writes or fence the failed primary.
2. Select mutually consistent database/object/key recovery points.
3. Restore with no public ingress.
4. run schema and integrity verification;
5. rotate credentials potentially exposed by the incident;
6. start workers paused, then API;
7. verify environment pointers and signed maps;
8. resume workers and ingress; and
9. reconcile webhook generations and external targets.

## Site bundles

Signed site bundles support portability but are not an installation backup:
they intentionally exclude identities, secrets, and trust keys.
