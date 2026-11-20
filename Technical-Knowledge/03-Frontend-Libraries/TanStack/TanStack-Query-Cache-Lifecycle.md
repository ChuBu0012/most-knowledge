---
title: "TanStack Query Cache Lifecycle"
type: concept
domain: tanstack query
level: intermediate
tags: [tanstack-query, cache, async]
status: researched
last_verified: 2026-11-20
sources:
  - https://tanstack.com/query/latest/docs/framework/react/guides/caching
---

# TanStack Query Cache Lifecycle

## Overview

TanStack Query เก็บผล query ตาม query key และจัดการ freshness, refetch, retries, observers และ invalidation แทนการผูก remote data กับ UI state เอง

## กลไกและแนวคิดหลัก

`queryKey` เป็น identity ของข้อมูลและต้องมีทุก input ที่มีผลต่อผล query; `staleTime` กำหนดช่วงที่ข้อมูลถือว่าสด; stale ไม่เท่ากับถูกลบ. Cache retention/GC ทำงานเมื่อไม่มี observer. Mutation ไม่เปลี่ยน cache ให้อัตโนมัติตาม domain: เลือก invalidate query ที่เกี่ยวข้องหรือ update cache อย่างแม่นยำ

## ตัวอย่าง

```typescript
const users = useQuery({
  queryKey: ['users', { page }],
  queryFn: ({ signal }) => fetchUsers({ page, signal }),
});
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

key กว้าง/ไม่ครบทำให้แสดงข้อมูลผิด; invalidation มากเกินทำให้ request storm; optimistic update ต้อง snapshot และ rollback เมื่อ mutation fail; query function ควรส่ง `signal` เพื่อยกเลิก request

## แนวทางใช้งาน

ให้ server state อยู่ใน query cache, ทำ query key factory กลาง และคิดเรื่อง pagination, auth scope, stale data และ invalidation หลัง mutation

## ความสัมพันธ์

[[JavaScript Promises]] · [[React State and Batching]] · [[TanStack-Table]] · [[TanStack-Router]] · [[Zod]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://tanstack.com/query/latest/docs/framework/react/guides/caching)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
