---
title: "Nginx Reverse Proxy Request Flow"
type: concept
domain: nginx
level: intermediate-to-advanced
tags: [nginx, proxy, networking]
status: researched
last_verified: 2026-11-20
sources:
  - https://nginx.org/en/docs/http/ngx_http_proxy_module.html
---

# Nginx Reverse Proxy Request Flow

## Overview

reverse proxy รับ request จาก client แล้วส่งต่อ backend; ใช้ TLS termination, routing, buffering และ load balancing ได้

## กลไกและแนวคิดหลัก

`location` จับ path แล้ว `proxy_pass` ส่ง request. Nginx ควรกำหนด Host/forwarded headers ที่เชื่อถือได้, upstream timeout, body limits และ buffering ตามประเภทงาน. Client-supplied `X-Forwarded-*` ไม่ควรถูกเชื่อโดยตรง; proxy ต้อง overwrite/append เฉพาะ trusted chain

## ตัวอย่าง

```nginx
location /api/ {
  proxy_pass http://api:8080/;
  proxy_set_header Host $host;
  proxy_set_header X-Real-IP $remote_addr;
  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  proxy_set_header X-Forwarded-Proto $scheme;
}
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

slash ท้าย `location`/`proxy_pass` เปลี่ยน URI rewrite semantics; forwarded host/proto ที่ spoof ได้ทำให้ auth redirect/CSRF checks ผิด; timeout สั้นไปตัดงานยาว ส่วน timeout ยาวเกินกิน connection

## แนวทางปฏิบัติ

จำกัด trusted proxy hops, เปิด TLS และ security headers ที่ edge, ตรวจ `nginx -t` ก่อน reload และติดตาม upstream response time/status

## ความสัมพันธ์

[[Nginx]] · [[HTTP Request Lifecycle]] · [[Docker-Compose-Service-Networking-and-Health]] · [[OAuth-2.0]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://nginx.org/en/docs/http/ngx_http_proxy_module.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
