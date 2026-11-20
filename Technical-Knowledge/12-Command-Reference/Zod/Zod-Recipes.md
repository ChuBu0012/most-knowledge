---
title: Zod Recipes
type: reference
tags: [technical-knowledge, zod, typescript, validation, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://zod.dev/basics
  - https://zod.dev/api
---

# Zod Recipes

Examples use Zod 4. Check v3 migration notes before copying APIs between majors.

## Define schema and infer type

```ts
const UserSchema = z.object({
  id: z.string().uuid(),
  email: z.email(),
  displayName: z.string().min(1).max(80),
})
type User = z.infer<typeof UserSchema>
```

Schema validates runtime data; inferred type prevents duplicate handwritten contracts.

## Parse untrusted data

```ts
const result = UserSchema.safeParse(await response.json())
if (!result.success) {
  console.error(result.error.issues)
  return { kind: 'invalid-response' as const }
}
const user = result.data
```

Use `parse` when invalid data should throw; `safeParse` when caller should branch on validation result. Never cast API JSON directly to a trusted type.

## Transform input and output types

```ts
const AgeSchema = z.string().transform(Number).pipe(z.number().int().nonnegative())
type AgeInput = z.input<typeof AgeSchema>   // string
type AgeOutput = z.output<typeof AgeSchema> // number
```

Keep input/output distinction visible when forms coerce strings into domain values.

## Compose schemas

Use `.extend()` to add object fields, `.pick()`/`.omit()` to derive safe subsets, and `.array()` for lists. Avoid sharing a response schema that accidentally exposes password hashes or internal fields.

## Validate environment/config

Parse environment variables once at startup; report missing/invalid keys early. Keep private server env schemas separate from values bundled to clients.

## Format errors

Use `error.issues` to map path/code/message into field errors. Do not expose raw internal values in user-facing messages or logs.

## Read next

[[Zod Runtime Validation]] · [[TypeScript Recipes]] · [[React Hook Form Registration and Validation]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
