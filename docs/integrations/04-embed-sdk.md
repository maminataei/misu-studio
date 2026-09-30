# Embed SDK

**Status:** Authoritative SDK contract  
**Audience:** Host frontend and backend engineers  
**Owner:** Web SDK area

## Package

@commerce-studio/web-sdk is a framework-neutral TypeScript/JavaScript package.
It creates and destroys the editor iframe, performs protocol negotiation,
transfers a MessageChannel, and exposes typed events and commands.

## Host flow

The host backend obtains a one-time embedded-session grant. The browser passes
the grant to the SDK in memory; it MUST NOT persist it in local storage or put
it in a URL. The SDK loads the configured Studio origin and redeems through the
iframe protocol.

~~~ts
const studio = createStudioEmbed({
  container,
  studioOrigin,
  grant,
  initialRoute: { siteId, pageKey: "home" }
});

studio.on("ready", handleReady);
studio.on("dirty-state", handleDirty);
studio.on("published", handlePublication);
studio.on("error", handleSafeError);
~~~

## Events

Events include ready, route, selection, sync state, lease state, comment,
readiness, publication, session-expiring, height, and recoverable/fatal error.
Payloads are strictly validated and contain no session secrets.

## Host commands

The host may request semantic navigation, focus, readiness panel, publication
panel, session refresh, or graceful close. It cannot send map mutations,
bypass Studio authorization, or impersonate another site through messaging.

## Lifecycle

Destroying the embed closes ports, clears timers, and removes the iframe.
Session expiry prompts refresh through the authenticated host backend.
Protocol incompatibility fails with an actionable version error.
