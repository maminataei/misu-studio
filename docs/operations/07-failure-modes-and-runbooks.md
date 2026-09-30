# Failure Modes and Runbooks

**Status:** Authoritative  
**Audience:** Operators, support, reliability  
**Owner:** Reliability area

| Failure | Product behavior | Operator action |
| --- | --- | --- |
| API unavailable | Editing and publication stop; storefronts use cache | Restore API/database; verify no pointer corruption |
| PostgreSQL unavailable | API fails closed; workers retry connection | Recover primary; inspect transactions and queue age |
| Worker unavailable | Commands continue; async assets/readiness/webhooks pause | Restore workers; monitor oldest job and retries |
| Object storage unavailable | Existing map edits may continue; asset operations/readiness block | Restore storage; verify object digests |
| OIDC unavailable | Existing sessions follow policy; new SSO fails | Use permitted local admin recovery; restore issuer |
| Preview unavailable | Draft remains durable; preview/readiness target blocks | Inspect target health, origin, protocol, certificate |
| Host preflight unavailable | Publication blocks without override | Restore host target; rerun readiness |
| Webhook endpoint unavailable | Publication remains committed; delivery retries | Fix endpoint; replay retained event if required |
| Bad renderer release | Activation/publish blocked; old release remains | Revoke target activation; deploy corrected release |
| Signing key unavailable | Publication/runtime signing blocks | Restore protected key; do not generate unrelated replacement |
| Signature verification alert | Renderer retains last known good | Investigate key, artifact, transport, and possible compromise |
| Full disk or quota | Mutations likely block safely | Add capacity; verify database/object consistency |

## Incident rules

Preserve evidence, avoid destructive queue or database changes, identify exact
affected generations and key IDs, and record an incident timeline. Never
resolve a publication incident by editing immutable version rows or disabling
signature verification.

## Safe retries

Use original idempotency keys for uncertain client requests. Worker retries are
automatic within policy. Manual replay requires inspecting terminal category
and confirming the external effect is idempotent.

## Renderer fallback

A renderer that cannot verify a new pointer continues serving the previous
verified map, reports target health failure, and never falls back to a mutable
draft or generic unverified template.
