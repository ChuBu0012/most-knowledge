---
title: "How-To: ใน Terminal ได้ แต่ใน script / ssh / cron บอก command not found"
aliases:
  - command not found ใน cron
  - command not found ssh
  - ssh host command not found
  - cron ไม่ทำงาน
  - non-interactive shell
  - nvm ใน script
tags: [linux, how-to, shell, troubleshooting]
type: how-to
status: published
---

# ใน Terminal ได้ แต่ใน script / ssh / cron ไม่ได้

**สาเหตุเดียว:** ที่เหล่านี้เป็น *non-interactive shell* → ไม่โหลด `.bashrc` → PATH / alias / nvm ที่ตั้งไว้ไม่มา

## หา path เต็มของโปรแกรมก่อน (ใช้กับทุกกรณี)

💻 ในหน้าต่างที่ใช้งานได้:

```bash
command -v node        # เช่น /home/chubu/.nvm/versions/node/v22.11.0/bin/node
```

## กรณี `ssh host 'cmd'`

```bash
# แก้เร็ว: ใช้ path เต็ม
ssh lab '/home/chubu/.nvm/versions/node/v22.11.0/bin/node -v'

# หรือบังคับเป็น login shell (โหลด ~/.profile)
ssh lab 'bash -lc "node -v"'
```

แก้ถาวร: บน Server ย้ายบรรทัด `export PATH=...` / nvm ไปไว้ **บนสุด** ของ `~/.bashrc` (ก่อนบรรทัด `case $- in *i*) ... return`)

## กรณี script (`./deploy.sh`)

```bash
#!/usr/bin/env bash
export PATH="$HOME/.local/bin:$PATH"     # ตั้ง PATH เองในต้น script
set -euo pipefail                         # ให้ script หยุดทันทีเมื่อ error (แนะนำ)
```

- alias ใช้ใน script ไม่ได้ → เขียนคำสั่งเต็ม
- อย่าพึ่งพา `.bashrc` ใน script — script ที่ดีควรรันได้แม้ไม่มี rc file

## กรณี cron

```bash
crontab -e
```

```cron
PATH=/home/chubu/.local/bin:/usr/local/bin:/usr/bin:/bin
SHELL=/bin/bash

# ทุกวัน 02:00 — ใช้ path เต็ม + เก็บ log เสมอ
0 2 * * * /home/chubu/scripts/backup.sh >> /home/chubu/backup.log 2>&1
```

ดูว่า cron เห็น environment แบบไหน: ใส่ `* * * * * env > /tmp/cron-env.txt` รอ 1 นาที แล้ว `cat /tmp/cron-env.txt` (ลบบรรทัดนี้ทิ้งหลังดู)

## กรณี systemd service

ใส่ใน unit file:

```ini
[Service]
Environment=PATH=/home/chubu/.local/bin:/usr/bin:/bin
ExecStart=/home/chubu/.local/bin/myapp
```

## ลึกกว่านี้

[[Shell-Types-Login-Interactive]] — ทำไมแต่ละที่โหลดไฟล์ต่างกัน · [[Shell-Startup-Files]]
