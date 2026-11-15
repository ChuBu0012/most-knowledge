---
title: "How-To: ปิด Login ด้วย Password (ให้เข้าได้แค่ Key)"
aliases:
  - ปิด password ssh
  - disable password authentication
  - sshd_config
  - harden ssh server
  - PasswordAuthentication no
tags:
  - ssh
  - how-to
  - security
  - sshd
type: how-to
status: published
---

# ปิด Login ด้วย Password

> **ใช้เมื่อ:** Login ด้วย Key ได้แล้ว และอยากกัน Brute-force รหัสผ่าน
> **ต้องมี:** `sudo` บน Server

> [!danger] กฎข้อเดียว: อย่าปิด Terminal ที่ Login อยู่ จนกว่าจะทดสอบผ่าน
> ถ้าตั้งผิดแล้วปิด Session ไป = ล็อกตัวเองออกจาก Server

## 1. ยืนยันก่อนว่า Key ใช้ได้

💻 **เครื่องเรา** (Terminal ใหม่)

```bash
ssh -o PasswordAuthentication=no chubu@192.168.64.8 'echo KEY OK'
```

ไม่ได้ `KEY OK` → หยุด กลับไปทำ [[SSH-Add-Public-Key-to-Server]] ก่อน

## 2. แก้ Config ของ SSH Server

🖥️ **บน Server**

ระบบใหม่ (Ubuntu 22.04+) รองรับไฟล์แยกใน `sshd_config.d` ซึ่งชนะค่าในไฟล์หลัก ปลอดภัยกว่าแก้ไฟล์หลักตรงๆ:

```bash
sudo nano /etc/ssh/sshd_config.d/99-key-only.conf
```

ใส่:

```sshconfig
PasswordAuthentication no
KbdInteractiveAuthentication no
PubkeyAuthentication yes
PermitRootLogin prohibit-password
```

บันทึก `Ctrl+O` → `Enter` → `Ctrl+X`

> [!note] ระบบเก่าที่ไม่มีโฟลเดอร์ `sshd_config.d`
> แก้ใน `/etc/ssh/sshd_config` แทน: หาบรรทัดเดิมด้วย `Ctrl+W` แล้วเปลี่ยนค่า (ลบ `#` หน้าบรรทัดด้วย)

## 3. ตรวจ Syntax แล้ว Reload

```bash
sudo sshd -t && echo CONFIG OK          # ต้องไม่มี error
sudo systemctl reload ssh 2>/dev/null || sudo systemctl reload sshd
```

`reload` ไม่ตัด Session ที่ต่ออยู่

## 4. ทดสอบจาก Terminal ใหม่

💻 **เครื่องเรา**

```bash
# ต้องเข้าได้
ssh chubu@192.168.64.8 'echo KEY OK'

# ต้องถูกปฏิเสธ = ปิด password สำเร็จ
ssh -o PubkeyAuthentication=no -o PreferredAuthentications=password chubu@192.168.64.8
# ผลที่ถูก: Permission denied (publickey)
```

🖥️ ตรวจค่าจริงที่ Server ใช้:

```bash
sudo sshd -T | grep -Ei "passwordauthentication|kbdinteractive|permitrootlogin"
```

## ถ้าล็อกตัวเองออกไปแล้ว

เข้าทาง Console ของ VM / Cloud (เช่น UTM, Proxmox, AWS EC2 Serial Console) แล้วลบไฟล์ที่สร้าง:

```bash
sudo rm /etc/ssh/sshd_config.d/99-key-only.conf
sudo systemctl reload ssh
```

## ลึกกว่านี้

- [[SSH-Install-and-Enable-Server]] — ติดตั้งและเปิด SSH Server
- [[SSH-Knowledge-Gaps-and-Future-Labs]] — Hardening ขั้นต่อไป
