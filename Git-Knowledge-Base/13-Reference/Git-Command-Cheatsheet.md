---
title: Git Command Cheatsheet
tags:
  - git
  - cheatsheet
  - reference
  - commands
type: reference
status: published
---

# Git Command Cheatsheet: รวมคำสั่งลัดพร้อมหมวดหมู่

รวบรวมคำสั่ง Git ที่สำคัญและใช้บ่อยที่สุด จัดหมวดหมู่ตามการใช้งานจริง พร้อมลิงก์ไปยังเอกสารอธิบายเชิงลึก

---

## 1. การตั้งค่าและเริ่มต้นระบบ (Setup & Init)
- `git init` — เริ่มต้นสร้าง Repository ในโฟลเดอร์ปัจจุบัน ([[Repository-and-Working-Tree]])
- `git clone <url>` — โคลนโปรเจกต์จาก Remote ลงมาในเครื่อง ([[Repository-and-Working-Tree]])
- `git config --global user.name "Your Name"` — ตั้งชื่อผู้เขียน Commit ([[Git-Configuration]])
- `git config --global user.email "you@example.com"` — ตั้งอีเมลของผู้เขียน Commit ([[Git-Configuration]])
- `git config --list --show-origin` — ตรวจสอบค่าคอนฟิกทั้งหมด ([[Git-Configuration]])

---

## 2. การทำงานประจำวัน (Daily Workflow)
- `git status` — ตรวจสอบสถานะของ Working Tree และ Staging Area ([[Daily-Git-Commands]])
- `git add <file>` — นำไฟล์เข้า Staging Area เพื่อบันทึก Snapshot ([[Git-Add-and-Staging]])
- `git add .` — นำทุกไฟล์ที่มีการเปลี่ยนแปลงเข้า Staging Area ([[Git-Add-and-Staging]])
- `git add -p` — เลือก Stage เฉพาะบางท่อนของโค้ดแบบ Interactive ([[Git-Add-and-Staging]])
- `git commit -m "message"` — บันทึก Snapshot ถาวรลงประวัติศาสตร์ ([[Git-Commit]])
- `git commit --amend --no-edit` — ผนวกการเปลี่ยนแปลงเข้า Commit ล่าสุด ([[Git-Commit]])
- `git diff` — เปรียบเทียบความต่าง Working Tree vs Staging Area ([[Git-Diff]])
- `git diff --staged` — เปรียบเทียบ Staging Area vs HEAD ([[Git-Diff]])

---

## 3. การจัดการ Branch (Branching & Switching)
- `git branch` — แสดงรายชื่อ Local Branches ทั้งหมด ([[Branch-Commands]])
- `git branch -a -v` — แสดงทุก Branch รวมถึง Remote พร้อม Commit ล่าสุด ([[Branch-Commands]])
- `git switch <branch>` — สลับไปยัง Branch ที่มีอยู่ ([[Branch-Commands]])
- `git switch -c <new-branch>` — สร้างและสลับไปยัง Branch ใหม่ทันที ([[Branch-Commands]])
- `git branch -d <branch>` — ลบ Branch ที่ผสานงานแล้วอย่างปลอดภัย ([[Branch-Commands]])
- `git branch -D <branch>` — บังคับลบ Branch ทิ้งทันที ([[Branch-Commands]])

---

## 4. การเชื่อมต่อ Remote (Remote Operations)
- `git remote -v` — แสดงรายชื่อ URL ของ Remote Repository ([[Remote-Repository]])
- `git remote add origin <url>` — ผูก Remote ใหม่ในชื่อ `origin` ([[Remote-Repository]])
- `git fetch origin` — ดาวน์โหลดออบเจกต์และอัปเดต Remote-tracking branches ([[Fetch-Pull-Push]])
- `git pull origin <branch>` — ดาวน์โหลดและรวมโค้ดเข้า Working Tree ทันที ([[Fetch-Pull-Push]])
- `git pull --rebase origin <branch>` — ดึงโค้ดและ Replay งานของเราบนฐานใหม่ ([[Fetch-Pull-Push]])
- `git push -u origin <branch>` — Push งานพร้อมผูก Tracking ความสัมพันธ์ Upstream ([[Upstream-and-Tracking-Branch]])

