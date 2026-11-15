---
title: "How-To: เพิ่มโฟลเดอร์เข้า PATH (ติดตั้งแล้วแต่ command not found)"
aliases:
  - เพิ่ม path
  - add to path
  - export PATH
  - command not found หลังติดตั้ง
  - ~/.local/bin
tags: [linux, how-to, shell, path]
type: how-to
status: published
---

# เพิ่มโฟลเดอร์เข้า PATH

> **ใช้เมื่อ:** ติดตั้งโปรแกรมแล้ว (เช่น pip, cargo, go, ไฟล์ที่ดาวน์โหลดมา) แต่พิมพ์ชื่อแล้ว `command not found`

## 1. หาว่าโปรแกรมอยู่ไหน

```bash
ls ~/.local/bin ~/bin ~/go/bin ~/.cargo/bin 2>/dev/null
# หรือหาตรงๆ
find ~ -name "<ชื่อโปรแกรม>" -type f 2>/dev/null | head
```

## 2. ลองชั่วคราวก่อน (หายเมื่อปิดหน้าต่าง)

```bash
export PATH="$HOME/.local/bin:$PATH"
<ชื่อโปรแกรม> --version
```

ได้แล้วค่อยทำให้ถาวร

## 3. ทำให้ถาวร

```bash
# bash (Ubuntu)
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.profile

# zsh (macOS)
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zprofile
```

> ⚠️ ใช้ `>>` (ต่อท้าย) ห้าม `>` (เขียนทับไฟล์ทั้งไฟล์)
> ⚠️ ต้องมี `:$PATH` ต่อท้ายเสมอ ไม่งั้น PATH เดิมหาย → `ls` ก็หาไม่เจอ

ใส่ไว้ **หน้า** `$PATH` = ให้ตัวนี้ชนะตัวที่ติดมากับระบบ · ใส่ **หลัง** = ใช้เมื่อหาที่อื่นไม่เจอ

ให้มีผล: `exec $SHELL -l`

## ตรวจ

```bash
echo "$PATH" | tr ':' '\n'    # ต้องเห็นโฟลเดอร์ที่เพิ่ม
command -v <ชื่อโปรแกรม>       # ต้องได้ path
```

## พัง PATH ไปแล้ว (ls ก็หาไม่เจอ)

```bash
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
nano ~/.profile     # แก้บรรทัดที่ผิด
```

## ลึกกว่านี้

[[Environment-Variables-and-PATH]] · [[Shell-Startup-Files]]
