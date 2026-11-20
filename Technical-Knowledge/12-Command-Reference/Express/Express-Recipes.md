---
title: Express Recipes
type: reference
tags: [technical-knowledge, express, nodejs, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://expressjs.com/en/guide/routing.html
  - https://expressjs.com/en/guide/error-handling.html
---

# Express Recipes

Express 5 patterns; Express 4 and 5 differ in async error propagation and some APIs. Check installed major.

## Install and start

```sh
npm install express
npm install -D typescript tsx @types/express @types/node
npx tsx src/server.ts
```

## Define route and parse JSON

```ts
import express from 'express'
const app = express()
app.use(express.json({ limit: '1mb' }))
app.get('/users/:id', async (req, res) => {
  const user = await users.find(req.params.id)
  if (!user) return res.status(404).json({ error: 'not_found' })
  res.json(user)
})
app.post('/users', async (req, res) => {
  const input = CreateUserSchema.parse(req.body)
  res.status(201).json(await users.create(input))
})
```

Validate request bodies at the boundary; `express.json()` only parses JSON and does not validate schema.

## Middleware

```ts
app.use(requestId)
app.use('/api', authenticate)
app.use('/api/users', usersRouter)
```

Middleware order is execution order. Put parsers before handlers and routes; scope auth middleware to protected routes. Call `next()` once or end the response.

## Central error handler

```ts
app.use((err, req, res, next) => {
  if (res.headersSent) return next(err)
  const status = err.statusCode ?? 500
  req.log?.error({ err }, 'request failed')
  res.status(status).json({ error: status < 500 ? err.message : 'internal_error' })
})
```

Place after routes. Express 5 forwards rejected async handlers; in Express 4 wrap async handlers or use a wrapper. Never expose stack traces/secrets in production responses.

## Start and shut down

```ts
const server = app.listen(Number(process.env.PORT ?? 3000))
process.on('SIGTERM', () => server.close(() => process.exit(0)))
```

Also close DB/queue clients during shutdown and impose a deadline. Configure proxy trust only for known ingress hops.

## Read next

[[Express Middleware Ordering and Errors]] · [[HTTP Request Lifecycle]] · [[Zod Runtime Validation]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
