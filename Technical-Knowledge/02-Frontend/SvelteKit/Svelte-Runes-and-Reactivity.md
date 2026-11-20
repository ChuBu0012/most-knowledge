---
title: "Svelte Runes and Reactivity"
type: concept
domain: sveltekit
level: intermediate
tags: [svelte, reactivity]
status: researched
last_verified: 2026-11-20
sources:
  - https://svelte.dev/docs/svelte/what-are-runes
---

# Svelte Runes and Reactivity

## Overview

Svelte compiler แปลง component ให้ updates ทำงานตาม reactive dependencies; Svelte 5 ใช้ runes แสดง state/derived/effect อย่างชัดเจน

## กลไกและแนวคิดหลัก

`$state` ระบุ state ที่เปลี่ยนได้, `$derived` คำนวณจาก dependencies, `$effect` เชื่อมกับ side effect. Runes เป็น compiler syntax ที่ใช้ใน script ไม่ใช่ runtime function ทั่วไป. SvelteKit เพิ่ม server/client routing และ load lifecycle รอบ component

## ตัวอย่าง

```svelte
let count = $state(0);
let doubled = $derived(count * 2);
function increment() { count += 1; }
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

ใช้ `$effect` เป็นที่รวม derived state ทั้งหมดจะสร้าง dependency loop และ code ที่ยาก debug; อย่าสับสน legacy `$:` syntax กับ rune mode ใน project ที่ยังผสมอยู่

## แนวทางใช้งาน

ใช้ derived สำหรับค่า UI, effect เฉพาะ integration ภายนอก, และแยก state ที่ต้องอยู่ฝั่ง server ออกจาก client state

## ความสัมพันธ์

[[SvelteKit]] · [[Vite]] · [[Playwright]] · [[TypeScript]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://svelte.dev/docs/svelte/what-are-runes)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
