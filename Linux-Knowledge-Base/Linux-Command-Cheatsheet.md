---
title: Linux Command Cheatsheet
aliases:
  - linux cheatsheet
  - คำสั่ง linux
  - linux commands
  - option ที่ใช้บ่อย
tags: [linux, reference, cheatsheet]
type: reference
status: published
---

# Linux Command Cheatsheet

คำสั่งพื้นฐาน + **option ที่ใช้จริงบ่อย** · ดู option ทั้งหมด: `man <คำสั่ง>` หรือ `<คำสั่ง> --help`

## ไฟล์และโฟลเดอร์

| คำสั่ง | Option ที่มีประโยชน์ |
|---|---|
| `ls` | `-l` รายละเอียด · `-a` รวมไฟล์ซ่อน · `-h` ขนาดอ่านง่าย · `-t` ใหม่สุดก่อน · `-S` ใหญ่สุดก่อน · `-r` กลับลำดับ → `ls -lahtr` |
| `cd` | `cd -` กลับโฟลเดอร์ก่อนหน้า · `cd` / `cd ~` กลับบ้าน |
| `pwd` | `-P` path จริง (ไม่ผ่าน symlink) |
| `mkdir` | `-p` สร้างซ้อนหลายชั้น ไม่ error ถ้ามีแล้ว |
| `cp` | `-r` ทั้งโฟลเดอร์ · `-a` เก็บ permission/เวลา · `-i` ถามก่อนทับ · `-v` แสดงที่ทำ |
| `mv` | `-i` ถามก่อนทับ · `-n` ไม่ทับเด็ดขาด |
| `rm` | `-r` ทั้งโฟลเดอร์ · `-f` ไม่ถาม · `-i` ถามทุกไฟล์ · ⚠️ ไม่มีถังขยะ |
| `ln` | `-s` สร้าง symlink: `ln -s <ของจริง> <ชื่อลิงก์>` |
| `tree` | `-L 2` ลึก 2 ชั้น · `-a` รวมซ่อน · `-I node_modules` ข้าม |

## อ่านและค้นหา

| คำสั่ง | Option ที่มีประโยชน์ |
|---|---|
| `cat` | `-n` เลขบรรทัด |
| `less` | `/คำ` ค้น · `n` ถัดไป · `G` ท้ายไฟล์ · `q` ออก · `+F` ตามดูสด |
| `head` / `tail` | `-n 50` จำนวนบรรทัด · `tail -f` ดู log สด · `tail -F` ตามต่อแม้ไฟล์ถูกหมุน |
| `grep` | `-r` ทั้งโฟลเดอร์ · `-i` ไม่สนตัวพิมพ์ · `-n` เลขบรรทัด · `-v` บรรทัดที่ไม่มี · `-l` แค่ชื่อไฟล์ · `-E` regex · `-C 3` บรรทัดรอบๆ |
| `find` | `-name "*.log"` · `-iname` · `-type f`/`d` · `-mtime -1` แก้ใน 1 วัน · `-size +100M` · `-delete` |
| `wc` | `-l` นับบรรทัด |
| `sort` / `uniq` | `sort -h` เรียงขนาด (1K, 2M) · `sort -n` ตัวเลข · `uniq -c` นับซ้ำ → `sort \| uniq -c \| sort -rn` |
| `du` | `-s` รวม · `-h` อ่านง่าย → `du -sh * \| sort -h` |
| `df` | `-h` อ่านง่าย · `-T` ชนิด filesystem |

## Permission และ User

| คำสั่ง | ใช้ |
|---|---|
| `chmod` | `chmod 600 file` (เจ้าของอ่าน/เขียน) · `chmod 755 dir` · `chmod +x script.sh` · `-R` ทั้งโฟลเดอร์ |
| `chown` | `sudo chown user:group file` · `-R` ทั้งโฟลเดอร์ |
| `sudo` | `sudo -i` เป็น root แบบ login · `sudo !!` รันคำสั่งเมื่อกี้ด้วย sudo |
| `id` / `whoami` / `groups` | ดูตัวเองเป็นใคร อยู่กลุ่มไหน |

