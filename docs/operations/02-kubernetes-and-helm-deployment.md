# Kubernetes and Helm Deployment

**Status:** Authoritative beta packaging  
**Audience:** Platform and SRE teams  
**Owner:** Operations maintainers

## Chart resources

The Helm chart defines editor and API Services, API and worker Deployments,
migration Job, ServiceAccounts, PodDisruptionBudgets, NetworkPolicy templates,
health probes, resource requests, security contexts, and optional ingress.
It does not install production PostgreSQL or S3 by default.

## Release safety

The migration Job completes before new API replicas become ready. Only one
migration holder proceeds. API and worker images use the same chart version
and immutable digest. Readiness verifies database schema compatibility,
required signing configuration, and storage access.

## Scaling

API replicas scale on latency and utilization. Worker replicas and task
concurrency scale on runnable jobs and database capacity. SSE requires ingress
timeouts and buffering settings compatible with long-lived HTTP responses but
does not require sticky sessions.

## Security

Pods run as non-root with dropped capabilities, seccomp defaults, read-only
root where possible, and dedicated service accounts. Secrets arrive through a
Kubernetes Secret or external secret provider. Network policies allow only
documented inbound and outbound flows.

## Disruption

API rolling updates keep available capacity. Workers stop accepting jobs and
finish or safely release leases before termination. A disruption cannot leave
a publication half committed because publication authority is PostgreSQL.

## Values contract

Every chart value maps to the configuration reference. Unknown values fail
schema validation. Sensitive values support existing-secret references and are
never rendered in notes.
