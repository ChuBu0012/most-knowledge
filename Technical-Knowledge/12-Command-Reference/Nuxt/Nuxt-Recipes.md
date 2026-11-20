---
title: Nuxt Recipes
type: reference
tags: [technical-knowledge, nuxt, vue, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://nuxt.com/docs/4.x/getting-started/introduction
  - https://nuxt.com/docs/4.x/api/composables/use-fetch
---

# Nuxt Recipes

## Create and run

```sh
npx nuxi@latest init my-app
cd my-app
npm install
npm run dev
```

## Create page and route param

Create `app/pages/users/[id].vue`; access `const route = useRoute()` and validate `route.params.id` before calling services.

## Fetch data with SSR/hydration

```vue
<script setup lang="ts">
const route = useRoute()
const { data, pending, error } = await useFetch(() => `/api/users/${route.params.id}`)
</script>
```

`useFetch` serializes SSR result for hydration. Use reactive key/getter when route param changes; render pending/error states and avoid exposing private response fields.

## Create server endpoint

Create `server/api/users/[id].get.ts`:

```ts
export default defineEventHandler(async (event) => {
  const id = getRouterParam(event, 'id')
  if (!id) throw createError({ statusCode: 400, statusMessage: 'Invalid id' })
  return await findUser(id)
})
```

Validate/authenticate on server. `$fetch`/`useFetch` calls do not replace access control.

## Runtime config

Declare secrets in private `runtimeConfig`; place only intentionally public values under `runtimeConfig.public`. Read request-scoped settings in server event context; don't expose secret env through serialized page data.

## Build/deploy

`npm run build`; choose Nitro preset matching platform. For Node server output, use the generated `.output/server/index.mjs` entry; static output requires prerender-compatible routes.

## Read next

[[Nuxt Data Fetching and Request Context]] · [[Vue API Recipes]] · [[FastAPI Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
