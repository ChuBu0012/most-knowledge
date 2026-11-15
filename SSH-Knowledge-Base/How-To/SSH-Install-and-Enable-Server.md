---
title: "How-To: ติดตั้งและเปิด SSH Server"
aliases:
  - ติดตั้ง ssh server
  - เปิด ssh server
  - openssh-server
  - enable sshd
  - macOS remote login
  - connection refused port 22
tags:
  - ssh
  - how-to
  - sshd
type: how-to
status: published
---

# ติดตั้งและเปิด SSH Server

> **ใช้เมื่อ:** เครื่องใหม่ / VM ใหม่ ยัง ssh เข้าไม่ได้ หรือเจอ `Connection refused`

## Ubuntu / Debian

🖥️ **บนเครื่องที่จะเป็น Server**

```bash
sudo apt update
sudo apt install -y openssh-server
sudo systemctl enable --now ssh
```

## Fedora / RHEL / Rocky

```bash
sudo dnf install -y openssh-server
sudo systemctl enable --now sshd
```

## macOS (ให้ Mac รับ ssh เข้ามา)

```bash
sudo systemsetup -setremotelogin on
```

หรือ System Settings → General → Sharing → เปิด **Remote Login**

## เปิด Firewall (ถ้ามี)

```bash
# Ubuntu (ufw)
sudo ufw allow OpenSSH
# Fedora/RHEL (firewalld)
sudo firewall-cmd --permanent --add-service=ssh && sudo firewall-cmd --reload
```

## หา IP ของ Server

```bash
hostname -I        # Linux
ipconfig getifaddr en0   # macOS
```

## ตรวจว่าสำเร็จ

🖥️ บน Server:

```bash
systemctl status ssh --no-pager      # (หรือ sshd) ต้องเป็น active (running)
sudo ss -tlnp | grep ':22'           # ต้องเห็น LISTEN 0.0.0.0:22
```

💻 จากเครื่องเรา:

```bash
nc -vz 192.168.64.8 22     # succeeded = เข้าถึงพอร์ตได้
ssh chubu@192.168.64.8
```

| อาการ | สาเหตุ |
|---|---|
| `Connection refused` | Service ไม่รัน หรือฟังคนละ Port |
| `Connection timed out` | Firewall / IP ผิด / คนละ Network |

## ขั้นต่อไป

1. [[SSH-Add-Public-Key-to-Server]]
2. [[SSH-Disable-Password-Login]]

## ลึกกว่านี้

- [[SSH-Architecture-and-Fundamentals]]
- [[Foundational-Networking-and-Sockets]]
