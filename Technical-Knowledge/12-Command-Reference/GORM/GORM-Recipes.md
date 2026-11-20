---
title: GORM Recipes
type: reference
tags: [technical-knowledge, gorm, go, database, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://gorm.io/docs/
  - https://gorm.io/docs/transactions.html
---

# GORM Recipes

## Connect and define model

```go
type User struct {
  ID uint `gorm:"primaryKey"`
  Email string `gorm:"uniqueIndex;not null"`
  Name string
}
```

Open a DB handle once per process with driver config; set pool limits on underlying `sql.DB` and close on shutdown.

## Create and query

```go
result := db.Create(&user)
if result.Error != nil { return result.Error }
var user User
if err := db.Where("email = ?", email).First(&user).Error; err != nil { return err }
```

Always bind values with `?`; do not concatenate untrusted SQL. Check `ErrRecordNotFound` separately from infrastructure errors.

## Select fields and paginate

Use `Select("id", "name")`, deterministic `Order("created_at DESC, id DESC")`, and bounded `Limit`. Avoid unbounded `Find(&all)` on large tables. Inspect SQL with logger in development.

## Transaction

```go
err := db.Transaction(func(tx *gorm.DB) error {
  if err := tx.Create(&order).Error; err != nil { return err }
  return tx.Model(&Inventory{}).Where("id = ? AND quantity > 0", id).
    UpdateColumn("quantity", gorm.Expr("quantity - 1")).Error
})
```

Returning an error rolls back; nil commits. Check affected rows to enforce inventory invariants. Keep network calls outside transaction.

## Preload association

`db.Preload("Orders").Find(&users)` loads associations separately. Use only needed relations; review query count/row explosion and prefer explicit select for API response.

## Read next

[[GORM Transactions and Associations]] · [[Go Recipes]] · [[SQL Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