---

## 5. การรวมโค้ด (Integration)
- `git merge <branch>` — ผสานกิ่งเข้ามายังกิ่งปัจจุบัน ([[Git-Merge]])
- `git merge --no-ff <branch>` — บังคับสร้าง Merge Commit เสมอ ([[Git-Merge]])
- `git merge --abort` — ยกเลิกการ Merge ที่ติด Conflict กลับคืนสู่สภาพเดิม ([[Git-Merge]])
- `git rebase <base-branch>` — นำ Commit ปัจจุบันไปเรียงใหม่บน Base ล่าสุด ([[Git-Rebase]])
- `git rebase -i HEAD~n` — Interactive Rebase เพื่อจัดแต่ง ยุบ หรือแก้ข้อความ Commit ([[Git-Rebase]])
- `git rebase --continue` — เดินหน้า Rebase ต่อหลังแก้ Conflict แล้ว ([[Git-Rebase]])
- `git rebase --abort` — ยกเลิกการ Rebase ทั้งหมด ([[Git-Rebase]])
- `git cherry-pick <commit-hash>` — หยิบเฉพาะ Commit เจาะจงมาใส่กิ่งปัจจุบัน ([[Git-Cherry-Pick]])

---

## 6. การยกเลิกและกู้คืน (Undo & Recovery)
- `git restore <file>` — ยกเลิกการแก้ไขไฟล์ใน Working Tree ทิ้ง ([[Git-Restore]])
- `git restore --staged <file>` — เอาไฟล์ออกจาก Staging Area (Unstaging) ([[Git-Restore]])
- `git reset --soft HEAD~1` — ถอย 1 Commit โดยคงของไว้ใน Staging Area ([[Git-Reset]])
- `git reset --mixed HEAD~1` — ถอย 1 Commit โดยของกลับมาเป็น Unstaged ใน Working Tree ([[Git-Reset]])
- `git reset --hard HEAD~1` — ถอย 1 Commit และกวาดทิ้งการแก้ไขใน Working Tree ทั้งหมด! ([[Git-Reset]])
- `git revert <commit-hash>` — สร้าง Commit ใหม่ที่หักล้างการเปลี่ยนแปลงเดิมอย่างปลอดภัย ([[Git-Revert]])
- `git reflog` — ส่องกล่องดำบันทึกประวัติการก้าวเดินทั้งหมดของ HEAD ([[Git-Reflog]])

---

## 7. การสืบสวนและค้นหา (Inspection & Debugging)
- `git log --oneline --graph --decorate --all` — กราฟประวัติศาสตร์รวมแบบกระชับ ([[Git-Log]])
- `git show <commit-hash>` — แสดงรายละเอียดและการเปลี่ยนแปลงของ Commit ([[Git-Show-and-Blame]])
- `git blame -L 10,20 <file>` — ตรวจสอบว่าใครเขียนโค้ดแต่ละบรรทัด ([[Git-Show-and-Blame]])
- `git bisect start / bad / good / reset` — ทำ Binary Search ค้นหา Commit บั๊กอัตโนมัติ ([[Git-Bisect]])

---

## 8. Git Worktree (Parallel Development)
- `git worktree add <path> -b <branch>` — สร้างโฟลเดอร์ทำงานคู่ขนานพร้อมกิ่งใหม่ ([[Worktree-Commands]])
- `git worktree list` — แสดงรายชื่อ Worktrees ทั้งหมด ([[Worktree-Commands]])
- `git worktree remove <path>` — ลบโฟลเดอร์ Worktree และถอนทะเบียน ([[Worktree-Commands]])
- `git worktree prune` — กวาดล้าง Worktree ขยะที่โฟลเดอร์หายไปแล้ว ([[Worktree-Commands]])

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-Terminology]] — พจนานุกรมคำศัพท์สำคัญ
- [[Common-Mistakes]] — รวมข้อผิดพลาดที่พบบ่อย\n