ตัวเลข permission: `r=4 w=2 x=1` รวมกันต่อกลุ่ม (เจ้าของ/กลุ่ม/คนอื่น) → `750` = `rwx r-x ---`

## Process และ Port

| คำสั่ง | Option ที่มีประโยชน์ |
|---|---|
| `ps` | `ps aux` ทุก process · `ps aux \| grep node` |
| `pgrep` / `pkill` | `pgrep -fl node` หา PID ตามชื่อ · `pkill -f "npm run dev"` |
| `kill` | `kill <PID>` ขอให้ปิด · `kill -9 <PID>` บังคับ (ใช้เมื่อแบบแรกไม่ได้) |
| `top` / `htop` | `P` เรียง CPU · `M` เรียง RAM · `q` ออก |
| `ss` (Linux) | `sudo ss -tlnp` port ที่เปิดรอ + โปรแกรม |
| `lsof` | `lsof -nP -iTCP:3000 -sTCP:LISTEN` ใครใช้ port 3000 (ใช้ได้บน macOS) |
| `systemctl` | `status` / `start` / `stop` / `restart` / `enable --now` / `--failed` |
| `journalctl` | `-u nginx` เฉพาะ service · `-f` ดูสด · `-n 100` · `--since "1 hour ago"` |

## Network

| คำสั่ง | Option ที่มีประโยชน์ |
|---|---|
| `curl` | `-I` แค่ header · `-L` ตาม redirect · `-s` เงียบ · `-o file` บันทึก · `-v` debug · `-X POST -d '{}' -H 'Content-Type: application/json'` |
| `wget` | `-c` ดาวน์โหลดต่อ |
| `ping` | `-c 4` ส่ง 4 ครั้งแล้วหยุด |
| `ip` | `ip a` ดู IP · `ip r` ดู route |
| `nc` | `nc -vz host 22` เช็กว่า port เปิดไหม |
| `dig` | `dig +short example.com` ดู DNS |

## บีบอัด

```bash
tar -czvf backup.tar.gz folder/     # สร้าง  (c=create z=gzip v=verbose f=file)
tar -xzvf backup.tar.gz             # แตก    (x=extract)
tar -tzvf backup.tar.gz             # ดูข้างในโดยไม่แตก
zip -r out.zip folder/ && unzip out.zip
```

## Pipe และ Redirect

| เขียน | ความหมาย |
|---|---|
| `a \| b` | ส่งผลของ a ให้ b |
| `> file` / `>> file` | เขียนทับ / ต่อท้าย |
| `2>&1` | รวม error เข้ากับ output ปกติ |
| `> /dev/null 2>&1` | ทิ้งทุก output |
| `a && b` / `a \|\| b` | b รันเมื่อ a สำเร็จ / ล้มเหลว |
| `cmd \| tee file` | ดูบนจอ + บันทึกไฟล์พร้อมกัน |

## คีย์ลัดใน Terminal

| คีย์ | ทำอะไร |
|---|---|
| `Tab` (2 ครั้ง) | เติมชื่อ / แสดงตัวเลือก |
| `Ctrl+C` | หยุดคำสั่งที่รันอยู่ |
| `Ctrl+R` | ค้นประวัติคำสั่ง |
| `Ctrl+A` / `Ctrl+E` | ไปต้น / ท้ายบรรทัด |
| `Ctrl+U` / `Ctrl+W` | ลบทั้งบรรทัด / ลบคำก่อนหน้า |
| `Ctrl+L` | ล้างจอ |
| `Ctrl+D` | ออกจาก shell |
| `!!` / `!$` | คำสั่งล่าสุด / argument ท้ายของคำสั่งล่าสุด |

## ข้อมูลเครื่อง

`hostname` · `uname -a` · `cat /etc/os-release` → ดู [[Linux-Check-System-Info]]
