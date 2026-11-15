---
title: "How-To: ส่ง / ดึงไฟล์กับ Server"
aliases:
  - scp
  - rsync
  - ส่งไฟล์ไป server
  - ดึงไฟล์จาก server
  - copy file ssh
tags:
  - ssh
  - how-to
  - file-transfer
type: how-to
status: published
---

# ส่ง / ดึงไฟล์กับ Server

> **จำง่าย:** `scp <ต้นทาง> <ปลายทาง>` — ฝั่งที่มี `server:` คือฝั่ง Server

💻 ทุกคำสั่ง **รันบนเครื่องเรา** (ไม่ใช่ใน Server)

## ไฟล์เดียว

```bash
scp ./report.pdf lab:/home/chubu/          # ส่งขึ้น
scp lab:/var/log/syslog ./                 # ดึงลง
```

## ทั้งโฟลเดอร์

```bash
scp -r ./project lab:/home/chubu/
scp -r lab:/home/chubu/project ./
```

## โฟลเดอร์ใหญ่ / ส่งซ้ำบ่อย → ใช้ `rsync` (ส่งเฉพาะที่เปลี่ยน, ต่อได้ถ้าหลุด)

```bash
rsync -avzP ./project/ lab:/home/chubu/project/
rsync -avzP lab:/home/chubu/project/ ./project/
```

> `/` ท้าย `./project/` = ส่ง "ของข้างใน" ไม่ใส่ `/` = ส่ง "โฟลเดอร์ทั้งก้อน" ไปซ้อนอีกชั้น

ลองดูก่อนว่าจะส่งอะไร (ไม่ส่งจริง): เติม `--dry-run`

## ถ้าไม่ได้ตั้ง alias

แทน `lab` ด้วย `chubu@192.168.64.8` และถ้า port ไม่ใช่ 22:

```bash
scp -P 2222 ./file chubu@192.168.64.8:/tmp/     # scp ใช้ -P ตัวใหญ่
rsync -avzP -e "ssh -p 2222" ./dir/ chubu@192.168.64.8:/tmp/dir/
```

## ลึกกว่านี้

- [[SSH-SCP-File-Transfer]] · [[SSH-SFTP-File-Transfer]]
