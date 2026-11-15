---
title: "How-To: แก้ REMOTE HOST IDENTIFICATION HAS CHANGED"
aliases:
  - host key changed
  - known_hosts
  - remote host identification has changed
  - ssh-keygen -R
tags:
  - ssh
  - how-to
  - troubleshooting
type: how-to
status: published
---

# แก้ `REMOTE HOST IDENTIFICATION HAS CHANGED!`

> **ใช้เมื่อ:** Server เพิ่งลง OS ใหม่ / สร้าง VM ใหม่ที่ได้ IP เดิม แล้ว ssh ไม่ยอมต่อ

## 1. ถามตัวเองก่อน: เราเพิ่ง Reinstall / เปลี่ยนเครื่องจริงไหม

- **ใช่** → ทำต่อข้อ 2
- **ไม่ใช่ / ไม่แน่ใจ** → อย่าเพิ่งลบ อาจมีคนดักกลางทาง (MITM) ให้ตรวจ Fingerprint ที่ Server ผ่าน Console ก่อน:
  ```bash
  # บน Server (ทาง Console)
  ssh-keygen -lf /etc/ssh/ssh_host_ed25519_key.pub
  ```
  แล้วเทียบกับ Fingerprint ที่ข้อความ Warning แสดง

## 2. ลบ Host Key เก่า

💻 **เครื่องเรา**

```bash
ssh-keygen -R 192.168.64.8
# ถ้าเคยต่อด้วยชื่อหรือ port อื่น ลบด้วย
ssh-keygen -R lab
ssh-keygen -R "[192.168.64.8]:2222"
```

## 3. ต่อใหม่แล้วยอมรับ Key ใหม่

```bash
ssh chubu@192.168.64.8
# Are you sure you want to continue connecting (yes/no)? → yes
```

> Server ใหม่ = `authorized_keys` ก็หายด้วย อาจต้องทำ [[SSH-Add-Public-Key-to-Server]] อีกรอบ

## ลึกกว่านี้

- [[SSH-Handshake-and-Authentication-Anatomy]] — Host Auth (`known_hosts`) ต่างจาก User Auth (`authorized_keys`) อย่างไร
