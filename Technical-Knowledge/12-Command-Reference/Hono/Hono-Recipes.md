---
title: Hono Recipes
type: reference
tags: [technical-knowledge, hono, typescript, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://hono.dev/docs/
  - https://hono.dev/docs/guides/validation
---

# Hono Recipes

## Install and create app

```sh
npm install hono
```

```ts
import { Hono } from 'hono'
const app = new Hono()
app.get('/health', c => c.json({ ok: true }))
export default app
```

Export shape depends on target adapter (Workers, Bun, Node); choose the deployment adapter rather than assuming one runtime.

## Validate request with schema middleware

```ts
import { zValidator } from '@hono/zod-validator'
import { z } from 'zod'
const bodySchema = z.object({ name: z.string().min(1) })
app.post('/users', zValidator('json', bodySchema), async c => {
  const input = c.req.valid('json')
  return c.json(await createUser(input), 201)
})
```

Validation middleware parses at the boundary. Do not use `c.req.json()` as trusted typed data without validating it.

## Middleware and environment bindings

```ts
app.use('/api/*', async (c, next) => {
  c.set('requestId', crypto.randomUUID())
  await next()
})
```

Use typed `Env` bindings for platform resources/secrets; keep secrets out of source and client responses. Middleware order controls which routes receive it.

## Handle not found and errors

Set `app.notFound(...)` and `app.onError((err, c) => ...)`; return safe JSON/status, log details in server context, and avoid exposing stack traces. Keep expected validation failures distinct from unexpected faults.

## Read next

[[Hono Middleware and Request Validation]] · [[TypeScript Recipes]] · [[Zod Runtime Validation]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
