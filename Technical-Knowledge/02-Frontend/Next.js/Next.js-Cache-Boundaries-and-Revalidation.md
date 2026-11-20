---
title: "Next.js Cache Boundaries and Revalidation"
type: concept
domain: next.js
level: intermediate
tags: [nextjs, caching, rendering]
status: researched
last_verified: 2026-11-20
sources:
  - https://nextjs.org/docs/app/guides/caching
---

# Next.js Cache Boundaries and Revalidation

## Overview

cache ใน Next.js มีหลายชั้น; ต้องรู้ว่า cache อะไร อยู่ที่ไหน และข้อมูลของ user คนใดจึงจะไม่รั่วข้าม request

## Mental model

แยก request memoization, persistent data/cache, prerendered route output และ client router cache. Route handler/server component อาจทำงานใน request context; cache data ที่ขึ้นกับ session ต้อง scope ตาม identity หรือไม่ cache. Revalidation สามารถเกิดจาก time/tag/path ตาม feature ของรุ่นที่ใช้. Next 16.4 ปรับ Cache Components จึงใช้ migration docs ของ v16 โดยตรง

## Example

```ts
// แนวคิด: ระบุ cache key/tag จาก resource ที่ชัดเจน
const product = await fetch(url, {
  next: { revalidate: 60, tags: [`product:${id}`] },
});
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

cache key ขาด tenant/user dimension เป็นข้อมูลรั่ว; revalidate time ไม่ได้รับประกัน freshness ทันที; อย่าสมมติว่า route ทุกหน้า dynamic/static จาก pathname อย่างเดียว ตรวจ `use cache`/Cache Components ตาม Next major

## Practical guidance

ทำ cache inventory ต่อ data source: owner, key, lifetime, invalidation path, user scope. เขียน tests สำหรับ personalized responses และ mutation แล้ว revalidate tag/path ที่ผูกกับ resource

## Related knowledge

[[Next.js with TypeScript]] · [[React Server and Client Components]] · [[TanStack Query Cache Lifecycle]] · [[Cookie and Session Security]]

## References

- [nextjs.org](https://nextjs.org/docs/app/guides/caching)
