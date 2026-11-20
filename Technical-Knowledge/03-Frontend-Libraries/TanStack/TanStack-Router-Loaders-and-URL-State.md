---
title: "TanStack Router Loaders and URL State"
type: concept
domain: tanstack router
level: intermediate
tags: [routing, frontend, url-state]
status: researched
last_verified: 2026-11-20
sources:
  - https://tanstack.com/router/latest/docs/framework/react/guide/data-loading
---

# TanStack Router Loaders and URL State

## Overview

Router loader ผูกการโหลดข้อมูลกับ route match และ URL state ช่วยให้ deep link, back/forward และ refresh สะท้อนหน้าจอเดียวกัน

## กลไกและแนวคิดหลัก

search params เป็น input ที่ผู้ใช้แก้ได้ จึงควร validate/coerce ด้วย schema ก่อนนำไปใช้. Loader รับ route params/search, preload data ก่อน render, และสามารถทำงานร่วม query cache. Route tree มี type inference จากการลงทะเบียน router. URL state เหมาะกับ filter/page/sort ที่ควรแชร์ลิงก์

## ตัวอย่าง

```tsx
const Route = createFileRoute('/products')({
  validateSearch: zodValidator(z.object({ page: z.number().catch(1) })),
  loaderDeps: ({ search }) => ({ page: search.page }),
  loader: ({ context, deps }) => context.queryClient.ensureQueryData(
    productsQueryOptions(deps.page)
  ),
});
```

ตัวอย่างเป็น schematic; adapter/package imports และ API ต้องตรงกับ version ที่ใช้จริง

## จุดพลาดและข้อควรระวัง

อย่าใส่ sensitive data ใน URL; validate query string เพราะ input ไม่ trusted; ระวัง duplicate fetch ระหว่าง loader กับ component ถ้า query key ไม่ตรง; navigation cancellation ต้องส่ง signal ลง fetch

## แนวทางปฏิบัติ

ให้ URL เป็น source of truth สำหรับ state ที่ต้อง deep-link; ใช้ query cache สำหรับ remote data และกำหนด error/not-found boundary ใน route

## ความสัมพันธ์

[[TanStack-Router]] · [[TanStack Query Cache Lifecycle]] · [[Zod Runtime Validation]] · [[HTTP Semantics and REST]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://tanstack.com/router/latest/docs/framework/react/guide/data-loading)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
