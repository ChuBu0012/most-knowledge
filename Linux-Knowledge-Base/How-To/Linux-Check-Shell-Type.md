---
title: "How-To: เช็กว่าตอนนี้อยู่ใน shell อะไร แบบไหน และโหลดไฟล์ไหนบ้าง"
aliases:
  - เช็ก shell
  - ตอนนี้ใช้ bash หรือ zsh
  - login shell หรือเปล่า
  - debug bashrc
tags: [linux, how-to, shell]
type: how-to
status: published
---

# เช็กว่าอยู่ใน shell อะไร แบบไหน

## shell อะไร

```bash
ps -p $$ -o comm=     # shell ที่รันอยู่จริง
echo $SHELL           # shell เริ่มต้นของ user (อาจไม่ใช่ตัวที่รันอยู่)
```

## login / interactive ไหม

```bash
# bash
shopt -q login_shell && echo login || echo non-login
[[ $- == *i* ]] && echo interactive || echo non-interactive

# zsh
[[ -o login ]] && echo login || echo non-login
[[ -o interactive ]] && echo interactive || echo non-interactive
```

## ไฟล์ไหนถูกโหลดจริง (debug)

ใส่บรรทัดนี้ไว้บนสุดของแต่ละไฟล์ชั่วคราว:

```bash
echo "loaded: ~/.bashrc"        # ใน .bashrc
echo "loaded: ~/.profile"       # ใน .profile
```

เปิดหน้าต่างใหม่ / `ssh lab` แล้วดูว่าขึ้นอะไรบ้าง — **ลบออกเมื่อเสร็จ** (echo ใน `.bashrc` ทำให้ `scp`/`rsync` พังได้)

หรือให้ bash แสดงทุกบรรทัดที่รันตอนเปิด:

```bash
bash -lix -c exit 2>&1 | grep -E "^\++ *(\.|source)"
```

## เปลี่ยน shell เริ่มต้น

```bash
chsh -s "$(command -v zsh)"     # หรือ bash · มีผลเมื่อ login ใหม่
```

## ลึกกว่านี้

[[Shell-Types-Login-Interactive]] · [[Terminal-Shell-and-TTY]]
