---
title: "Hono Middleware and Request Validation"
type: concept
domain: hono
level: intermediate-to-advanced
tags: [hono, middleware, validation]
status: researched
last_verified: 2026-11-20
sources:
  - https://hono.dev/docs/guides/middleware
  - https://hono.dev/docs/guides/validation
---

# Hono Middleware and Request Validation

## Overview

Hono ใช้ middleware chain รอบ handler; request validation ควรเกิดก่อน logic ที่พึ่งข้อมูลนั้น และ middleware order มีผลต่อ auth/logging/errors

## How it works

แต่ละ middleware รับ context และ `next`; สามารถตั้งค่าที่ส่งต่อไป handler หรือหยุดตอบ response ได้. Hono validator middleware แปลง input ที่ตรวจแล้วให้ handler อ่าน typed data; runtime adapter ให้ APIs ต่างกัน จึงต้องเลือก adapter ที่ตรง platform

## Example

```typescript
const app = new Hono();
app.use('/api/*', requestId());
app.post('/users', zValidator('json', schema), c => {
  const body = c.req.valid('json');
  return c.json({ id: createUser(body) }, 201);
});
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

Hono 4.13.18 security fixes แสดงว่าควรอัปเดต middleware; อย่าเรียก `c.req.json()` แล้วใช้ raw data ซ้ำแทน validated result; จำกัด request body และตรวจ authz ก่อน data access

## Production practices

เรียง middleware: error/observability → request ID → security/cors → authn/authz → validation → handler; ทดสอบด้วย `app.request()` และ adapter integration

## Related knowledge

[[Hono]] · [[HTTP Request Lifecycle]] · [[Zod Runtime Validation]] · [[OAuth-2.0]]

## References

- [hono.dev](https://hono.dev/docs/guides/middleware)
- [hono.dev](https://hono.dev/docs/guides/validation)
