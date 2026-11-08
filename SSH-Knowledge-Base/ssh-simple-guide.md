---
title: SSH Simple Guide
tags:
  - ssh
  - cheatsheet
  - quickstart
type: guide
status: published
---

# SSH Cheat Sheet

	> [!tip] ถ้ากำลังทำงานจริง
	> เปิด [[SSH-Daily-Playbook]] ก่อน หน้านี้เป็น Reference แบบละเอียดสำหรับอ่านต่อและค้นคำสั่ง

คู่มือคำสั่ง SSH สำหรับใช้งานและอ้างอิงอย่างรวดเร็ว  
ตัวอย่างใช้ชื่อแทน เช่น `<user>`, `<host>`, `<ip>`, `<port>` และ `<key>` ไม่มีการผูกกับเครื่องหรือ Host ใดโดยเฉพาะ

## 1. รูปแบบคำสั่งพื้นฐาน

```bash
# เชื่อมต่อด้วย username และ hostname/IP
ssh <user>@<host>

# ระบุพอร์ต
ssh -p <port> <user>@<host>

# ระบุ Private Key
ssh -i ~/.ssh/<private_key> <user>@<host>

# รันคำสั่งบนเครื่องปลายทางโดยไม่เปิด interactive shell
ssh <user>@<host> "uptime"

# เปิด pseudo-terminal เมื่อต้องรันคำสั่งที่ใช้ sudo หรือ interactive
ssh -t <user>@<host> "sudo systemctl status <service>"

# ออกจาก session
exit

# ตัด SSH session ที่ค้าง: กด Enter แล้วพิมพ์ ~.
```

## 2. สร้างและจัดการ SSH Key

```bash
# สร้าง ED25519 key pair
ssh-keygen -t ed25519 -C "<key_comment>" -f ~/.ssh/<key_name>

# แสดง Public Key
cat ~/.ssh/<key_name>.pub

# สร้าง Public Key ใหม่จาก Private Key
ssh-keygen -y -f ~/.ssh/<key_name>

# แสดง Fingerprint
ssh-keygen -lf ~/.ssh/<key_name>.pub

# เปลี่ยนหรือเพิ่ม Passphrase ของ Private Key
ssh-keygen -p -f ~/.ssh/<key_name>
```

**ไฟล์สำคัญ**

| ไฟล์ | ใช้ทำอะไร |
|---|---|
| `~/.ssh/<key_name>` | Private Key เก็บเป็นความลับ |
| `~/.ssh/<key_name>.pub` | Public Key นำไปติดตั้งบน Server |
| `~/.ssh/authorized_keys` | Public Keys ที่อนุญาตให้ User นั้น Login |
| `~/.ssh/known_hosts` | Host Keys ของ Server ที่เคยเชื่อมต่อ |
| `~/.ssh/config` | Client-side SSH configuration |

### ติดตั้ง Public Key บน Server

ถ้ามี `ssh-copy-id` ติดตั้งอยู่:

```bash
ssh-copy-id -i ~/.ssh/<key_name>.pub <user>@<host>
```

วิธีติดตั้งด้วยตนเอง:

```bash
# บน Client: แสดงและคัดลอก Public Key
cat ~/.ssh/<key_name>.pub
```

บน Server ให้เพิ่ม Public Key เป็นหนึ่งบรรทัดใน `~/.ssh/authorized_keys` ของ User เป้าหมาย แล้วตั้ง Permission:

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
nano ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

> ติดตั้งเฉพาะ Public Key (`.pub`) เท่านั้น ห้ามคัดลอก Private Key ไปยัง Server

## 3. SSH File Permissions

ตัวอย่าง Permission ที่ใช้กันทั่วไป:

```bash
# บน Client
chmod 700 ~/.ssh
chmod 600 ~/.ssh/<private_key>
chmod 644 ~/.ssh/<private_key>.pub
chmod 600 ~/.ssh/config

# บน Server (รันใน account ของ User เป้าหมาย)
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

หากไฟล์หรือโฟลเดอร์เป็นเจ้าของผิด User ให้ตรวจสอบก่อนแก้ด้วย `chown` อย่าคัดลอกคำสั่งเปลี่ยนเจ้าของโดยไม่ตรวจสอบ Path และ User เป้าหมาย

## 4. SSH Client Config

ไฟล์: `~/.ssh/config`

```sshconfig
Host <alias>
    HostName <hostname_or_ip>
    User <username>
    Port <port>
    IdentityFile ~/.ssh/<private_key>
    IdentitiesOnly yes

Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
    ForwardAgent no
