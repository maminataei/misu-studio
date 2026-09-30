# Preview and Browser Isolation

**Status:** Authoritative  
**Audience:** Editor, SDK, preview, web security  
**Owner:** Browser security area

## Origins and CSP

The editor and preview SHOULD use different origins. Studio sends a restrictive
CSP, denies unconfigured framing, disables mixed content, and allowlists only
required API, asset, and OIDC destinations. Preview origin configuration is an
administrator operation and requires HTTPS outside local development.

## Sandbox

Preview iframes grant only capabilities required by the renderer fixture.
Top navigation, downloads, popups, presentation, pointer lock, and parent DOM
access are denied by default. Same-origin permission is allowed only when the
preview architecture requires it and does not share the editor origin.

## Messaging

Every message is received on a transferred MessagePort after exact origin,
nonce, target, and protocol verification. Payloads pass strict size and schema
validation. Unknown types are ignored and recorded at a bounded rate.

Selection geometry is data only. Preview-provided text is treated as untrusted.
The editor never inserts preview HTML into its own DOM.

## Preview grants

A grant authorizes one target to read one site's map at one draft revision and
fixture set. It expires quickly, is audience and nonce bound, and is stored
hashed after issuance. Redemption is server-to-server where possible.

## Navigation and actions

Preview actions are simulations against fixtures. They cannot create real
carts, orders, payments, accounts, messages, or entitlements. Navigation
changes semantic preview context and cannot redirect the top-level browser.

## Abuse limits

Studio bounds message frequency, geometry count, diagnostics, fixture size,
render time, and preview restarts. A failing preview is terminated without
affecting draft durability.
