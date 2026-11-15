---
title: "How-To: ตั้ง alias / ตัวแปรให้ถาวร (ควรใส่ไฟล์ไหน)"
aliases:
  - ตั้ง alias
  - alias ถาวร
  - export ถาวร
  - ใส่ใน bashrc หรือ profile
  - source bashrc
  - reload shell
tags: [linux, how-to, shell]
type: how-to
status: published
---

# ตั้ง alias / ตัวแปรให้ถาวร

## 1. ใช้ shell อะไรอยู่

```bash
ps -p $$ -o comm=     # bash หรือ zsh
```

## 2. เลือกไฟล์

| จะใส่ | bash (Ubuntu) | zsh (macOS) |
|---|---|---|
| `alias`, function, prompt | `~/.bashrc` | `~/.zshrc` |
| `export` ตัวแปร, `PATH` | `~/.profile` | `~/.zprofile` |

> ⚠️ Ubuntu: อย่าสร้าง `~/.bash_profile` ใหม่ ถ้ามี ไฟล์ `~/.profile` จะถูกเมิน
> (ถ้ามีอยู่แล้ว ต้องมีบรรทัด `[ -f ~/.profile ] && . ~/.profile` ในนั้น)

## 3. เพิ่มต่อท้ายไฟล์

```bash
nano ~/.bashrc        # หรือ ~/.zshrc
```

ตัวอย่างที่มีประโยชน์:

```bash
# alias
alias ll='ls -lah'
alias ..='cd ..'
alias gs='git status'
alias ports='sudo ss -tlnp'          # macOS: lsof -nP -iTCP -sTCP:LISTEN

# function (ทำได้มากกว่า alias เพราะรับ argument ได้)
mkcd() { mkdir -p "$1" && cd "$1"; }
```

```bash
nano ~/.profile       # หรือ ~/.zprofile
```

```bash
export EDITOR=nano
export LANG=en_US.UTF-8
```

> เขียน `alias x='...'` **ห้ามมีช่องว่างรอบ `=`** · `export A=1` ก็เช่นกัน

## 4. ให้มีผลทันที (ไม่ต้องเปิดหน้าต่างใหม่)

```bash
source ~/.bashrc         # หรือ source ~/.zshrc
# แก้ไฟล์ profile → ต้อง login ใหม่ หรือ:
exec $SHELL -l
```

## ตรวจ

```bash
type ll          # ll is aliased to `ls -lah'
echo $EDITOR
```

## ถ้าไม่ได้

- ใช้ใน script ไม่ได้ → ปกติ alias ไม่ทำงานใน script ใช้ชื่อคำสั่งเต็ม หรือเขียนเป็น script แยก → [[Linux-Fix-Command-Not-Found-in-Script]]
- macOS ใช้ bash แล้ว `.bashrc` ไม่โหลด → Terminal เปิด login shell ใส่ใน `~/.bash_profile` แทน

## ลึกกว่านี้

[[Shell-Startup-Files]] · [[Shell-Types-Login-Interactive]]