```

จากนั้นเชื่อมต่อด้วย Alias:

```bash
ssh <alias>
```

ตรวจสอบค่าที่ SSH ใช้จริง:

```bash
ssh -G <alias>
ssh -G <alias> | grep -E 'hostname|user|port|identityfile'
```

ตั้ง Permission ของ Config:

```bash
chmod 600 ~/.ssh/config
```

## 5. SSH Agent และ Passphrase

SSH Agent ช่วยใช้ Private Key ที่ปลดล็อกแล้ว โดยไม่ต้องกรอก Passphrase ทุกครั้งในระหว่างที่ Key ยังอยู่ใน Agent

```bash
# ตรวจสอบ Key ที่โหลดอยู่ (แสดง Fingerprint)
ssh-add -l

# แสดง Public Keys ที่ Agent มี
ssh-add -L

# เพิ่ม Private Key เข้า Agent
ssh-add ~/.ssh/<private_key>

# เพิ่ม Key พร้อมกำหนดอายุ เช่น 4 ชั่วโมง
ssh-add -t 4h ~/.ssh/<private_key>

# นำ Key หนึ่งรายการออกจาก Agent
ssh-add -d ~/.ssh/<private_key>

# นำทุก Key ออกจาก Agent
ssh-add -D
```

บน macOS สามารถเพิ่ม Key เข้า Apple Keychain ได้:

```bash
ssh-add --apple-use-keychain ~/.ssh/<private_key>
```

> `ssh-add -D` เอา Key ออกจาก Agent เท่านั้น ไม่ได้ลบไฟล์ Private Key บน Disk

## 6. SSH Port Forwarding

### Local Port Forwarding (`-L`)

ใช้เมื่อ Client ต้องการเข้าถึง Service ที่อยู่ฝั่ง Server หรือ Network ที่ Server เข้าถึงได้

```bash
ssh -L <local_port>:<destination_host>:<destination_port> <user>@<host>
```

ตัวอย่าง:

```bash
ssh -N -L 8080:127.0.0.1:8000 <user>@<host>
```

เปิดบน Client:

```text
http://127.0.0.1:8080
```

ในตัวอย่างนี้ `127.0.0.1:8000` คือปลายทางที่ฝั่ง Server เป็นผู้เชื่อมต่อไปหา

### Remote Port Forwarding (`-R`)

ใช้เมื่อฝั่ง Server ต้องการเข้าถึง Service ที่อยู่ฝั่ง Client

```bash
ssh -R <remote_port>:<destination_host>:<destination_port> <user>@<host>
```

ตัวอย่าง:

```bash
ssh -N -R 9000:127.0.0.1:3000 <user>@<host>
```

บน Server ทดสอบ:

```bash
curl http://127.0.0.1:9000
```

ในตัวอย่างนี้ `127.0.0.1:3000` คือ Service ที่ฝั่ง Client เป็นผู้เชื่อมต่อไปหา ส่วน Remote Port โดยปกติจะ Listen บน Loopback ของ Server

### Dynamic Port Forwarding (`-D`)

สร้าง SOCKS Proxy บน Client เพื่อให้ Application ส่ง Traffic ไปยังปลายทางที่เลือกผ่าน SSH Server

```bash
ssh -N -D 1080 <user>@<host>
```

ทดสอบด้วย curl:

```bash
curl --socks5-hostname 127.0.0.1:1080 https://example.com
```

`--socks5-hostname` ให้การ resolve ชื่อ Domain ทำผ่าน Proxy ด้วย

### รัน Tunnel แบบ Background

เพิ่ม `-f` และ `-N`:

```bash
ssh -f -N -L <local_port>:<destination_host>:<destination_port> <user>@<host>
ssh -f -N -R <remote_port>:<destination_host>:<destination_port> <user>@<host>
ssh -f -N -D <local_port> <user>@<host>
```

แนะนำเพิ่ม `ExitOnForwardFailure` เพื่อให้ SSH ออกจากการทำงานเมื่อสร้าง Forward ไม่สำเร็จ:

```bash
ssh -f -N -o ExitOnForwardFailure=yes -L <local_port>:<destination_host>:<destination_port> <user>@<host>
```

ตรวจสอบและปิด Tunnel บน Client:

```bash
# ตรวจสอบ Process ที่ Listen บน Port
lsof -nP -iTCP:<local_port> -sTCP:LISTEN

