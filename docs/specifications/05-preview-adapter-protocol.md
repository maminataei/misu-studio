# Preview Adapter Protocol

**Status:** Authoritative protocol  
**Audience:** Web SDK, editor, preview implementers, security  
**Owner:** Preview protocol area

## Transport

The editor loads an administrator-configured HTTPS preview origin in a
sandboxed iframe. After origin verification, both sides establish a dedicated
MessageChannel. Messages include protocol version, channel ID, sequence,
correlation ID where relevant, and discriminated payload.

## Handshake

1. Preview sends hello with supported protocol range, target release, and
   unpredictable nonce.
2. Editor verifies origin and asks Studio for a grant bound to nonce, site,
   draft revision, target, and audience.
3. Editor transfers a MessagePort and grant.
4. Preview exchanges the grant server-to-server for a read-only payload.
5. Preview returns ready with map and render hashes.

The grant is short-lived, one-purpose, and replay protected. It never appears
in a query string or referrer.

## Commands

Editor-to-preview messages select page, scenario, locale, view mode, section,
and diagnostic focus. Preview-to-editor messages report ready, navigation,
selection, semantic bounds, rendered tasks, warnings, errors, focus movement,
and height.

Preview MUST NOT request draft mutation. The editor translates user gestures
into ordinary Studio commands after validating current selection.

## Scenarios

The contract declares scenario keys and typed fixture requirements. The host
preview adapter supplies deterministic non-customer fixtures. A fixture is
identified by version and hash so readiness can reproduce it.

## Failure

Protocol mismatch, wrong origin, wrong target, expired grant, render-hash
mismatch, or malformed message closes the channel and reports a recoverable
preview error. Public storefront state is unaffected.
