---
title: "OAuth Authorization Code with PKCE"
type: concept
domain: oauth 2.0
level: intermediate-to-advanced
tags: [oauth, security, authorization]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.rfc-editor.org/rfc/rfc9700
---

# OAuth Authorization Code with PKCE

## Overview

flow สำหรับให้ client ขอ authorization ผ่าน authorization server โดยไม่รับรหัสผ่านของผู้ใช้โดยตรง

## กลไกและแนวคิดหลัก

client ส่งผู้ใช้ไป authorize endpoint พร้อม `state`, redirect URI และ PKCE `code_challenge`; หลัง consent server ส่ง short-lived authorization code กลับ redirect URI; client แลก code ที่ token endpoint พร้อม `code_verifier`. Authorization server ตรวจ challenge match. PKCE ป้องกันผู้ขโมย code แลก token ได้โดยไม่มี verifier. Native/mobile/browser clients เป็น public clients จึงไม่ควรฝัง client secret ที่อ่านได้ในแอป

## ตัวอย่าง

```text
// สร้างแบบสุ่มด้วย CSPRNG และเก็บ verifier ชั่วคราว
verifier = randomUrlSafeString();
challenge = BASE64URL(SHA256(verifier));
// ส่ง challenge ไป authorize endpoint
// แลก code + verifier ที่ token endpoint
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

`state` ป้องกัน CSRF/callback mix-up ใน client; PKCE ไม่ได้แทน state ทุก deployment. redirect URI ต้อง exact match. ตรวจ issuer, audience, nonce (เมื่อ OIDC), scope และ token audience. อย่าใช้ implicit flow หรือ password grant ในระบบใหม่

## แนวทางปฏิบัติ

ใช้ Authorization Code + PKCE; token สั้นอายุเท่าที่จำเป็น; ใช้ refresh-token rotation/revocation ตาม threat model; ทำ authorization check ที่ resource server

## ความสัมพันธ์

[[OAuth-2.0]] · [[HTTP Request Lifecycle]] · [[JWT Validation]] · [[Session-Management]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://www.rfc-editor.org/rfc/rfc9700)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
