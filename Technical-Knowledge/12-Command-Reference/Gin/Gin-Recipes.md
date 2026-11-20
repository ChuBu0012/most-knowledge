---
title: Gin Recipes
type: reference
tags: [technical-knowledge, gin, go, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://gin-gonic.com/en/docs/
  - https://github.com/gin-gonic/gin/releases
---

# Gin Recipes

## Install and run

```sh
go get github.com/gin-gonic/gin
go run ./cmd/api
```

## Register route and bind JSON

```go
type CreateUser struct { Email string `json:"email" binding:"required,email"` }
r := gin.Default()
r.POST("/users", func(c *gin.Context) {
    var input CreateUser
    if err := c.ShouldBindJSON(&input); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{"error": "invalid_request"}); return
    }
    user, err := service.Create(c.Request.Context(), input)
    if err != nil { c.Error(err); return }
    c.JSON(http.StatusCreated, user)
})
```

Use `ShouldBind...` when the handler owns response mapping; `Bind...` may write an automatic 400. Validate domain rules in service/domain layer too.

## Route groups and middleware

```go
api := r.Group("/api")
api.Use(requestID())
private := api.Group("/admin", requireAuth())
private.GET("/users", listUsers)
```

Middleware order follows registration. Avoid putting authentication on public routes accidentally; test both authorized and unauthorized paths.

## Abort and return errors

Use `c.AbortWithStatusJSON` in middleware when rejecting a request; always `return` afterward. A handler that calls `c.Error(err)` should have centralized middleware that logs/maps errors before response is committed.

## Test a handler

Use `httptest.NewRecorder`, create a request, call `r.ServeHTTP`, then assert status/body. Keep router construction injectable so tests avoid production network listeners.

## Read next

[[Go Recipes]] · [[Go HTTP Handler Boundaries]] · [[Go Error Handling]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
