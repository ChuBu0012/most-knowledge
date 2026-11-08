---
title: Worktree Commands
tags:
  - git
  - worktree
  - commands
type: tutorial
status: published
---

# Worktree Commands

คู่มือการใช้งานคำสั่งตระกูล `git worktree` ในชีวิตประจำวัน ตั้งแต่การสร้าง สลับ ตรวจสอบ ไปจนถึงการลบและทำความสะอาดอย่างปลอดภัย

---

## 1. คำสั่งสร้าง Worktree ใหม่ (`git worktree add`)

### 1.1 สร้าง Worktree พร้อมแตกกิ่งใหม่ทันที (ท่ามาตรฐานที่นิยมที่สุด)
```bash
# รูปแบบ: git worktree add <path> -b <new-branch>
git worktree add ../my-project-auth -b feature/auth-system
```
- Git จะสร้างโฟลเดอร์ใหม่ชื่อ `my-project-auth` อยู่นอกโฟลเดอร์ปัจจุบัน
- สร้าง Branch ใหม่ชื่อ `feature/auth-system`
- Checkout โค้ดของกิ่งใหม่ลงในโฟลเดอร์นั้นทันที พร้อมให้เปิด IDE ทำงานได้คู่ขนาน

### 1.2 สร้าง Worktree สำหรับกิ่งที่มีอยู่แล้ว
```bash
git worktree add ../my-project-hotfix hotfix/critical-bug
```

---

## 2. การตรวจสอบและสำรวจ Worktree (`git worktree list`)

```bash
git worktree list
```
**ตัวอย่างผลลัพธ์:**
```text
/Users/dev/my-project          8f2a1b0 [main]
/Users/dev/my-project-auth     e1c4d9a [feature/auth-system]
/Users/dev/my-project-hotfix   9a2b3c4 [hotfix/critical-bug]
```
จะแสดงพาธบนระบบไฟล์, Commit Hash ปัจจุบัน และชื่อ Branch ที่ผูกอยู่กับแต่ละ Worktree อย่างชัดเจน

---

## 3. การลบและทำความสะอาด Worktree (`remove` & `prune`)

### 3.1 การลบ Worktree อย่างถูกต้อง
เมื่อพัฒนางานเสร็จสิ้นและ Merge เข้าสู่กิ่งหลักเรียบร้อยแล้ว:
```bash
# ลบโฟลเดอร์ Worktree และถอนทะเบียนออกจาก Git
git worktree remove ../my-project-auth
```
> [!note] การลบ Worktree ไม่ได้ลบ Branch
> การลบโฟลเดอร์ Worktree ทิ้งไป จะไม่ทำให้ Branch ถูกลบตามไปด้วย หากต้องการลบ Branch ให้ใช้ `git branch -d feature/auth-system` ตามปกติ

### 3.2 การกวาดล้างข้อมูลตกค้าง (`prune`)
หากคุณเผลอไปกดลบโฟลเดอร์ Worktree ทิ้งจาก Finder หรือสั่ง `rm -rf` ด้วยมือ ทำให้ Git ยังมีข้อมูล Metadata ค้างอยู่ใน `.git/worktrees/`:
```bash
# สั่งให้ Git ตรวจสอบและตัดรายชื่อ Worktree ที่โฟลเดอร์หายไปแล้วออกจากระบบ
git worktree prune
```

---

## 4. ปัญหาที่พบบ่อย (Troubleshooting)

### อาการ: สั่ง `git worktree add` แล้วฟ้อง `fatal: 'main' is already checked out at ...`
- **Cause:** พยายามจะเปิด Worktree ไปยัง Branch ที่มี Worktree อื่น (เช่น Main Working Tree) เปิดใช้งานอยู่แล้ว
- **Solution:** ให้สร้าง Branch ใหม่แทน เช่น `git worktree add ../my-task -b feature/task` หรือสลับ Worktree แรกไปที่กิ่งอื่นก่อน

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Worktree-Concept]] — สถาปัตยกรรมภายในของ Worktree
- [[Worktree-vs-Clone]] — เปรียบเทียบ Worktree กับ Clone
- [[Worktree-with-AI-Agents]] — การประยุกต์ใช้งานร่วมกับ AI Agents\n