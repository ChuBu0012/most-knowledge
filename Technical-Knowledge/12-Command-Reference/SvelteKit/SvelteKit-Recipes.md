---
title: SvelteKit Recipes
type: reference
tags: [technical-knowledge, sveltekit, svelte, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://svelte.dev/docs/kit
---

# SvelteKit Recipes

## Create and run

```sh
npx sv create my-app
cd my-app
npm install
npm run dev
```

## Route and server load

Create `src/routes/products/[id]/+page.server.ts`:

```ts
import type { PageServerLoad } from './$types'
export const load: PageServerLoad = async ({ params, locals }) => {
  const product = await locals.db.product.findUnique({ where: { id: params.id } })
  if (!product) error(404, 'Not found')
  return { product }
}
```

Use server load for DB/secrets; return only serializable safe data. Use universal `+page.ts` for browser-safe/shared fetching.

## Form action

In `+page.server.ts`, export `actions = { default: async ({ request, locals }) => { ... } }`; parse `request.formData()`, validate, save, then `redirect(303, '/done')`. Return `fail(400, { errors })` for recoverable validation. Bind `<form method="POST">` and progressively enhance with `use:enhance`.

## API endpoint

Export `GET`/`POST` handlers from `+server.ts`; validate body and auth, return `json(data, { status })`. Do not expose server exception details.

## Navigation and invalidation

Use `goto` for client navigation, `invalidate`/`invalidateAll` after writes when relevant load data depends on the mutation. Prefer targeted `depends` identifiers to avoid refreshing unrelated data.

## Check/build

`npm run check`, `npm run build`, `npm run preview`; configure adapter for target runtime.

## Read next

[[Svelte Runes and Reactivity]] · [[SvelteKit Load Functions and Form Actions]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
