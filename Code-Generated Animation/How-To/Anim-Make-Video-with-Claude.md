---
title: "How-To: สั่ง Claude ทำวิดีโอ ตั้งแต่ไอเดียจนได้ MP4"
aliases:
  - ทำวิดีโอด้วย claude
  - prompt ทำ animation
  - explainer video
  - สั่ง ai ทำคลิป
tags: [animation, prompting, how-to]
type: how-to
status: published
---

# สั่ง Claude ทำวิดีโอ ตั้งแต่ไอเดียจนได้ MP4

> หลักเดียว: **อย่าสั่งทั้งเรื่องในครั้งเดียว** ทำทีละขั้น ตรวจก่อนไปต่อ
> เปิด Claude Code ในโฟลเดอร์โปรเจกต์ (ทำ [[Anim-Setup-New-Project]] ก่อน)

Copy prompt แต่ละขั้น แก้ส่วนใน `<...>` แล้วส่ง:

## ขั้น 1 — ล็อกเรื่องก่อน (ยังไม่เขียนโค้ด)

```text
ใช้ /hyperframes ช่วยทำวิดีโอ <ความยาว เช่น 30 วินาที> แนวตั้ง 1080x1920
หัวข้อ: <เรื่องอะไร>
คนดูต้องเข้าใจ: <1 ประโยค>
ยังไม่ต้องเขียนโค้ด ให้เขียน storyboard.md: แบ่งฉาก เวลาแต่ละฉาก ภาพหลัก ข้อความบนจอ และ VO
```

✅ ตรวจ: อ่าน storyboard แล้วแก้จนพอใจ

## ขั้น 2 — ทดสอบสไตล์ 6 วินาที

```text
ทำแค่ฉากแรก 6 วินาที ในสไตล์ <เช่น flat vector สีพาสเทล / isometric / dark tech>
เขียน style-guide.md (สี ฟอนต์ กติกาการเคลื่อนไหว) แล้ว snapshot ให้ดู
```

✅ ตรวจ: ดูภาพ snapshot ถ้าไม่ชอบ แก้สไตล์ตอนนี้ (ถูกที่สุด)
เลือกสไตล์ไม่ถูก → [[04 - Animation Styles]]

## ขั้น 3 — ทำทีละฉาก

```text
ทำฉากที่ <N> ตาม storyboard และ style-guide แล้วรัน lint + check และ snapshot กลางฉาก
```

ทำซ้ำจนครบทุกฉาก

## ขั้น 4 — รวมและเรนเดอร์

```text
รวมทุกฉากใน index.html รัน check --json แก้ error ให้หมด
แล้ว render --quality draft ให้ดูก่อน
```

✅ ดูคลิป draft จริงทั้งเรื่อง แก้จุดที่ไม่ชอบ แล้วสั่ง `render --quality delivery`

ตรวจ/เรนเดอร์ด้วยตัวเอง → [[Anim-Check-and-Render]]

## ลึกกว่านี้

- [[05 - Prompting & Quality Control]] — Master Prompt ฉบับเต็ม + QA Checklist
- [[01 - Production Workflow]] — 8 ขั้นการผลิต, โครงสร้างโฟลเดอร์
