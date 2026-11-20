---
title: Bun Recipes
type: reference
tags: [technical-knowledge, bun, javascript-runtime, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://bun.sh/docs
  - https://bun.sh/docs/runtime/http/server
---

# Bun Recipes

## Create project and manage dependencies

```sh
bun init
bun add zod
bun add -d typescript
bun install
bun run src/index.ts
```

Commit `bun.lock` and verify native modules/production runtime compatibility before relying on Bun-specific behavior.

## Serve HTTP

```ts
const server = Bun.serve({
  port: Number(Bun.env.PORT ?? 3000),
  async fetch(request) {
    const url = new URL(request.url)
    if (url.pathname === '/health') return Response.json({ ok: true })
    return new Response('Not found', { status: 404 })
  },
})
console.log(`listening on ${server.port}`)
```

Use Fetch API Request/Response semantics; validate inputs, set limits/timeouts, and do not expose exception messages to clients.

## Read/write file

```ts
const text = await Bun.file('./data.txt').text()
await Bun.write('./copy.txt', text)
```

For large files, use streams rather than buffering entire contents. Treat file paths and uploads as untrusted.

## Hash / password

Use `Bun.password.hash` / `Bun.password.verify` for password workflows instead of general-purpose fast hashes; still apply rate limits, reset protections, and secure storage policy. For tokens/hashes, use cryptographic APIs appropriate to the purpose.

## Run tests and build

```sh
bun test
bun build ./src/index.ts --outdir ./dist
```

Check Bun test-runner compatibility with Node-based tooling; run production smoke checks in the actual target environment.

## Read next

[[Bun Runtime Compatibility and Deployment]] · [[Elysia Recipes]] · [[Hono Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
