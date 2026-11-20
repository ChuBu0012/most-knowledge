---
title: "Cookie and Session Security"
type: concept
domain: http
level: intermediate-to-advanced
tags: [security, cookies, sessions]
status: researched
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Cookies
---

# Cookie and Session Security

## Overview

session cookie เป็น bearer credential ที่เชื่อม browser กับ server-side session; ผู้ขโมย cookie อาจสวมรอยผู้ใช้ได้

## กลไกและแนวคิดหลัก

สร้าง session ID แบบสุ่ม entropy สูง เก็บเฉพาะ ID ใน cookie และเก็บ state/revocation ฝั่ง server. ตั้ง `Secure`, `HttpOnly`, `SameSite` และ Path/Domain แบบจำกัด; rotate session หลัง login/privilege change. SameSite ลด CSRF บางรูปแบบแต่ไม่ได้แทน CSRF strategy ทุกกรณี

## ตัวอย่าง

```http
Set-Cookie: __Host-session=<opaque-random-id>; Path=/; Secure; HttpOnly; SameSite=Lax
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

ห้ามวาง session identifier ใน URL/localStorage โดยไม่มี threat model; logout ต้อง invalidate server state; ป้องกัน fixation ด้วย rotation; ตั้ง proxy/TLS ให้ถูกก่อนเชื่อ secure-cookie flags

## แนวทางปฏิบัติ

ใช้ short idle/absolute expiry ตามความเสี่ยง, CSRF token/origin check สำหรับ unsafe requests, rate limit login และ redact credentials จาก logs

## ความสัมพันธ์

[[Session-Management]] · [[HTTP-Authentication]] · [[OAuth Authorization Code with PKCE]] · [[Nginx]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Cookies)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
