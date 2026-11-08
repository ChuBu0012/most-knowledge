---
title: Branch Commands
tags:
  - git
  - branching
  - commands
type: tutorial
status: published
---

# Branch Commands

คู่มือการจัดการ Branch ด้วยชุดคำสั่งยุคใหม่ (`git switch`, `git branch`) และคำสั่งดั้งเดิม (`git checkout`)

---

## 1. การเปลี่ยนผ่านคำสั่ง: `git checkout` สู่ `git switch`

ในอดีต คำสั่ง `git checkout` ทำหน้าที่หนักเกินไป (Overloaded) เพราะใช้ทั้งการสลับ Branch และการยกเลิกการแก้ไขไฟล์ใน Working Tree ซึ่งสร้างความสับสนอย่างมาก

ตั้งแต่ Git เวอร์ชัน 2.23 เป็นต้นมา มีการแยกคำสั่งออกเป็น 2 คำสั่งที่ชัดเจน:
- `git switch` — ใช้สำหรับ **สลับและสร้าง Branch เท่านั้น**
- `git restore` — ใช้สำหรับ **กู้คืนและยกเลิกการเปลี่ยนแปลงของไฟล์**

> [!tip] คำแนะนำ
> ควรใช้ `git switch` แทน `git checkout` สำหรับงานจัดการ Branch ทั้งหมดเพื่อความชัดเจนและป้องกันการเผลอเขียนทับไฟล์โดยไม่ตั้งใจ

---

## 2. คำสั่งจัดการ Branch ในชีวิตจริง

### 2.1 แสดงรายการ Branch
```bash
# แสดง Local Branches ทั้งหมด (* ชี้กิ่งปัจจุบัน)
git branch

# แสดงทั้ง Local และ Remote-tracking Branches พร้อม Commit ล่าสุด
git branch -a -v
```

### 2.2 สร้างและสลับ Branch
```bash
# สร้าง Branch ใหม่แต่ยังอยู่ที่เดิม
git branch feature/payment

# สลับไปยัง Branch ที่มีอยู่แล้ว
git switch feature/payment

# สร้าง Branch ใหม่และสลับไปทันทีในคำสั่งเดียว (นิยมที่สุด)
git switch -c feature/shopping-cart

# เทียบเท่าคำสั่งยุคเก่า
git checkout -b feature/shopping-cart
```

### 2.3 การเปลี่ยนชื่อ Branch
```bash
# เปลี่ยนชื่อ Branch ที่เรากำลังยืนอยู่
git branch -m feature/cart-v2

# เปลี่ยนชื่อ Branch อื่น
git branch -m old-name new-name
```

### 2.4 การลบ Branch
```bash
# ลบ Branch ที่ผสาน (Merge) เข้ากิ่งหลักเรียบร้อยแล้วอย่างปลอดภัย
git branch -d feature/shopping-cart

# บังคับลบ Branch ทิ้ง แม้จะมี Commit ที่ยังไม่ได้ Merge (Force Delete)
git branch -D feature/abandoned-idea
```

---

## 3. ตัวอย่างการทำงานจริง (Step-by-Step)

```bash
# 1. เริ่มจากกิ่งหลักที่สะอาด
git switch main
git pull

# 2. แตกกิ่งใหม่ไปทำฟีเจอร์ Login
git switch -c feature/auth-login

# 3. ทำงานและ Commit โค้ด
git add .
git commit -m "feat(auth): add google oauth provider"

# 4. สลับกลับมาตรวจกิ่งหลัก
git switch main

# 5. เมื่อตรวจเสร็จ สลับกลับไปทำต่อ
git switch feature/auth-login
```

---

## 4. ปัญหาที่พบบ่อย (Troubleshooting)

### อาการ: สั่ง `git switch other-branch` ไม่สำเร็จ มีข้อผิดพลาด `error: Your local changes to the following files would be overwritten by checkout`
- **Cause:** มีไฟล์ใน Working Tree ถูกแก้ไขค้างไว้ และไฟล์เหล่านั้นมีความขัดแย้งกับโค้ดใน Branch ปลายทาง
- **Solution:**
  1. Commit การเปลี่ยนแปลงนั้นเสียก่อน หากงานพร้อมบันทึก
  2. หรือพักงานไว้ชั่วคราวด้วย `git stash` แล้วค่อยสลับกิ่ง
  3. หรือหากไม่ต้องการการเปลี่ยนแปลงนั้นแล้ว ให้ทิ้งด้วย `git restore .`
- **Prevention:** ตรวจสอบ `git status` ให้ Working Tree สะอาดก่อนสลับกิ่งเสมอ หรือใช้ [[Worktree-Concept]] เพื่อเปิดสองกิ่งพร้อมกันโดยไม่ต้องสลับ!

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Branch-Concept]] — ความเข้าใจเชิงทฤษฎีเรื่อง Pointer
- [[Detached-HEAD]] — การรับมือสภาวะ Detached HEAD
- [[Worktree-Concept]] — การทำงานพร้อมกันหลายกิ่งโดยไม่ต้องสลับไปมา\n