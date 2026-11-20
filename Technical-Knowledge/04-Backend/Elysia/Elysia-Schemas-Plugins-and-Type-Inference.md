---
title: "Elysia Schemas Plugins and Type Inference"
type: concept
domain: elysia
level: intermediate-to-advanced
tags: [elysia, bun, typescript]
status: researched
last_verified: 2026-11-20
sources:
  - https://elysiajs.com/essential/validation
  - https://next.elysiajs.com/blog/elysia-20-rc/
---

# Elysia Schemas Plugins and Type Inference

## Overview

Elysia ผูก route schema กับ validation, response typing และ inferred client types; plugin encapsulation ช่วยแบ่งขอบเขต dependency/routes

## How it works

route schema ระบุ body/params/query/response; derive/resolve hooks เหมาะกับค่าที่เตรียมก่อน handler. Plugin scope มีผลต่อ route registration และ lifecycle. Elysia 2 อยู่สถานะ RC ใน Oct 2026 และมี architecture/AOT changes จึงแยก v1/v2 APIs ตามเอกสาร

## Example

```typescript
const app = new Elysia()
  .post('/users', ({ body }) => createUser(body), {
    body: t.Object({ email: t.String({ format: 'email' }) }),
    response: t.Object({ id: t.String() }),
  });
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

อย่าเชื่อเพียง static inferred type สำหรับข้อมูล runtime; plugin ที่ register คนละ scope อาจไม่เห็น decorator; Elysia 2 RC API ไม่ควรนำไปผสมตัวอย่าง stable v1

## Production practices

ประกาศ input/response schemas ที่ route boundary, ใช้ plugin เพื่อแบ่ง module, test validation failures และระบุ Bun/Elysia version ใน lockfile

## Related knowledge

[[Elysia]] · [[Bun]] · [[TypeScript Type Narrowing]] · [[HTTP Semantics and REST]]

## References

- [elysiajs.com](https://elysiajs.com/essential/validation)
- [next.elysiajs.com](https://next.elysiajs.com/blog/elysia-20-rc/)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
