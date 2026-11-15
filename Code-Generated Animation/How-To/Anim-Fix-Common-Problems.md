---
title: "How-To: แก้ปัญหาวิดีโอที่เจอบ่อย"
aliases:
  - animation ไม่ขยับ
  - render ออกมาจอดำ
  - วิดีโอกระตุก
  - hyperframes error
tags: [animation, hyperframes, how-to, troubleshooting]
type: how-to
status: published
---

# แก้ปัญหาวิดีโอที่เจอบ่อย

| อาการ | สาเหตุที่พบบ่อย | แก้ |
|---|---|---|
| Preview ขยับ แต่ MP4 นิ่ง | Timeline ไม่ได้ `paused: true` หรือไม่ได้ push เข้า `window.__timelines` | ดูตัวอย่างโค้ดด้านล่าง |
| เรนเดอร์แต่ละรอบไม่เหมือนกัน / กระตุก | ใช้ `Date.now()`, `setInterval`, `requestAnimationFrame`, `Math.random()` | ผูกทุกการเคลื่อนไหวกับ GSAP timeline, random ใช้ค่าคงที่ |
| บางเฟรมรูป/ฟอนต์หาย | โหลด asset กลางเรื่อง | Preload ทุกอย่างตั้งแต่ต้น |
| คลิปยาวผิด | `data-duration` ไม่ตรง | แก้ที่ root element |
| `check` บอก contrast fail | ตัวหนังสือกลืนพื้นหลัง | ใช้สีตาม `suggestedColor` ที่ check แนะนำ |
| Chrome เปิดไม่ได้ | browser ไม่ครบ | `npx hyperframes browser ensure` |
| ฉากย่อยขึ้นเล็กจิ๋ว / ไม่มี | sub-composition mount ผิด | สั่ง Claude: "snapshot กลางทุกฉากแล้วแก้ฉากที่ mount ผิด" |

## Timeline ที่ถูกต้อง

```javascript
const tl = gsap.timeline({ paused: true });
tl.to("#box", { x: 500, duration: 2 });
window.__timelines = window.__timelines || [];
window.__timelines.push(tl);
```

## สั่ง Claude แก้ให้

```text
รัน npx hyperframes check --json แล้วแก้ทุก error จากนั้น snapshot ให้ดูว่าแก้แล้ว
```

## ลึกกว่านี้

[[02 - HyperFrames & Rendering]] (กฎ Deterministic 6 ข้อ) · [[05 - Prompting & Quality Control]] (9 ข้อผิดพลาดที่พบบ่อย)
