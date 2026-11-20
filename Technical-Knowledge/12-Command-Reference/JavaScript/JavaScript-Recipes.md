---
title: "JavaScript Recipes"
type: reference
domain: javascript
tags: [technical-knowledge, api-reference, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript
---

# JavaScript Recipes

คู่มือค้นจากงานที่ต้องทำ ตัวอย่างมุ่งที่ API/คำสั่งที่ใช้บ่อย; ตรวจ runtime/compiler version ในโปรเจกต์ก่อนใช้

## สร้างตัวแปรและฟังก์ชัน

```js
const taxRate = 0.07; // binding เปลี่ยนไม่ได้
let total = 0;         // reassign ได้
function addTax(price) { return price * (1 + taxRate); }
const double = value => value * 2;
```

ใช้ `const` เป็นค่าเริ่มต้น; object ที่ประกาศด้วย const ยังแก้ property ได้. ใช้ `let` เมื่อจำเป็นต้อง reassign; หลีกเลี่ยง `var` เพราะ function scope/hoisting ทำให้อ่านยาก.

## แปลงและตรวจข้อมูล

```js
const n = Number(input);
if (!Number.isFinite(n)) throw new TypeError('Expected a finite number');
const label = String(value ?? '');
const isRecord = value => value !== null && typeof value === 'object' && !Array.isArray(value);
```

`typeof null === 'object'`; ตรวจ null ก่อน. TypeScript type ไม่ได้ตรวจข้อมูลจาก network ระหว่าง runtime—parse/validate boundary.

## จัดการ array

```js
const activeNames = users.filter(user => user.active).map(user => user.name);
const byId = new Map(users.map(user => [user.id, user]));
const total = prices.reduce((sum, price) => sum + price, 0);
```

เลือก `map` เมื่อ output มีจำนวนสมาชิกเท่าเดิม, `filter` เมื่อต้องคัด, `reduce` เมื่อต้องรวม accumulator. อย่าใช้ reduce ซ้อนซับซ้อนแทน loop ที่อ่านง่าย.

## ทำงาน async

```js
async function loadUser(id, signal) {
  const response = await fetch(`/api/users/${encodeURIComponent(id)}`, { signal });
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return response.json();
}
try { const user = await loadUser('u1'); } catch (error) { /* report/recover */ }
```

`fetch` ไม่ reject แค่เพราะ HTTP 404/500; เช็ค `response.ok`. ใช้ `Promise.all` เมื่องานอิสระและต้องรอทั้งหมด; `Promise.allSettled` เมื่อต้องเก็บผลทุกงานแม้บางงานล้มเหลว.

## แบ่ง module

```js
// math.js
export const clamp = (value, min, max) => Math.min(max, Math.max(min, value));
// app.js
import { clamp } from './math.js';
```

ระบุ extension ตาม environment ที่ต้องการ; Node/browser module resolution อาจต่างกัน. อย่าอ่านไฟล์ที่มี side effects ผ่าน import โดยไม่รู้ผลตอนโหลด.

## ทำงานกับ object โดยไม่ mutate ต้นฉบับ

```js
const renamed = { ...user, name: 'Ada' };
const next = items.map(item => item.id === targetId ? { ...item, done: true } : item);
```

Spread copy เพียง shallow; nested object ยังอ้างอิงตัวเดิม. ใช้ structuredClone เฉพาะข้อมูลที่รองรับและต้อง deep-copy จริง; อย่าใช้ JSON stringify เป็น universal clone.

## ดูแล resource

```js
const controller = new AbortController();
try { await fetch(url, { signal: controller.signal }); } finally { controller.abort(); }
```

ยกเลิก fetch เมื่อผู้ใช้เปลี่ยนหน้า/ยกเลิกงาน; ปิด stream/socket/timer/listener ตาม lifecycle เพื่อไม่ให้ leak.

## ค้นต่อ

[[JavaScript Execution Model]] · [[JavaScript Promises]] · [[JavaScript Modules]] · [[JavaScript Error Handling]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
