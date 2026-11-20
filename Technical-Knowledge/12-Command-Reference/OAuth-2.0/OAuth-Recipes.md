---
title: OAuth 2.0 Recipes
type: reference
tags: [technical-knowledge, oauth, security, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.rfc-editor.org/rfc/rfc9700
  - https://www.rfc-editor.org/rfc/rfc7636
---

# OAuth 2.0 Recipes

OAuth is an authorization protocol; prefer maintained OIDC/OAuth client libraries over hand-implementing protocol details.

## Authorization Code with PKCE flow

1. Generate a cryptographically random `state` and PKCE `code_verifier`.
2. Compute `code_challenge = BASE64URL(SHA256(code_verifier))`; use `code_challenge_method=S256`.
3. Redirect to authorization endpoint with `response_type=code`, client ID, exact registered redirect URI, scopes, state and challenge.
4. On callback, compare returned state to stored one; reject mismatch/replay.
5. Exchange code + original verifier at token endpoint from trusted client/server context.
6. Validate issuer, audience, signature and expiry of returned tokens before using them.

## PKCE primitives (illustrative)

```ts
const verifier = base64url(crypto.getRandomValues(new Uint8Array(32)))
const digest = await crypto.subtle.digest('SHA-256', new TextEncoder().encode(verifier))
const challenge = base64url(new Uint8Array(digest))
```

Use a vetted implementation for base64url and secure randomness; verifier must be bound to the login transaction and stored safely until callback.

## Protect callback and redirect

Use exact redirect URI matching; do not accept arbitrary `returnTo` URLs. Validate `state`, bind it to the browser session, and clear it after use. Use nonce and ID-token validation for OIDC authentication.

## Refresh/access token handling

Keep client secrets and refresh tokens server-side when possible; use secure HttpOnly cookies/session storage patterns. Rotate/revoke refresh tokens as provider supports. Request least-privilege scopes and avoid logging bearer tokens.

## Do not use legacy flows

Avoid implicit grant and resource-owner-password credentials. Do not treat OAuth access token as proof of user identity unless using validated OIDC ID token.

## Read next

[[OAuth Authorization Code with PKCE]] · [[JWT Recipes]] · [[Cookie and Session Security]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
