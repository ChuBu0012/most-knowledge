---
title: SSH Daily Playbook
tags:
  - ssh
  - daily-use
  - workflow
  - playbook
type: guide
status: published
---

# SSH Daily Playbook

คู่มือใช้งาน SSH ในชีวิตประจำวัน แยก “เชื่อมต่อ”, “ส่งไฟล์”, “ทำ Tunnel” และ “แก้ปัญหา” ให้หยิบใช้ได้ทันที

กลับไปยังแผนที่รวม: [[START-HERE]]

## 1. เชื่อมต่อครั้งแรก

```bash
ssh-keygen -t ed25519 -C "<comment>" -f ~/.ssh/<key_name>
chmod 700 ~/.ssh
chmod 600 ~/.ssh/<key_name>
ssh-copy-id -i ~/.ssh/<key_name>.pub <user>@<host>
ssh <user>@<host>
```

ติดตั้งเฉพาะ Public Key เท่านั้น ห้ามคัดลอก Private Key ไปยัง Server

## 2. ตั้ง Alias เพื่อใช้ทุกวัน

เพิ่มใน `~/.ssh/config`:

```sshconfig
Host <alias>
    HostName <host>
    User <user>
    IdentityFile ~/.ssh/<key_name>
    IdentitiesOnly yes
    ServerAliveInterval 60
```

จากนั้นใช้:

```bash
ssh <alias>
```

ตรวจค่าที่ SSH จะใช้จริงด้วย `ssh -G <alias>`

## 3. ส่งและดึงไฟล์

ส่งไฟล์จาก Client ไป Server:

```bash
scp ./local-file <alias>:/tmp/
```

ดึงไฟล์จาก Server มา Client:

```bash
scp <alias>:/tmp/remote-file ./
```

ส่งหรือดึงทั้งโฟลเดอร์ด้วย `-r`:

```bash
scp -r ./local-folder <alias>:/tmp/
scp -r <alias>:/tmp/remote-folder ./
```

ถ้าต้อง browse หรือจัดการหลายไฟล์ใน Session เดียว:

```bash
sftp <alias>
```

รายละเอียดอยู่ที่ [[SSH-SCP-File-Transfer]] และ [[SSH-SFTP-File-Transfer]]

## 4. ใช้งานคำสั่งบน Server

```bash
ssh <alias>
ssh <alias> "uptime"
scp ./local-file <alias>:/tmp/
scp <alias>:/tmp/remote-file ./
```

## 5. เปิด Tunnel

### เข้าถึง Service ฝั่ง Server จากเครื่องเรา (`-L`)

```bash
ssh -N -o ExitOnForwardFailure=yes \
  -L <local_port>:<destination_host>:<destination_port> <alias>
```

### ให้ Server เข้าถึง Service ฝั่งเรา (`-R`)

```bash
ssh -N -o ExitOnForwardFailure=yes \
  -R <remote_port>:127.0.0.1:<local_port> <alias>
```

### ใช้ Server เป็น SOCKS5 Proxy (`-D`)

```bash
ssh -N -D <local_port> <alias>
curl --socks5-hostname 127.0.0.1:<local_port> https://example.com
```

รายละเอียดของ `-L`, `-R` และ `-D` อยู่ใน [[SSH-Local-Port-Forwarding]], [[SSH-Remote-Port-Forwarding]] และ [[SSH-Dynamic-Port-Forwarding-and-SOCKS5]]

## 6. Debug และปิด Tunnel

```bash
ssh -vvv <alias>
lsof -nP -iTCP:<local_port> -sTCP:LISTEN
kill <verified-pid>
```

ตรวจ PID ก่อน `kill` ทุกครั้ง และอย่าใช้คำสั่งที่ปิด SSH ทุก Process พร้อมกัน

## 7. Error ที่พบบ่อย

| อาการ | เปิดดู |
|---|---|
| `Permission denied (publickey)` | [[SSH-Common-Misconceptions-and-Troubleshooting]] |
| `Connection refused` | [[Localhost-Loopback-and-Port-Binding]] |
| `Connection timed out` | [[SSH-Common-Misconceptions-and-Troubleshooting]] |
| `REMOTE HOST IDENTIFICATION HAS CHANGED` | ยืนยัน Fingerprint ก่อนใช้ `ssh-keygen -R` |
| Tunnel ต่อได้แต่เข้า Service ไม่ได้ | [[SSH-Local-Port-Forwarding]] |
| ส่ง/ดึงไฟล์ไม่ได้ | [[SSH-SCP-File-Transfer]] หรือ [[SSH-SFTP-File-Transfer]] |

## ไปต่อ

- [[SSH-Command-Reference-and-Cheatsheet]] — Reference ครบชุด
- [[SSH-Handshake-and-Authentication-Anatomy]] — เข้าใจการ Login
- [[SSH-Agent-and-Memory-Security]] — จัดการ Key ใน Agent
- [[SSH-SCP-File-Transfer]] — ส่งไฟล์แบบคำสั่งเดียว
- [[SSH-SFTP-File-Transfer]] — จัดการไฟล์แบบ Interactive
