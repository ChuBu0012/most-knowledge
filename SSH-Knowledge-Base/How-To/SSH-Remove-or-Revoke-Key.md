---
title: "How-To: ถอน Key ออกจาก Server (เครื่องหาย / เลิกให้สิทธิ์)"
aliases:
  - ลบ public key
  - revoke ssh key
  - เอา key ออก
  - เครื่องหาย ssh
tags:
  - ssh
  - how-to
  - security
type: how-to
status: published
---

# ถอน Key ออกจาก Server

> **ใช้เมื่อ:** Laptop หาย / คนออกจากทีม / เปลี่ยน Key ใหม่

## 1. ดูว่ามี Key อะไรบ้าง

🖥️ **บน Server**

ดูเลขบรรทัด + ชนิด Key + comment ท้ายบรรทัด (ชื่อเครื่อง):

```bash
awk '{print NR": "$1" ... "$NF}' ~/.ssh/authorized_keys
```

## 2. สำรองแล้วลบบรรทัดที่ไม่ต้องการ

```bash
cp ~/.ssh/authorized_keys ~/.ssh/authorized_keys.bak
nano ~/.ssh/authorized_keys     # ไปบรรทัดนั้น กด Ctrl+K เพื่อตัดทั้งบรรทัด → Ctrl+O → Ctrl+X
```

หรือลบด้วยคำสั่ง ตาม comment (เช่น `old-laptop`):

```bash
grep -v 'old-laptop$' ~/.ssh/authorized_keys.bak > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

> ⚠️ อย่าลบ Key ของเครื่องที่ใช้อยู่ตอนนี้ ทดสอบจาก Terminal ใหม่ก่อนปิด Session

## 3. ตรวจ

💻 จากเครื่องที่ถูกถอน ต้องได้ `Permission denied (publickey)`
💻 จากเครื่องที่ยังใช้ ต้องเข้าได้ตามปกติ

## ลึกกว่านี้

- [[SSH-Knowledge-Gaps-and-Future-Labs]] — SSH Certificate ที่ไม่ต้องไล่ลบทีละ Server
