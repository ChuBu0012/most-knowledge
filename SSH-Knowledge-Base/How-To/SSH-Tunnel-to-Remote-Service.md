---
title: "How-To: เปิด Tunnel เข้า Database / Web ที่อยู่บน Server"
aliases:
  - ssh tunnel
  - port forward
  - ssh -L
  - ต่อ database ผ่าน ssh
  - เปิดเว็บบน server จากเครื่องเรา
tags:
  - ssh
  - how-to
  - port-forwarding
type: how-to
status: published
---

# เปิด Tunnel เข้า Service บน Server (`ssh -L`)

> **ใช้เมื่อ:** Postgres / Redis / เว็บ Admin รันอยู่บน Server แต่เปิดให้แค่ `localhost` ของ Server และอยากใช้จากเครื่องเรา

## สูตร

```text
ssh -L <พอร์ตเครื่องเรา>:<ปลายทางมองจาก Server>:<พอร์ตปลายทาง> <server>
```

## ตัวอย่างที่ใช้บ่อย

💻 **เครื่องเรา**

```bash
# Postgres บน server → ใช้ที่ localhost:5432 ของเรา
ssh -N -L 5432:127.0.0.1:5432 lab

# เว็บ dev server port 3000 บน server → เปิด http://localhost:8080
ssh -N -L 8080:127.0.0.1:3000 lab

# DB อีกเครื่องที่ Server มองเห็นแต่เรามองไม่เห็น
ssh -N -L 5433:10.0.0.12:5432 lab
```

`-N` = ไม่เปิด shell แค่ถือ Tunnel ไว้ · ปิดด้วย `Ctrl+C`

รันเป็น Background:

```bash
ssh -f -N -o ExitOnForwardFailure=yes -L 5432:127.0.0.1:5432 lab
```

## ตรวจว่าสำเร็จ

```bash
lsof -nP -iTCP:5432 -sTCP:LISTEN     # ต้องเห็น ssh ฟังพอร์ตนี้
psql -h 127.0.0.1 -p 5432 -U postgres
curl -I http://localhost:8080
```

## ปิด Tunnel ที่รัน Background

```bash
lsof -nP -iTCP:5432 -sTCP:LISTEN     # ดู PID ของ ssh
kill <PID>
```

## ถ้าไม่ได้

| อาการ | แก้ |
|---|---|
| `bind: Address already in use` | พอร์ตเครื่องเราถูกใช้แล้ว เปลี่ยนเลขซ้าย เช่น `15432:...` |
| ต่อ Tunnel ได้ แต่ `channel open failed: connect failed` | Service บน Server ไม่ได้ฟังที่ปลายทางที่ระบุ → บน Server รัน `ss -tlnp` |

## แบบอื่น

- ให้ Server เข้ามาหาเครื่องเรา (`-R`) → [[SSH-Remote-Port-Forwarding]]
- ใช้ Server เป็น Proxy ทั้งเครื่อง (`-D`) → [[SSH-Dynamic-Port-Forwarding-and-SOCKS5]]

## ลึกกว่านี้

- [[SSH-Local-Port-Forwarding]]
- [[Localhost-Loopback-and-Port-Binding]] — `localhost` คือเครื่องไหน
