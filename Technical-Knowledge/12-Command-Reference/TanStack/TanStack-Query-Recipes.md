---
title: TanStack Query Recipes
type: reference
tags: [technical-knowledge, tanstack-query, cache, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://tanstack.com/query/latest/docs/framework/react/overview
  - https://tanstack.com/query/latest/docs/framework/react/guides/invalidations-from-mutations
---

# TanStack Query Recipes

Examples use React adapter v5. Query core concepts carry across adapters, but hook syntax differs.

## Create client/provider

```tsx
const [client] = useState(() => new QueryClient())
return <QueryClientProvider client={client}>{children}</QueryClientProvider>
```

Create one client per browser app; on SSR create an isolated client per request to prevent cache data crossing users.

## Fetch with a complete query key

```tsx
const query = useQuery({
  queryKey: ['users', { page, status }],
  queryFn: ({ signal }) => api.listUsers({ page, status, signal }),
})
```

Include every variable that changes result in `queryKey`; pass abort `signal` to transport. Render `isPending`, `isError`, and data explicitly.

## Mutate and invalidate

```tsx
const mutation = useMutation({
  mutationFn: api.createUser,
  onSuccess: async () => queryClient.invalidateQueries({ queryKey: ['users'] }),
})
```

Invalidate keys whose server data may be stale. Avoid invalidating the entire cache for a local change.

## Optimistic update

In `onMutate`, cancel matching queries, snapshot cached value, and write optimistic value. In `onError`, restore snapshot; in `onSettled`, invalidate/reconcile. Make rollback safe when overlapping mutations can occur.

## Pagination / infinite queries

Put page/filter in query key for independent pages. Use `useInfiniteQuery` with a `getNextPageParam` that returns `undefined` when finished; flatten pages only at render boundary. Verify stable identity and duplicate handling.

## Tune freshness and retries

`staleTime` controls when data is considered fresh; `gcTime` controls retention after unused. They are different. Configure retry by error class/status; do not retry deterministic validation/auth failures endlessly.

## Read next

[[TanStack Query Cache Lifecycle]] · [[TanStack Router Loaders and URL State]] · [[Zod Runtime Validation]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
