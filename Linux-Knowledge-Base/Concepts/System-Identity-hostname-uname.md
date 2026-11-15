---
title: "hostname, uname, os-release: เครื่องนี้คือใคร"
aliases:
  - hostname
  - uname
  - uname -a
  - os-release
  - hostnamectl
  - kernel version
  - architecture
tags: [linux, concept, system]
type: concept
status: published
---

# hostname, uname, os-release

3 คำถาม 3 คำสั่ง:

| อยากรู้ | คำสั่ง | ตอบมาจาก |
|---|---|---|
| เครื่องนี้**ชื่ออะไร** | `hostname` | Kernel (ตั้งค่าถาวรใน `/etc/hostname`) |
| **Kernel / CPU** อะไร | `uname` | Kernel |
| **Distro** อะไร (Ubuntu 24.04?) | `cat /etc/os-release` | ไฟล์ของ Distro (Kernel ไม่รู้ว่าตัวเองอยู่ใน Ubuntu) |

## `hostname`

```bash
hostname          # ชื่อสั้น เช่น lab-ubuntu
hostname -f       # FQDN เช่น lab-ubuntu.local (Linux)
hostname -I       # IP ทุกตัวของเครื่อง (Linux เท่านั้น; macOS ใช้ ipconfig getifaddr en0)
hostnamectl       # ชื่อ + OS + kernel + arch + virtualization (systemd)
```

ชื่อเครื่องเก็บ 2 ที่บน Linux:
- `/etc/hostname` — ชื่อที่ใช้ตอน boot
- `/etc/hosts` — แปลงชื่อเป็น IP ในเครื่อง (Ubuntu มีบรรทัด `127.0.1.1 <ชื่อเครื่อง>`) ถ้าไม่ตรงกัน `sudo` จะช้าและขึ้น `unable to resolve host`

เปลี่ยนชื่อ → [[Linux-Change-Hostname]]

## `uname`

| Option | แสดง | ตัวอย่าง |
|---|---|---|
| `-a` | ทั้งหมด | `Linux lab 6.8.0-45-generic #45-Ubuntu SMP ... aarch64 GNU/Linux` |
| `-s` | ชื่อ kernel | `Linux` / `Darwin` (macOS) |
| `-n` | ชื่อเครื่อง (= hostname) | `lab` |
| `-r` | **เวอร์ชัน kernel** ⭐ | `6.8.0-45-generic` |
| `-v` | build ของ kernel | `#45-Ubuntu SMP PREEMPT_DYNAMIC ...` |
| `-m` | **สถาปัตยกรรม CPU** ⭐ | `x86_64` / `aarch64` (Linux ARM) / `arm64` (Apple Silicon) |
| `-o` | ชื่อระบบ (GNU uname เท่านั้น) | `GNU/Linux` |

`-m` สำคัญตอนดาวน์โหลดโปรแกรม: `x86_64` = amd64 · `aarch64`/`arm64` = ARM
`-r` สำคัญตอนลง driver / ตรวจช่องโหว่ kernel

## `/etc/os-release`

```bash
cat /etc/os-release
. /etc/os-release && echo "$PRETTY_NAME"     # Ubuntu 24.04.1 LTS
lsb_release -a                               # ถ้ามี
sw_vers                                      # macOS
```

ใช้ใน script ได้ เช่น `if [ "$ID" = "ubuntu" ]; then ...`

## ต่อไป

ลงมือ → [[Linux-Check-System-Info]]
