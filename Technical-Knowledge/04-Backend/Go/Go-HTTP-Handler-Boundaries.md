---
title: "Go HTTP Handler Boundaries"
type: concept
domain: go
level: intermediate-to-advanced
tags: [go, http, backend]
status: researched
last_verified: 2026-11-20
sources:
  - https://pkg.go.dev/net/http
---

# Go HTTP Handler Boundaries

## Overview

HTTP handler เป็น boundary ระหว่าง untrusted request กับ domain logic; แยก parse/validate, authorization, use case และ response mapping

## How it works

handler รับ method/path/header/body; parse body ด้วย size limit, validate input แล้วเรียก service พร้อม context. Domain layer คืน typed result/error; transport layer แปลงเป็น status/headers/JSON. Gin/Fiber สะดวกกับ routing/middleware แต่ behavior/context API แตกต่างกัน ต้องอ่าน framework-specific docs

## Example

```go
func createUser(w http.ResponseWriter, r *http.Request) {
  ctx := r.Context()
  var input CreateUserInput
  if err := json.NewDecoder(io.LimitReader(r.Body, 1<<20)).Decode(&input); err != nil {
    http.Error(w, "invalid request", http.StatusBadRequest); return
  }
  user, err := service.Create(ctx, input)
  if err != nil { writeError(w, err); return }
  writeJSON(w, http.StatusCreated, user)
}
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

อย่า bind body แบบไม่จำกัด; อย่าส่ง database error/stack trace กลับ client; ตรวจ authz ในแต่ละ resource action; Fiber context ไม่ใช่ `context.Context` โดยตรงทุกกรณี

## Production practices

ให้ transport handler บาง, ส่ง `context.Context` ไป downstream, ทำ error mapping กลาง, เพิ่ม request ID/structured logs และ integration test สำหรับ status/headers

## Related knowledge

[[Go]] · [[Gin]] · [[Fiber]] · [[Go Error Handling]] · [[Go Context]] · [[HTTP Semantics and REST]]

## References

- [pkg.go.dev](https://pkg.go.dev/net/http)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
