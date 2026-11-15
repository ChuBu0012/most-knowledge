---
title: "How-To: เตรียมเครื่องและสร้างโปรเจกต์วิดีโอใหม่ (HyperFrames)"
aliases:
  - hyperframes init
  - เริ่มโปรเจกต์วิดีโอ
  - ติดตั้ง hyperframes
  - setup animation
tags: [animation, hyperframes, how-to]
type: how-to
status: published
---

# เตรียมเครื่องและสร้างโปรเจกต์ใหม่

## 1. เช็กเครื่อง (ครั้งแรกครั้งเดียว)

```bash
node --version      # ต้อง v22 ขึ้นไป
ffmpeg -version     # ไม่มี → brew install ffmpeg
npx hyperframes doctor
```

Chrome มีปัญหา → `npx hyperframes browser ensure`

## 2. สร้างโปรเจกต์

```bash
npx hyperframes init my-video
cd my-video
```

## 3. เปิดดู

```bash
npx hyperframes preview
```

เปิด URL ที่แสดงใน Browser จะเห็นตัวเล่นพร้อม Scrub bar

## ต่อไป

ให้ Claude สร้างวิดีโอ → [[Anim-Make-Video-with-Claude]]

## ลึกกว่านี้

[[02 - HyperFrames & Rendering]] — ทำไมต้อง Deterministic, โครงสร้าง Composition
