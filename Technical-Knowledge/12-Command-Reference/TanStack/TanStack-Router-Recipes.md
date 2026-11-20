---
title: TanStack Router Recipes
type: reference
tags: [technical-knowledge, tanstack-router, routing, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://tanstack.com/router/latest/docs/framework/react/overview
---

# TanStack Router Recipes

Examples use React + file-based route generation; code-based route trees are also supported.

## Create route and validate search params

```tsx
export const Route = createFileRoute('/products')({
  validateSearch: z.object({ page: z.number().int().positive().catch(1) }),
  component: ProductsPage,
})
function ProductsPage() {
  const { page } = Route.useSearch()
  return <ProductList page={page} />
}
```

Use `validateSearch` to parse URL state once and keep it typed. Search params are user input; validate ranges and avoid putting secrets in URLs.

## Load route data

```tsx
export const Route = createFileRoute('/users/$userId')({
  loader: ({ params, abortController }) => api.getUser(params.userId, { signal: abortController.signal }),
  component: UserPage,
})
function UserPage() { const user = Route.useLoaderData(); return <h1>{user.name}</h1> }
```

Loader belongs to matched route; pass cancellation to network client. Configure pending/error UI and avoid duplicating the same server-state cache without a clear ownership model.

## Navigate with typed params/search

```tsx
<Link to="/products" search={{ page: 2 }}>Next page</Link>
```

Use router navigation APIs for imperative transitions; preserve or reset search keys intentionally.

## Search-param updates

Use functional updater when preserving unrelated keys: `navigate({ search: prev => ({ ...prev, page: prev.page + 1 }) })`. Keep URL state serializable and stable.

## Route context / auth

Provide typed context from router construction and validate access in `beforeLoad`/server boundary as appropriate. Client route guards improve UX but do not replace backend authorization.

## Read next

[[TanStack Router Loaders and URL State]] · [[TanStack Query Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
