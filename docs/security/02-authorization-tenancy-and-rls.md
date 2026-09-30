# Authorization, Tenancy, and Row-Level Security

**Status:** Authoritative\
**Authority:** Normative within its stated scope\
**Audience:** API, database, security, QA\
**Owner:** Authorization area\
**Related:** [Security index](./README.md)\

## Authorization model

Capabilities are explicit actions over resources. Standard roles provide
bundles, but services authorize capabilities rather than role names. Scope
flows installation to organization to integration to site; a child grant
cannot exceed its parent.

Sensitive capabilities include membership administration, service credential
creation, renderer activation, policy activation, production approval,
publication, retention override, signing-key operations, and export.

## Request context

Authentication establishes actor identity. Route resolution establishes
authorized organization and resource scope. User-supplied IDs are selectors,
not authority. Authorization occurs before repositories return existence.

Background jobs carry a minimal signed or persisted execution context and
recheck current resource state. They do not inherit a web request's database
session.

## Database enforcement

Tenant tables include organization identity directly or through a constrained
parent. Transactions set validated tenant context on the connection. RLS
policies deny rows outside that context, and missing context defaults to deny.
Application repositories also include tenant predicates so RLS is defense in
depth rather than the only boundary.

Migration, backup, and maintenance roles are separate from application roles.
The application role does not own protected tables or hold BYPASSRLS.

## Object storage

Object keys use server-generated identifiers and content digests. Database
authorization precedes signed URL creation. Bucket listing is not exposed.
External asset adapters receive only the scoped query permitted by integration
policy.

## Tests

Every resource family has cross-organization and cross-site negative tests,
including guessed IDs, nested resources, jobs, SSE cursors, exports, assets,
comments, templates, versions, and runtime credentials.
