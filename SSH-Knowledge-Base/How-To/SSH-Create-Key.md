---
title: "How-To: สร้าง SSH Key ใหม่"
aliases:
  - สร้าง ssh key
  - ssh-keygen
  - generate ssh key
  - gen key
tags:
  - ssh
  - how-to
  - keys
type: how-to
status: published
---

# สร้าง SSH Key ใหม่

> **ใช้เมื่อ:** เครื่องใหม่ / ยังไม่มี Key / อยากแยก Key สำหรับงานใดงานหนึ่ง
> **ใช้เวลา:** 1 นาที

## 1. เช็กก่อนว่ามี Key อยู่แล้วไหม

💻 **เครื่องเรา**

```bash
ls -la ~/.ssh/*.pub
```

- เจอ `id_ed25519.pub` อยู่แล้ว → ใช้ได้เลย ไม่ต้องสร้างใหม่ ข้ามไป [[SSH-Add-Public-Key-to-Server]]
- `No such file` → สร้างตามขั้นที่ 2

## 2. สร้าง Key

```bash
ssh-keygen -t ed25519 -C "most-too@macbook"
```

ระบบจะถาม 3 คำถาม:

| คำถาม | ตอบ |
|---|---|
| `Enter file in which to save the key` | กด `Enter` (ใช้ `~/.ssh/id_ed25519`) หรือพิมพ์ชื่อแยก เช่น `~/.ssh/id_ed25519_lab` |
| `Enter passphrase` | ตั้งรหัสปกป้อง Key (แนะนำ) หรือกด `Enter` ถ้าไม่ต้องการ |
| `Enter same passphrase again` | พิมพ์ซ้ำ |

> [!warning] ถ้าระบบถาม `Overwrite (y/n)?` ให้ตอบ `n`
> แปลว่ามี Key ชื่อนี้อยู่แล้ว ถ้าทับ Server ทุกเครื่องที่ใช้ Key เก่าจะเข้าไม่ได้ทันที

## 3. ตั้ง Permission และโหลดเข้า Agent

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519

# macOS: เก็บ passphrase ใน Keychain จะได้ไม่ต้องพิมพ์ทุกครั้ง
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
# Linux:
# eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519
```

## ตรวจว่าสำเร็จ

```bash
ls -la ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.pub   # ต้องมี 2 ไฟล์
ssh-keygen -lf ~/.ssh/id_ed25519.pub             # แสดง fingerprint = key ใช้ได้
ssh-add -l                                       # key อยู่ใน agent
```

## ขั้นต่อไป

- เอา Key ไปใส่ Server → [[SSH-Add-Public-Key-to-Server]]
- เอา Key ไปใส่ GitHub → [[SSH-Use-Key-with-GitHub]]

## ลึกกว่านี้

- [[SSH-Key-Types-and-Algorithms]] — ทำไมเลือก `ed25519` แทน `rsa`
- [[SSH-Passphrase-and-Key-Protection]] — ควรตั้ง Passphrase ไหม
