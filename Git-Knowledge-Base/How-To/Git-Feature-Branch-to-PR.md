---
title: "How-To: เริ่มงานใหม่จนเปิด Pull Request"
aliases:
  - เปิด PR
  - pull request
  - feature branch
  - workflow ประจำวัน
  - git daily
tags: [git, how-to, workflow, pull-request]
type: how-to
status: published
---

# เริ่มงานใหม่จนเปิด Pull Request

## 1. เริ่มจาก main ล่าสุด

```bash
git switch main
git pull --ff-only
git switch -c feature/login-page
```

## 2. ทำงาน แล้ว Commit เป็นรอบเล็กๆ

```bash
git status
git add <file>          # เลือกไฟล์ที่ตรวจแล้ว
git diff --staged       # ดูสิ่งที่จะ commit
git commit -m "feat: add login page"
```

## 3. Push แล้วเปิด PR

```bash
git push -u origin feature/login-page
gh pr create --fill          # หรือกดปุ่ม "Compare & pull request" บน GitHub
```

## 4. ระหว่างรอ Review ถ้า main ขยับ

```bash
git fetch
git rebase origin/main
git push --force-with-lease
```

## 5. หลัง Merge แล้ว เก็บกวาด

```bash
git switch main
git pull --ff-only
git branch -d feature/login-page
```

## ลึกกว่านี้

[[Pull-Request-Workflow]] · [[Branch-Concept]] · [[Upstream-and-Tracking-Branch]]
