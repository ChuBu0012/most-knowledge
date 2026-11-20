---
title: "Express Middleware Ordering and Errors"
type: concept
domain: express
level: intermediate-to-advanced
tags: [express, middleware, nodejs]
status: researched
last_verified: 2026-11-20
sources:
  - https://expressjs.com/en/guide/using-middleware.html
  - https://expressjs.com/en/guide/error-handling.html
---

# Express Middleware Ordering and Errors

## Overview

Express application คือ stack ของ middleware/route handlers; ลำดับ `app.use()` เป็นส่วนหนึ่งของ behavior และ security

## How it works

middleware รับ `(req,res,next)`; เรียก `next()` ส่ง control ต่อ, `next(err)` ส่งเข้า error handler. Express 5 จัดการ rejected Promise จาก async handlers โดยส่งต่อ error. Error middleware มี 4 arguments และควรลงท้ายหลัง routes. Body parser ต้องมาก่อน handler ที่อ่าน parsed body

## Example

```bash
app.use(express.json({ limit: '1mb' }));
app.post('/users', async (req, res) => {
  const input = UserSchema.parse(req.body);
  const user = await users.create(input);
  res.status(201).json(user);
});
app.use((err, req, res, next) => {
  if (res.headersSent) return next(err);
  res.status(500).json({ error: 'internal_error' });
});
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

middleware ที่ route ก่อน security/auth อาจเปิด endpoint; parser ไม่มี body limit เพิ่ม DoS risk; Express 4 async rejection ต้อง wrapper/catch ส่วน Express 5 behavior ต่าง; error handler ห้ามส่ง stack/secret

## Production practices

จัด app factory, mount middleware ตาม boundary, normalize domain errors, redact logs และ integration test middleware order/headers/cors

## Related knowledge

[[Express]] · [[JavaScript Error Handling]] · [[HTTP Request Lifecycle]] · [[Zod Runtime Validation]]

## References

- [expressjs.com](https://expressjs.com/en/guide/using-middleware.html)
- [expressjs.com](https://expressjs.com/en/guide/error-handling.html)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