# ดู Process ที่เกี่ยวข้อง
pgrep -af ssh

# ปิดด้วย PID ที่ตรวจสอบแล้ว
kill <pid>
```

> หลีกเลี่ยง `pkill -f "ssh.*-N"` หากมี SSH Tunnel หลายรายการ เพราะอาจปิด Tunnel อื่นโดยไม่ตั้งใจ

## 7. localhost และ Address ที่พบบ่อย

| Address | ความหมาย |
|---|---|
| `localhost` | Hostname ที่อ้างถึงเครื่องตัวเอง โดยปกติ resolve เป็น `127.0.0.1` และ/หรือ `::1` |
| `127.0.0.1` | IPv4 Loopback ของเครื่องตัวเอง |
| `::1` | IPv6 Loopback ของเครื่องตัวเอง |
| `0.0.0.0` | ใช้เป็น Bind Address เพื่อ Listen บนทุก IPv4 Interface |
| `<LAN_IP>` | IP ของเครื่องบนเครือข่ายภายใน |

**จำไว้:** `localhost` หมายถึงเครื่องที่กำลังประมวลผลการเชื่อมต่อนั้น ไม่ได้หมายถึงเครื่องต้นทางหรือปลายทางโดยอัตโนมัติ ต้องดูว่า Service หรือคำสั่งกำลังทำงานอยู่ที่ฝั่งใด

## 8. Server: OpenSSH Service และ Configuration (Ubuntu)

```bash
# ตรวจสอบสถานะ Service
sudo systemctl status ssh

# เริ่ม / หยุด / Restart / Reload
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl restart ssh
sudo systemctl reload ssh

# ตรวจสอบ Syntax ของ Server Config
sudo sshd -t

# แสดง Effective Configuration
sudo sshd -T

# ดู Log แบบ Real-time
sudo journalctl -u ssh -f

# ดู Listening Ports
sudo ss -tulpn | grep sshd
```

ไฟล์หลักของ Server:

```text
/etc/ssh/sshd_config
/etc/ssh/sshd_config.d/
```

ก่อนแก้ Configuration:

1. สำรองไฟล์เดิม
2. คง Session SSH เดิมไว้
3. ตรวจ Syntax ด้วย `sudo sshd -t`
4. Reload Service
5. เปิด Terminal ใหม่เพื่อทดสอบ Login
6. ปิด Session เดิมเมื่อยืนยันว่าเข้าใหม่ได้แล้ว

ตัวอย่างค่าที่เกี่ยวกับ Authentication:

```sshconfig
PubkeyAuthentication yes
PasswordAuthentication no
KbdInteractiveAuthentication no
PermitRootLogin no
```

> อย่าปิด Password Authentication จนกว่าจะทดสอบ Public Key Login สำเร็จและมีช่องทางเข้าถึง Console สำรอง การตั้งค่าจริงอาจได้รับผลจากไฟล์ Drop-in และลำดับการอ่าน Configuration

## 9. Firewall: UFW (Ubuntu)

```bash
# ดูสถานะและกฎ
sudo ufw status verbose
sudo ufw status numbered

# อนุญาต SSH ก่อนเปิด Firewall
sudo ufw allow <ssh_port>/tcp

# เปิดใช้งาน UFW
sudo ufw enable

# อนุญาตเฉพาะ Source IP
sudo ufw allow from <source_ip> to any port <ssh_port> proto tcp

