---
title: "Shell 4 แบบ: Login / Non-login × Interactive / Non-interactive"
aliases:
  - login shell
  - non-login shell
  - interactive shell
  - non-interactive shell
  - shell แบบไหน
tags: [linux, concept, shell]
type: concept
status: published
---

# Shell 4 แบบ

Shell ถูกเปิดได้หลายแบบ และ **แต่ละแบบโหลดไฟล์ตั้งค่าไม่เหมือนกัน** — นี่คือต้นเหตุของ "ใน Terminal ได้ แต่ใน script / ssh / cron ไม่ได้"

แยกด้วย 2 คำถาม:

1. **Interactive?** — มีคนพิมพ์คำสั่งโต้ตอบอยู่ไหม (มี prompt)
2. **Login?** — เป็น shell แรกหลังยืนยันตัวตน (login) หรือเปล่า

| | Interactive (มีคนพิมพ์) | Non-interactive (รัน script/คำสั่งเดียว) |
|---|---|---|
| **Login** | `ssh user@host` · Console login · macOS Terminal.app / iTerm เปิดแท็บใหม่ · `bash -l` · `su - user` | `ssh host 'cmd'` บางกรณี · `bash -l script.sh` |
| **Non-login** | เปิด Terminal บน Linux Desktop · พิมพ์ `bash` ซ้อน · `su user` (ไม่มี `-`) | `bash script.sh` · `./script.sh` · cron · systemd · `ssh host 'cmd'` · Makefile, CI |

## ไฟล์ที่ bash โหลด (สรุป)

| แบบ | โหลด |
|---|---|
| Login (interactive หรือไม่ก็ตาม) | `/etc/profile` → ไฟล์**แรกที่เจอ**ใน `~/.bash_profile`, `~/.bash_login`, `~/.profile` |
| Interactive non-login | `/etc/bash.bashrc` (Debian/Ubuntu) → `~/.bashrc` |
| Non-interactive | **ไม่โหลดอะไรเลย** (ยกเว้นไฟล์ที่ชี้ด้วยตัวแปร `$BASH_ENV`) |

รายละเอียดแต่ละไฟล์และของ zsh → [[Shell-Startup-Files]]

## ผลในชีวิตจริง

| อาการ | เพราะ |
|---|---|
| alias ที่ตั้งใน `.bashrc` ใช้ใน script ไม่ได้ | script = non-interactive ไม่อ่าน `.bashrc` และ bash ปิด alias ใน script อยู่แล้ว |
| `ssh host 'node -v'` → `command not found` แต่ ssh เข้าไปพิมพ์ได้ | คำสั่งเดียวผ่าน ssh = non-interactive · `.bashrc` ของ Ubuntu มีบรรทัด `return` ถ้าไม่ interactive · nvm/PATH เลยไม่ถูกโหลด |
| cron รันแล้วหาโปรแกรมไม่เจอ | cron ใช้ `sh` non-interactive กับ PATH แค่ `/usr/bin:/bin` |
| แก้ `.bashrc` แล้วไม่มีผลบน macOS (bash) | Terminal.app เปิด login shell → อ่าน `.bash_profile` ไม่ใช่ `.bashrc` |

วิธีแก้แต่ละอาการ → [[Linux-Fix-Command-Not-Found-in-Script]]

## เช็กว่าตอนนี้เป็น shell แบบไหน

```bash
# bash
shopt -q login_shell && echo login || echo non-login
[[ $- == *i* ]] && echo interactive || echo non-interactive
echo $0          # ขึ้นต้นด้วย "-" เช่น -bash, -zsh = login shell

# zsh
[[ -o login ]] && echo login || echo non-login
[[ -o interactive ]] && echo interactive || echo non-interactive
```

`$-` คือ flag ของ shell ถ้ามีตัว `i` = interactive

## ต่อไป

- [[Shell-Startup-Files]]
- [[Environment-Variables-and-PATH]]
