---
title: "Playwright Locators and Auto-Waiting"
type: concept
domain: playwright
level: intermediate-to-advanced
tags: [playwright, e2e, testing]
status: researched
last_verified: 2026-11-20
sources:
  - https://playwright.dev/docs/locators
---

# Playwright Locators and Auto-Waiting

## Overview

Locator คือ query ที่ resolve element ณ เวลาสั่ง action/assertion; auto-wait ช่วยรอ actionability และ condition โดยไม่ต้อง sleep

## กลไกและแนวคิดหลัก

`getByRole`/label/text ใกล้ semantics ที่ผู้ใช้เห็น; `locator` จะหา element ตอนใช้ action ทำให้ทนต่อ rerender มากกว่าเก็บ ElementHandle เก่า. Assertions ของ Playwright retry จน timeout. Browser contexts แยก cookies/storage เพื่อ isolate tests

## ตัวอย่าง

```typescript
await page.getByRole('button', { name: 'Save' }).click();
await expect(page.getByRole('status')).toHaveText('Saved');
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

selector แบบ CSS ลึกผูกกับ implementation; `waitForTimeout` เพิ่ม flakiness; test ที่แชร์ account/data แข่งขันกันเมื่อ parallel; อย่าใช้ same browser context ข้ามผู้ใช้

## แนวทางปฏิบัติ

เลือก locator ตาม accessible name, สร้าง test data แยกต่อ test, เก็บ trace on failure และใช้ API setup เฉพาะเมื่อยังตรวจ UI journey จริง

## ความสัมพันธ์

[[Playwright]] · [[Unit Integration and End-to-End Tests]] · [[HTTP-Authentication]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://playwright.dev/docs/locators)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
