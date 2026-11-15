---
title: "How-To: ใช้ SSH Key กับ GitHub"
aliases:
  - ssh github
  - github ssh key
  - git push ด้วย ssh
  - git@github.com permission denied
tags:
  - ssh
  - git
  - github
  - how-to
type: how-to
status: published
---

# ใช้ SSH Key กับ GitHub

> **ใช้เมื่อ:** อยาก `git push` / `git clone git@github.com:...` โดยไม่ต้องใส่ Token

## 1. มี Key หรือยัง

```bash
ls ~/.ssh/id_ed25519.pub || ssh-keygen -t ed25519 -C "github"
```

## 2. Copy Public Key

```bash
pbcopy < ~/.ssh/id_ed25519.pub     # macOS
# หรือ: cat ~/.ssh/id_ed25519.pub แล้ว copy เอง
```

## 3. เพิ่มใน GitHub

GitHub → รูปโปรไฟล์ → **Settings** → **SSH and GPG keys** → **New SSH key**
- Title: ชื่อเครื่อง เช่น `macbook`
- Key type: `Authentication Key`
- Key: วางที่ copy ไว้ → **Add SSH key**

หรือใช้ `gh` CLI:

```bash
gh ssh-key add ~/.ssh/id_ed25519.pub --title "macbook"
```

## 4. ทดสอบ

```bash
ssh -T git@github.com
```

ต้องได้: `Hi <username>! You've successfully authenticated...`

## 5. เปลี่ยน Repo เดิมจาก HTTPS เป็น SSH

```bash
git remote -v                                           # ดูว่าตอนนี้เป็น https:// ไหม
git remote set-url origin git@github.com:<user>/<repo>.git
git push
```

## ลึกกว่านี้

- [[Remote-Repository]] — Remote URL แบบต่างๆ
- [[SSH-Fix-Permission-Denied-Publickey]] — ถ้า `ssh -T` ไม่ผ่าน
