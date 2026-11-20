---
title: "Nuxt Data Fetching and Request Context"
type: concept
domain: nuxt
level: intermediate
tags: [nuxt, data-fetching, ssr]
status: researched
last_verified: 2026-11-20
sources:
  - https://nuxt.com/docs/4.x/getting-started/data-fetching
---

# Nuxt Data Fetching and Request Context

## Overview

Nuxt มี composables สำหรับโหลดข้อมูลใน lifecycle ที่รองรับ SSR, hydration และ deduplication; เลือกให้ตรงว่า data ต้องอยู่ฝั่ง server, client หรือทั้งสอง

## Mental model

`useFetch`/`useAsyncData` ถูกออกแบบให้ผลลัพธ์เชื่อมกับ Nuxt payload เพื่อไม่ยิงซ้ำโดยไม่จำเป็นระหว่าง SSR/hydration; `$fetch` เป็น raw request helper และเรียกซ้ำได้ถ้าใช้ตรงใน component setup. Server API ใช้ event/request context; runtime config แยก public/private values

## Example

```ts
const { data, pending, error, refresh } = await useFetch('/api/products', {
  key: 'products:index',
});
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

อย่าแชร์ mutable user-specific data ผ่าน module singleton ใน SSR; อย่า expose private runtime config; อย่าใช้ `$fetch` ใน setup แทน data composable โดยไม่จัดการ SSR duplicate request; server route ยังต้อง authorize

## Practical guidance

กำหนด stable key/params, ส่ง auth/request context อย่างปลอดภัย, แยก public/private config, และตรวจ cache headers กับ tenant isolation

## Related knowledge

[[Nuxt]] · [[Nitro]] · [[Vue Composables]] · [[Cookie and Session Security]] · [[HTTP Request Lifecycle]]

## References

- [nuxt.com](https://nuxt.com/docs/4.x/getting-started/data-fetching)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
