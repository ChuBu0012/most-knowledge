---
title: Daily Git Commands
tags:
  - git
  - commands
  - essential
type: tutorial
status: published
---

# Daily Git Commands

ในกระบวนการพัฒนาซอฟต์แวร์จริง นักพัฒนาใช้คำสั่ง Git เพียงประมาณ 10 คำสั่งเป็นประจำทุกวัน หน้านี้รวบรวมคำสั่งเหล่านั้น พร้อมอธิบายบริบทและเหตุผลในการเรียกใช้

---

## 1. แผนผังคำสั่งประจำวัน (Daily Command Flow)

```mermaid
flowchart TD
    Start([เริ่มงานตอนเช้า]) --> Fetch[git fetch / git pull]
    Fetch --> Branch[git switch -c feature/new-task]
    Branch --> Code[เขียนโค้ด / แก้ไขไฟล์]
    Code --> Status[git status / git diff]
    Status --> Add[git add <file>]
    Add --> Commit[git commit -m "..."]
    Commit --> MoreWork{ทำงานต่อใน Branch นี้ไหม?}
    MoreWork -- ใช่ --> Code
    MoreWork -- ไม่/เสร็จแล้ว --> Push[git push -u origin feature/new-task]
    Push --> PR[เปิด Pull Request บน GitHub]
```

---

## 2. เจาะลึกคำสั่งประจำวัน

### 2.1 `git status` — เรดาร์ตรวจสอบสถานการณ์
- **ใช้ทำอะไร:** ตรวจสอบว่า Branch ปัจจุบันคืออะไร, มีไฟล์ใด Modified, Staged หรือ Untracked อยู่บ้าง
- **เมื่อใดที่ควรใช้:** รันบ่อยที่สุดเท่าที่ทำได้ ทั้งก่อนแก้โค้ด, ก่อน `git add`, หลัง `git add`, และก่อน `git commit`
```bash
git status
# หรือแบบย่อ (Short format)
git status -s
```

### 2.2 `git diff` — ตรวจสอบสายตาเนื้อโค้ด
- **ใช้ทำอะไร:** เปรียบเทียบความต่างของโค้ดบรรทัดต่อบรรทัด
```bash
# ดูความต่างระหว่าง Working Tree กับ Staging Area (สิ่งที่ยังไม่ได้ add)
git diff

# ดูความต่างระหว่าง Staging Area กับ Commit ล่าสุด (สิ่งที่กำลังจะ commit)
git diff --staged
```

### 2.3 `git add` — คัดเลือกวัตถุดิบเข้าตะกร้า
```bash
# เพิ่มเฉพาะไฟล์
git add src/app.js

# เพิ่มทุกไฟล์ที่มีการเปลี่ยนแปลงในไดเรกทอรีปัจจุบัน
git add .
```

### 2.4 `git commit` — กดชัตเตอร์บันทึกประวัติ
```bash
git commit -m "fix(api): handle null response in user profile"
```

### 2.5 `git log` — ดูประวัติย้อนหลัง
```bash
# แสดงแบบบรรทัดเดียวพร้อมแผนผังกิ่ง
git log --oneline --graph --decorate -n 10
```

---

## 3. ตัวอย่างสถานการณ์จำลองใน 1 วัน (Real-world Scenario)

```bash
# 1. ซิงค์โค้ดล่าสุดจากทีม
git switch main
git pull origin main

# 2. แยกกิ่งไปทำงานฟีเจอร์ใหม่
git switch -c feature/cart-checkout

# 3. แก้ไขไฟล์ Cart.js และเพิ่ม Test ใน Cart.test.js
# ... แก้ไขโค้ด ...

# 4. ตรวจสอบสิ่งที่แก้
git status
git diff

# 5. นำเข้า Staging Area
git add src/Cart.js tests/Cart.test.js

# 6. บันทึก Commit
git commit -m "feat(cart): calculate discount vouchers correctly"

# 7. ส่งขึ้น Remote เพื่อเตรียมส่ง Review
git push -u origin feature/cart-checkout
```

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-Add-and-Staging]] — รายละเอียดกลไกการ Add
- [[Git-Commit]] — รูปแบบ Commit Message มาตรฐาน
- [[Git-Diff]] — เทคนิคการอ่าน Diff ขั้นสูง\n