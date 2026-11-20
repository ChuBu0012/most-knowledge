---
title: "Bun Runtime Compatibility and Deployment"
type: concept
domain: bun
level: intermediate-to-advanced
tags: [bun, runtime, javascript]
status: researched
last_verified: 2026-11-20
sources:
  - https://bun.sh/blog/bun-v1.4.4
  - https://bun.sh/docs/runtime/bun-apis
---

# Bun Runtime Compatibility and Deployment

## Overview

Bun รวม JavaScript runtime, package manager, test runner และ bundler; การแทน Node.js ต้องตรวจ API, package/native dependency และ operational behavior ทีละส่วน

## How it works

Bun ใช้ JavaScriptCore; มี Node compatibility layer และ Web APIs แต่ compatibility ไม่ได้เท่ากับ Node ทุก API/version. `bun.lock`/install modes กำหนด dependency resolution; `Bun.serve` ใช้ Request/Response model และ server lifecycle. รุ่น 1.4 เพิ่ม HTTP/2 แต่ protocol feature flags ต้องตั้งและทดสอบโดยตรง

## Example

```typescript
const server = Bun.serve({
  port: 3000,
  fetch(req) {
    const url = new URL(req.url);
    return Response.json({ path: url.pathname });
  },
});
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

อย่าตัด Node ออกจาก production pipeline ก่อนตรวจ native addons, subprocess, TLS roots, inspector, memory limits และ graceful shutdown; HTTP/2/3 ยังมี feature caveats ตาม release notes

## Production practices

รักษา lockfile, pin runtime/container image, run tests บน runtime จริงและ Node ที่อาจต้องรองรับ, monitor RSS/latency และทำ shutdown drain

## Related knowledge

[[Bun]] · [[JavaScript Execution Model]] · [[Docker Image Layers and Reproducible Builds]] · [[Playwright Locators and Auto-Waiting]]

## References

- [bun.sh](https://bun.sh/blog/bun-v1.4.4)
- [bun.sh](https://bun.sh/docs/runtime/bun-apis)
