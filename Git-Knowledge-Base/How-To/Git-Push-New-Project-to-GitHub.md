---
title: "How-To: เอาโปรเจกต์ในเครื่องขึ้น GitHub ครั้งแรก"
aliases:
  - git init
  - push project ขึ้น github
  - สร้าง repo ใหม่
  - remote add origin
tags: [git, how-to, github]
type: how-to
status: published
---

# เอาโปรเจกต์ในเครื่องขึ้น GitHub ครั้งแรก

## ทางเร็ว (มี `gh` CLI)

```bash
cd my-project
git init
git add .
git commit -m "initial commit"
gh repo create my-project --private --source=. --push
```

## ทางปกติ

1. สร้าง Repo เปล่าบน GitHub (ไม่ต้องติ๊ก README / .gitignore)
2. ในเครื่อง:
   ```bash
   cd my-project
   git init
   git add .
   git commit -m "initial commit"
   git branch -M main
   git remote add origin git@github.com:<user>/my-project.git
   git push -u origin main
   ```

> ก่อน `git add .` สร้าง `.gitignore` ก่อน (อย่างน้อย `.env`, `node_modules/`, `.DS_Store`)

`Permission denied (publickey)` → [[SSH-Use-Key-with-GitHub]]

## ลึกกว่านี้

[[Remote-Repository]] · [[Repository-and-Working-Tree]]
