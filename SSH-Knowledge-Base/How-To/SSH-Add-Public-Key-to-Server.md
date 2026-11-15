---
title: "How-To: เพิ่ม Public Key ให้ Server (Login ไม่ต้องใช้รหัสผ่าน)"
aliases:
  - เพิ่ม public key
  - ใส่ public key ใน server
  - set public key ssh server
  - authorized_keys
  - ssh-copy-id
  - login ssh ไม่ใช้ password
tags: [ssh, how-to, authorized-keys]
type: how-to
status: published
---

# เพิ่ม Public Key ให้ Server

ตัวอย่าง: User `chubu` · Server `192.168.64.8` · Key `~/.ssh/id_ed25519` — แทนด้วยของตัวเอง
ยังไม่มี Key (`ls ~/.ssh/*.pub` ไม่เจอ) → [[SSH-Create-Key]]

## วิธีที่ 1: คำสั่งเดียว (macOS / Linux)

💻 เครื่องเรา

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub chubu@192.168.64.8
```

ใส่ Password ของ Server ครั้งสุดท้าย แล้วข้ามไป [ตรวจ](#ตรวจ)

## วิธีที่ 2: ทำมือด้วย `nano` (ไม่มี ssh-copy-id / เข้าทาง Console)

**1) Copy Public Key** — 💻 เครื่องเรา

```bash
pbcopy < ~/.ssh/id_ed25519.pub     # macOS (copy ลง clipboard)
cat ~/.ssh/id_ed25519.pub          # อื่นๆ (ลากคลุมแล้ว copy)
```

ต้องได้ **บรรทัดเดียว** ขึ้นต้นด้วย `ssh-ed25519 AAAA...`
⚠️ ใช้ไฟล์ `.pub` เท่านั้น — ถ้าเห็น `BEGIN OPENSSH PRIVATE KEY` คือเปิดผิดไฟล์ ห้ามส่ง

**2) วางลง Server** — 🖥️ Login เป็น User ที่จะใช้ Key นี้

```bash
mkdir -p ~/.ssh && chmod 700 ~/.ssh
nano ~/.ssh/authorized_keys
```

- วาง Key ต่อท้ายเป็น **บรรทัดใหม่** (ห้ามขาดกลางบรรทัด)
- บันทึก `Ctrl+O` → `Enter` · ออก `Ctrl+X`

```bash
chmod 600 ~/.ssh/authorized_keys
```

**ถ้า Login เป็น root แต่จะใส่ให้ User อื่น** — ทำแบบเดียวกันที่ `/home/chubu/.ssh/` แล้วปิดท้ายด้วย
`chown -R chubu:chubu /home/chubu/.ssh` (ลืม = Permission denied)

## ตรวจ

💻 เครื่องเรา (Terminal ใหม่)

```bash
ssh -o PasswordAuthentication=no chubu@192.168.64.8 'echo KEY OK'
```

- ได้ `KEY OK` → ✅ เสร็จ
- `Permission denied (publickey)` → [[SSH-Fix-Permission-Denied-Publickey]]
- ถาม Passphrase → ปกติ (เป็นรหัสของ Key เอง ไม่ใช่ Password Server)

## ต่อไป

[[SSH-Setup-Config-Alias]] (พิมพ์แค่ `ssh lab`) · [[SSH-Disable-Password-Login]] (ปิด Password)

## ลึกกว่านี้ (ทำงานยังไง)

[[SSH-Handshake-and-Authentication-Anatomy]] · [[Asymmetric-Cryptography-and-Key-Generation]]
