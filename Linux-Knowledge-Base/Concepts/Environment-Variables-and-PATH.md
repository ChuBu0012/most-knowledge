---
title: "Environment Variables และ PATH ทำงานยังไง"
aliases:
  - environment variable
  - ตัวแปร env
  - PATH คืออะไร
  - export
  - command not found
tags: [linux, concept, shell, environment]
type: concept
status: published
---

# Environment Variables และ PATH

## ตัวแปร shell vs environment variable

```bash
NAME=dev          # ตัวแปร shell: เห็นแค่ใน shell นี้
export NAME=dev   # environment variable: ส่งต่อให้โปรแกรม/shell ลูกที่เปิดจากที่นี่
```

```bash
X=1;        bash -c 'echo $X'   # ว่าง   (ลูกไม่เห็น)
export X=1; bash -c 'echo $X'   # 1
X=2 bash -c 'echo $X'           # 2      (ตั้งให้เฉพาะคำสั่งนี้คำสั่งเดียว)
```

Environment **ไหลจากแม่ไปลูกเท่านั้น** — ลูกแก้ตัวแปรแล้วแม่ไม่เห็น
นี่คือเหตุผลที่ `./set-env.sh` ไม่มีผล แต่ `source set-env.sh` มีผล (`source` รันใน shell ปัจจุบัน ไม่เปิดลูก)

และ `export` ในหน้าต่างหนึ่ง **หายเมื่อปิดหน้าต่าง** — อยากให้ถาวรต้องเขียนลงไฟล์ startup ([[Shell-Startup-Files]])

## PATH

`PATH` = รายชื่อโฟลเดอร์คั่นด้วย `:` ที่ shell ไล่หาโปรแกรม **จากซ้ายไปขวา เจอตัวแรกใช้ตัวนั้น**

```bash
echo "$PATH" | tr ':' '\n'
# /opt/homebrew/bin    ← หาที่นี่ก่อน
# /usr/local/bin
# /usr/bin
# /bin
```

พิมพ์ `python3` → shell หา `/opt/homebrew/bin/python3` ก่อน ถ้าไม่มีค่อยไป `/usr/bin/python3`

| คำสั่ง | บอกอะไร |
|---|---|
| `command -v node` | path ของโปรแกรมที่จะถูกรันจริง (ใช้ใน script ได้) |
| `type node` | บอกด้วยว่าเป็น alias / function / builtin / ไฟล์ |
| `which -a python3` | ทุกตัวที่เจอใน PATH ตามลำดับ |
| `hash -r` (bash) / `rehash` (zsh) | ล้าง cache หลังติดตั้งโปรแกรมใหม่แล้วยังหาไม่เจอ |

## ตัวแปรที่ควรรู้จัก

| ตัวแปร | ความหมาย |
|---|---|
| `HOME` | โฟลเดอร์บ้าน (`~`) |
| `USER` | ชื่อ user |
| `SHELL` | shell เริ่มต้นของ user |
| `PATH` | ที่หาโปรแกรม |
| `EDITOR` | editor ที่โปรแกรมอื่นเรียกใช้ (git commit, crontab -e) |
| `LANG` | ภาษา/encoding เช่น `en_US.UTF-8` |
| `PWD` | โฟลเดอร์ปัจจุบัน |

ดูทั้งหมด: `env` หรือ `printenv` · ดูตัวเดียว: `printenv PATH`

## ต่อไป

- ลงมือทำ: [[Linux-Add-to-PATH]] · [[Linux-Add-Alias-and-Env-Var]]
- [[Shell-Types-Login-Interactive]] — ทำไม PATH ใน cron/script ไม่เหมือนใน Terminal
