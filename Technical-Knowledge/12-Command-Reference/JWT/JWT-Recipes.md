---
title: JWT Recipes
type: reference
tags: [technical-knowledge, jwt, security, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.rfc-editor.org/rfc/rfc7519
  - https://www.rfc-editor.org/rfc/rfc8725
---

# JWT Recipes

Use a maintained JOSE library. A JWT is a format; decoding the payload is not verification.

## Validate a token (required checks)

1. Parse with trusted library; reject malformed/oversized token.
2. Allowlist algorithm(s) from server configuration; never trust token header to choose arbitrary algorithm/key source.
3. Verify signature using trusted key set and expected key type.
4. Validate `iss`, `aud`, `exp`, and `nbf` when applicable, with small explicit clock tolerance.
5. Validate application claims, token purpose/type, tenant and authorization against current policy.
6. Reject unknown `kid`; refresh trusted JWKS under controlled policy, not from attacker-supplied URL.

## Pseudocode (library API varies)

```ts
const { payload, protectedHeader } = await jwtVerify(token, trustedKeySet, {
  issuer: expectedIssuer,
  audience: expectedAudience,
  algorithms: ['EdDSA'],
})
if (protectedHeader.typ !== 'at+jwt') throw new Error('wrong token type')
```

Set expected algorithm/issuer/audience out-of-band. Do not copy this exact call until confirming installed JOSE library version and token profile.

## Create claims safely

Use minimal claims: issuer, subject, audience, issued-at, expiry, unique token ID if revocation/replay control needs it. Keep expiration short for access tokens; never put secrets or sensitive data in payload because it is commonly readable.

## Key rotation

Publish key IDs; sign new tokens with current private key while validators accept current and retiring public keys for bounded overlap. Remove old key after max token lifetime plus clock tolerance. Protect private keys in secret manager/KMS.

## Revocation/logout

JWT is not automatically revocable. Use short expiry, refresh-token rotation, denylist keyed by `jti`, or server-side session strategy according to threat model. Do not assume deleting a browser cookie invalidates a stolen token.

## Read next

[[JWT Validation]] · [[OAuth 2.0 Recipes]] · [[Cookie and Session Security]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
