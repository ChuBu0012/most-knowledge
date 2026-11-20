---
title: React Router Recipes
type: reference
tags: [technical-knowledge, react-router, react, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://reactrouter.com/start/framework/installation
  - https://reactrouter.com/start/framework/data-loading
---

# React Router Recipes

## Create project

```sh
npx create-react-router@latest my-app
cd my-app
npm install
npm run dev
```

## Define route module

Route module exports `loader`, `action`, `Component`, and optional `ErrorBoundary`; generated `Route.*Args` types bind module code to route params/data.

## Load route data

```ts
export async function loader({ params, request }: Route.LoaderArgs) {
  const response = await fetch(`/api/users/${params.userId}`, { signal: request.signal })
  if (!response.ok) throw new Response('Not found', { status: response.status })
  return response.json() as Promise<User>
}
```

Pass abort signal, validate data and enforce server auth in server loader/action. Client loader cannot safely access secrets.

## Submit a mutation

Use `<Form method="post">` with named fields and an `action` that parses `request.formData()`, validates and persists. Return field errors or redirect after successful mutation. Use `useNavigation()` to show pending state.

## Fetch without navigating

Use `useFetcher()` for background form submissions or loads; inspect `fetcher.state` and preserve errors. Do not duplicate mutation execution in click handler and form action.

## URL search state

Use `useSearchParams()` for filters/pagination/sort that should persist in URL. Parse and clamp input; update via functional setter when preserving unrelated parameters.

## Read next

[[TanStack Router Recipes]] · [[React Recipes]] · [[HTTP Semantics and REST]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
