---
title: sqlc Recipes
type: reference
tags: [technical-knowledge, sqlc, go, sql, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://docs.sqlc.dev/en/latest/
  - https://docs.sqlc.dev/en/latest/howto/parameters.html
---

# sqlc Recipes

## Configure and generate

```sh
sqlc init
sqlc generate
```

Configure schema, query paths, engine, Go package/output and SQL driver in `sqlc.yaml`. Commit generated source or follow a deliberate generated-code policy; run generation in CI to detect drift.

## Write annotated query

```sql
-- name: GetUser :one
SELECT id, email, name FROM users WHERE id = $1;

-- name: ListUsers :many
SELECT id, email FROM users ORDER BY id LIMIT $1 OFFSET $2;
```

Annotations define generated method cardinality. Parameterize all values; dynamic SQL identifiers/order cannot be passed as ordinary bind parameters, so allowlist them.

## Call generated Go methods

```go
user, err := queries.GetUser(ctx, userID)
if errors.Is(err, sql.ErrNoRows) { return ErrNotFound }
if err != nil { return fmt.Errorf("get user: %w", err) }
```

Pass request context; map `sql.ErrNoRows` distinctly. Keep generated query package behind a repository/service boundary when domain behavior needs a stable API.

## Transaction-bound queries

```go
tx, err := db.BeginTx(ctx, nil)
if err != nil { return err }
defer tx.Rollback()
qtx := queries.WithTx(tx)
if err := qtx.UpdateUser(ctx, arg); err != nil { return err }
return tx.Commit()
```

Handle commit errors and ensure all queries in the unit use `qtx`. Use isolation/locking appropriate to the invariant.

## Read next

[[sqlc Query Contracts and Generated Code]] · [[SQL Recipes]] · [[Go Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
