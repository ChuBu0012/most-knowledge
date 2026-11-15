---
title: "How-To: ตรวจงานและเรนเดอร์เป็น MP4"
aliases:
  - hyperframes render
  - เรนเดอร์วิดีโอ
  - export mp4
  - hyperframes check
tags: [animation, hyperframes, how-to, render]
type: how-to
status: published
---

# ตรวจงานและเรนเดอร์เป็น MP4

รันในโฟลเดอร์โปรเจกต์ ตามลำดับ:

```bash
npx hyperframes lint             # 1. โครงสร้างไฟล์ถูกไหม
npx hyperframes check            # 2. ด่านหลัก: runtime, layout, contrast (ต้องไม่มี error)
npx hyperframes snapshot         # 3. ถ่ายภาพนิ่ง → ดูใน .hyperframes/artifacts/snapshots/
npx hyperframes preview          # 4. ดูจริงใน browser
```

## เรนเดอร์

```bash
npx hyperframes render --quality draft -o renders/draft.mp4       # ระหว่างแก้งาน (เร็ว)
npx hyperframes render --quality delivery -o renders/final.mp4    # ฉบับส่งจริง
```

ต้องการผลเหมือนกันทุกเครื่อง: เติม `--docker`

## ตรวจไฟล์ที่ได้

```bash
ffprobe -v error -show_entries format=duration -of csv=p=0 renders/final.mp4
```

ความยาวต้องตรงกับ `data-duration` ของ Composition — แล้ว **เปิดดูจริงทั้งคลิป**

มีปัญหา → [[Anim-Fix-Common-Problems]]

## ลึกกว่านี้

[[02 - HyperFrames & Rendering]] · [[05 - Prompting & Quality Control]] (QA Checklist)
