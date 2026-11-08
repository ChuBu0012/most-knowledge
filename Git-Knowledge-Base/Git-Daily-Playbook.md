---
title: Git Daily Playbook
tags:
  - git
  - daily-use
  - workflow
  - playbook
type: guide
status: published
---

# Git Daily Playbook

คู่มือสำหรับเปิดใช้ระหว่างทำงานจริง แบ่งตามช่วงเวลาและสถานการณ์  
ถ้าต้องการคำอธิบายกลไก ให้ตามลิงก์ไปยังบทเรียนเชิงลึก

กลับไปยังแผนที่รวม: [[START-HERE]]

## 0. ก่อนเริ่มงาน

```bash
git status
git switch main
git pull --ff-only origin main
git switch -c feature/<short-name>
```

ถ้า `git pull --ff-only` ไม่ผ่าน อย่าใช้ `reset` แก้ทันที ให้เปิด [[Troubleshooting-Scenarios]]

## 1. ระหว่างทำงาน

ทำงานเป็นรอบเล็ก ๆ:

```bash
git status
git diff
git add <files-you-reviewed>
git diff --staged
git commit -m "feat: describe the change"
```

> [!warning] ระวัง `git add .`
> ใช้ได้เมื่อรู้แน่ชัดว่าไฟล์ทั้งหมดในโฟลเดอร์ปลอดภัยแล้วเท่านั้น ตรวจ `git status` และ `git diff --staged` ก่อน Commit เสมอ

## 2. ก่อนส่งงาน

```bash
git status
git log --oneline --decorate -5
git push -u origin feature/<short-name>
```

จากนั้นเปิด Pull Request ตาม [[Pull-Request-Workflow]]

## 3. ต้องสลับไปทำงานด่วน

ถ้างานปัจจุบันยังไม่พร้อม Commit:

```bash
git stash push -u -m "wip: <short-name>"
git switch <target-branch>
```

กลับมาทำงานเดิม:

```bash
git switch feature/<short-name>
git stash pop
```

## 4. เจอ Conflict

1. อ่านสถานะด้วย `git status`
2. เปิดไฟล์และตัดสินใจเนื้อหาที่ถูกต้อง
3. ลบ Conflict Markers ให้หมด
4. รัน Test หรือ Build
5. สั่ง `git add <resolved-files>`
6. ทำต่อด้วย `git merge --continue` หรือ `git rebase --continue` ตามที่ `git status` ระบุ

รายละเอียดอยู่ที่ [[Conflict-Resolution-Workflow]]

## 5. ทำพลาด ให้เลือกตามสถานการณ์

| สถานการณ์ | คำสั่ง/หน้าอ้างอิง |
|---|---|
| แก้ไฟล์แต่ยังไม่ Commit และอยากทิ้ง | `git restore <file>` |
| Add แล้ว แต่อยากเอาออกจาก Staging | `git restore --staged <file>` |
| Commit ล่าสุดผิด แต่ยังไม่ Push | `git commit --amend` |
| Commit ผิดและต้องเก็บงานไว้แก้ต่อ | `git reset --soft HEAD~1` |
| งานบน Remote ถูกเขียนทับหรือหาไม่เจอ | [[Git-Reflog]] |
| Secret หลุดเข้า Commit | [[Troubleshooting-Scenarios]] และ Rotate Secret ทันที |

> [!danger] อย่าใช้ `git reset --hard` หรือ `git push --force` หากยังไม่เข้าใจผลกระทบ

## ไปต่อ

- [[Git-Simple-Guide]] — เวอร์ชันอธิบายแนวคิดสำหรับผู้เริ่มต้น
- [[Git-Command-Cheatsheet]] — ค้นคำสั่ง
- [[Git-Learning-Roadmap]] — เรียนเป็นลำดับ
- [[Git-Architecture]] — เข้าใจ Working Tree, Index และ Object Store
