---
title: "How-To: เปลี่ยนชื่อเครื่อง (hostname)"
aliases:
  - เปลี่ยน hostname
  - set hostname
  - hostnamectl set-hostname
  - unable to resolve host
tags: [linux, how-to, system]
type: how-to
status: published
---

# เปลี่ยนชื่อเครื่อง

## Linux (Ubuntu / Debian / Fedora)

```bash
sudo hostnamectl set-hostname lab-ubuntu
```

แล้วแก้ `/etc/hosts` ให้ตรง (ไม่แก้ = `sudo` ขึ้น `unable to resolve host`):

```bash
sudo nano /etc/hosts
```

```text
127.0.0.1   localhost
127.0.1.1   lab-ubuntu        ← เปลี่ยนชื่อเก่าเป็นชื่อใหม่
```

บันทึก `Ctrl+O` → `Enter` → `Ctrl+X`

## macOS

```bash
sudo scutil --set ComputerName  "most-mac"    # ชื่อที่โชว์ใน Finder / AirDrop
sudo scutil --set LocalHostName "most-mac"    # ชื่อ most-mac.local ใน network
sudo scutil --set HostName      "most-mac"    # ชื่อที่ terminal เห็น
```

## ตรวจ

```bash
hostname
hostnamectl          # Linux
```

Prompt ใน terminal จะเปลี่ยนเมื่อเปิดหน้าต่างใหม่ หรือ `exec $SHELL`

> ชื่อใหม่ไม่กระทบ SSH ที่ต่อด้วย IP แต่ถ้าเคยต่อด้วยชื่อเก่า ต้องเปลี่ยนใน `~/.ssh/config` ด้วย ([[SSH-Setup-Config-Alias]])

## ลึกกว่านี้

[[System-Identity-hostname-uname]]
