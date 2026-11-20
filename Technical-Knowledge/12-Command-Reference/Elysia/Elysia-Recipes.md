---
title: Elysia Recipes
type: reference
tags: [technical-knowledge, elysia, bun, typescript, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://elysiajs.com/
  - https://github.com/elysiajs/elysia/releases
---

# Elysia Recipes

Elysia targets Bun. Check whether project uses stable v1 or v2 RC; APIs/plugins may differ by major.

## Install and run

```sh
bun add elysia
bun run src/index.ts
```

## Declare route schemas

```ts
import { Elysia, t } from 'elysia'
const app = new Elysia()
  .post('/users', ({ body }) => createUser(body), {
    body: t.Object({ email: t.String({ format: 'email' }), name: t.String() }),
    response: t.Object({ id: t.String(), email: t.String() }),
  })
  .listen(3000)
```

Schema drives runtime validation and inferred handler/client types. Treat response schemas as an allowlist; do not return secrets.

## Add lifecycle hooks / derive context

Use `.derive()` for request-derived values that later handlers need; use `.resolve()` when derived values depend on validated input. Keep expensive work out of global hooks unless every route needs it; test hook order and scope.

## Compose plugin and groups

```ts
const auth = new Elysia({ name: 'auth' }).derive(({ headers }) => ({ user: verify(headers.authorization) }))
const app = new Elysia().use(auth).get('/me', ({ user }) => user)
```

Plugin scope/encapsulation affects where decorations and routes are visible. Give reusable plugins stable names and avoid accidental duplicate registration.

## Map errors

Use `.onError(({ code, error, set }) => { ... })` for centralized mapping; return a safe public error and log internal detail. Distinguish validation errors, not found, and internal faults.

## Read next

[[Elysia Schemas Plugins and Type Inference]] · [[Bun Recipes]] · [[TypeScript Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