# ลบกฎโดยระบุหมายเลข (ตรวจรายการก่อนทุกครั้ง)
sudo ufw status numbered
sudo ufw delete <rule_number>
```

> ก่อนเปิดหรือแก้ Firewall ผ่าน SSH ต้องแน่ใจว่าได้อนุญาต Port ที่ใช้เชื่อมต่อแล้ว เพื่อป้องกันการตัดตัวเองออกจาก Server

## 10. Troubleshooting

| อาการ | จุดที่ควรตรวจ |
|---|---|
| `Permission denied (publickey)` | User, Key ที่ Client เสนอ, `authorized_keys`, Ownership และ Permission |
| `Connection refused` | IP/Port ถูกต้องหรือไม่ และ `sshd` กำลัง Listen อยู่หรือไม่ |
| `Connection timed out` | Network Route, Firewall, Security Group และ IP ปลายทาง |
| `Host key verification failed` | ตรวจสอบ Host Key ของ Server ผ่านช่องทางที่เชื่อถือได้ก่อนแก้ `known_hosts` |
| `REMOTE HOST IDENTIFICATION HAS CHANGED` | อาจเกิดจาก Server เปลี่ยน Host Key หรือมีความเสี่ยงถูกแทรกกลาง ต้องยืนยัน Fingerprint ใหม่ก่อน |
| `The agent has no identities` | ตรวจ `ssh-add -l` และเพิ่ม Key ด้วย `ssh-add` |
| `Address already in use` | ตรวจว่า Port ถูกใช้งานอยู่หรือมี Tunnel เดิมค้างอยู่ |
| Tunnel เชื่อมต่อได้แต่ Service ใช้ไม่ได้ | ตรวจ Destination Host/Port และ Service ว่า Listen อยู่บน Address ที่ถูกต้อง |

คำสั่งวิเคราะห์เพิ่มเติม:

```bash
# Client: Debug การเชื่อมต่อ
ssh -v <user>@<host>
ssh -vvv <user>@<host>

# Client: ตรวจ Host Key ที่บันทึกไว้
ssh-keygen -F <host>

# Client: ลบ Host Key เก่า เฉพาะหลังยืนยัน Fingerprint ใหม่แล้ว
ssh-keygen -R <host>

# Server: ตรวจ Log
sudo journalctl -u ssh -n 100 --no-pager

# Server: ตรวจ Port ที่ Listen
sudo ss -tulpn
```

## 11. Security Checklist

- [ ] ใช้ Key Authentication และเลือก Key Type ที่เหมาะสม
- [ ] ตั้ง Passphrase ให้ Private Key
- [ ] ไม่ส่งหรือเก็บ Private Key บน Server
- [ ] ตั้ง Permission ของ `~/.ssh` และไฟล์สำคัญให้เหมาะสม
- [ ] ตรวจ Host Key ก่อนยอมรับ Server ครั้งแรก
- [ ] จำกัด User ที่ได้รับอนุญาตตามความจำเป็น
- [ ] ปิด Password Authentication เมื่อยืนยันว่า Key Login และช่องทางสำรองใช้งานได้
- [ ] ปิด Root Login โดยตรงเมื่อเหมาะสมกับระบบ
- [ ] ไม่เปิด Agent Forwarding โดยไม่จำเป็น
- [ ] จำกัด Port Forwarding และ Firewall ตามความจำเป็น
- [ ] อัปเดต OpenSSH และระบบปฏิบัติการสม่ำเสมอ

---

## 12. คำสั่งที่ใช้บ่อยที่สุด

| งาน | คำสั่ง |
|---|---|
| เชื่อมต่อ | `ssh <user>@<host>` |
| ระบุ Port | `ssh -p <port> <user>@<host>` |
| สร้าง Key | `ssh-keygen -t ed25519` |
| แสดง Public Key | `cat ~/.ssh/<key>.pub` |
| ติดตั้ง Public Key | `ssh-copy-id <user>@<host>` |
| ดู Fingerprint | `ssh-keygen -lf ~/.ssh/<key>.pub` |
| เพิ่ม Key เข้า Agent | `ssh-add ~/.ssh/<key>` |
| ดู Key ใน Agent | `ssh-add -l` |
| Debug | `ssh -vvv <user>@<host>` |
| Local Forward | `ssh -L <local_port>:<dest_host>:<dest_port> <user>@<host>` |
| Remote Forward | `ssh -R <remote_port>:<dest_host>:<dest_port> <user>@<host>` |
| Dynamic Forward | `ssh -D <local_port> <user>@<host>` |
| ตรวจ Server Config | `sudo sshd -t` |
| ดู SSH Log | `sudo journalctl -u ssh -f` |

### Placeholder Reference

- `<user>`: ชื่อบัญชีผู้ใช้บน Server
- `<host>`: Hostname หรือ IP Address ของ Server
- `<port>`: หมายเลข Port
- `<key>`: ชื่อไฟล์ Private Key (ไม่ใส่นามสกุล `.pub`)
- `<local_port>`: Port ที่เปิดบน Client
- `<remote_port>`: Port ที่เปิดบน Server
- `<destination_host>`: Host ที่ SSH ฝั่งปลายทางจะเชื่อมต่อไปหา
- `<destination_port>`: Port ของ Service ปลายทาง
- `<pid>`: Process ID ที่ตรวจสอบแล้ว
