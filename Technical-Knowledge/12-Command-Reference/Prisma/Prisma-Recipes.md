---
title: Prisma Recipes
type: reference
tags: [technical-knowledge, prisma, database, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.prisma.io/docs/orm/prisma-schema/overview
  - https://www.prisma.io/docs/orm/prisma-client/queries/transactions
---

# Prisma Recipes

Prisma major versions differ substantially. ORM 8 is prerelease in the checked snapshot; use commands and client imports from the installed major only.

## Initialize and configure

```sh
npx prisma init
npx prisma validate
npx prisma generate
```

Keep credentials in environment/secret manager; configure datasource and generated client according to the matching major's setup guide.

## Define model and migrate

```prisma
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  name      String
  createdAt DateTime @default(now())
}
```

```sh
npx prisma migrate dev --name add_user
npx prisma migrate deploy
```

`migrate dev` is for local development and creates migrations; production applies committed migrations with `migrate deploy`. Review SQL and backup before destructive schema changes.

## Query safely

```ts
const user = await prisma.user.findUnique({ where: { email } })
const users = await prisma.user.findMany({
  where: { name: { contains: search } },
  select: { id: true, name: true },
  take: 50,
})
```

Use `select` to minimize data exposure and payload. Add deterministic ordering for pagination; inspect generated SQL and indexes for hot paths.

## Create relation in transaction

```ts
const result = await prisma.$transaction(async tx => {
  const order = await tx.order.create({ data: orderInput })
  await tx.inventory.update({ where: { id: stockId }, data: { quantity: { decrement: 1 } } })
  return order
})
```

Keep transaction short; no remote API call inside DB transaction. Handle serialization/deadlock retries only when operation is safe to retry.

## Avoid connection leaks

Reuse one Prisma client per process/server instance, but isolate request data; close client during shutdown. Serverless deployments need connection pooling/proxy appropriate to provider.

## Read next

[[Prisma Data Model and Migration Safety]] · [[Database Transactions]] · [[SQL Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
