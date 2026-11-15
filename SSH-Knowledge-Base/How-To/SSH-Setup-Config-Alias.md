---
title: "How-To: ตั้งชื่อเล่น Server (ssh lab แทน ssh user@ip)"
aliases:
  - ssh config
  - ssh alias
  - ~/.ssh/config
  - ตั้งชื่อ server
tags:
  - ssh
  - how-to
  - config
type: how-to
status: published
---

# ตั้งชื่อเล่น Server ด้วย `~/.ssh/config`

> **ใช้เมื่อ:** ขี้เกียจพิมพ์ `ssh -i ~/.ssh/id_ed25519 -p 22 chubu@192.168.64.8` ทุกครั้ง

## 1. เปิดไฟล์

💻 **เครื่องเรา**

```bash
touch ~/.ssh/config
chmod 600 ~/.ssh/config
nano ~/.ssh/config
```

## 2. เพิ่ม Block นี้ (แก้ค่าให้ตรงของตัวเอง)

```sshconfig
Host lab
    HostName 192.168.64.8
    User chubu
    Port 22
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes

# ค่ากลางสำหรับทุก host (วางไว้ล่างสุดเสมอ)
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
    AddKeysToAgent yes
    UseKeychain yes
```

> `UseKeychain` ใช้ได้เฉพาะ macOS ถ้าเป็น Linux ให้ลบบรรทัดนั้น

บันทึก `Ctrl+O` → `Enter` → `Ctrl+X`

## 3. ใช้งาน

```bash
ssh lab
scp ./file.txt lab:/tmp/
ssh -L 5432:127.0.0.1:5432 lab
```

ชื่อ `lab` ใช้ได้กับทุกคำสั่งตระกูล ssh (`scp`, `sftp`, `rsync`, VS Code Remote-SSH)

## ตรวจว่าสำเร็จ

```bash
ssh -G lab | grep -Ei "^(hostname|user|port|identityfile) "
```

ต้องเห็นค่าที่ตั้งไว้ ถ้าไม่ตรง = มี Block ด้านบนที่ match ก่อน (SSH ใช้ค่าแรกที่เจอ)

## ลึกกว่านี้

- [[SSH-Client-Configuration-and-Aliases]] — ลำดับการ match และ option อื่นๆ (`ProxyJump`)
