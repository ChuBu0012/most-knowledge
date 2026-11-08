---
title: Git Restore
tags:
  - git
  - undo
  - commands
type: tutorial
status: published
---

# Git Restore

`git restore` เปิดตัวใน Git 2.23 เพื่อเป็นคำสั่งเฉพาะทางสำหรับการ **คืนค่า (Restore) และยกเลิกการแก้ไขไฟล์** ออกแบบมาเพื่อทดแทนคำสั่ง `git checkout <file>` และ `git reset <file>` ในอดีต

---

## 1. สถาปัตยกรรมเป้าหมายของการ Restore

```mermaid
flowchart LR
    Commit[Commit ล่าสุด / HEAD]
    Index[Staging Area / Index]
    WT[Working Tree]

    Commit -- "git restore --staged <file>" --> Index
    Index -- "git restore <file>" --> WT
    Commit -- "git restore --source=HEAD <file>" --> WT
```

---

## 2. รูปแบบการใช้งานหลัก

### 2.1 ทิ้งการแก้ไขใน Working Tree (Discard Local Changes)
เมื่อคุณพิมพ์แก้โค้ดในไฟล์แล้วพบว่าผิดทาง และต้องการให้ไฟล์กลับไปเหมือนสถานะที่เซฟไว้ล่าสุด:
```bash
# คืนค่าเฉพาะไฟล์เดียว
git restore src/app.js

# คืนค่าไฟล์ทั้งหมดในโฟลเดอร์ปัจจุบัน
git restore .
```
> [!warning] การเปลี่ยนแปลงที่ยังไม่ได้บันทึกจะหายไปถาวร!
> โค้ดที่คุณพิมพ์ไปใน Working Tree ที่ยังไม่เคยสั่ง `git add` หรือ `git commit` มาก่อน จะถูกลบทิ้งไปและไม่สามารถกู้คืนได้

### 2.2 เอาไฟล์ออกจาก Staging Area (Unstaging)
เมื่อสั่ง `git add` เข้าไปแล้ว แต่อยากเอาออกจากคิวที่จะ Commit โดย **ยังคงรักษาโค้ดที่พิมพ์ไว้ใน Working Tree**:
```bash
git restore --staged src/app.js
```
สถานะของไฟล์จะเปลี่ยนจาก `Changes to be committed` กลับมาเป็น `Changes not staged for commit`

### 2.3 ดึงไฟล์เวอร์ชันจาก Commit ในอดีต
```bash
# ดึงเนื้อหาของไฟล์ utils.js จาก Commit รหัส a1b2c3d มาทับลงใน Working Tree
git restore --source=a1b2c3d src/utils.js
```

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-Reset]] — คำสั่งย้อนประวัติศาสตร์ที่ครอบคลุม Commit
- [[Undo-Command-Comparison]] — สรุปตารางเปรียบเทียบการ Undo\n