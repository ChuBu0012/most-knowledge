---
title: "SSH Command Reference & Cheatsheet"
tags:
  - ssh
  - cheatsheet
  - reference
  - commands
type: reference
status: published
---

# SSH Command Reference & Cheatsheet

เอกสารสรุปคำสั่งและ Argument ที่ใช้บ่อยในงานประจำวัน จัดหมวดหมู่ตามวัตถุประสงค์พร้อมคำอธิบายแบบกระชับ

---

## 1. คำสั่งสร้างและบริหารจัดการกุญแจ (`ssh-keygen`, `ssh-copy-id`)

```bash
# สร้าง Key Pair แบบ ED25519 (แนะนำสูงสุด)
ssh-keygen -t ed25519 -C "chubu@macbook-air"

# สร้าง Key Pair แบบ RSA 4096 bits (สำหรับระบบเก่าที่ยังไม่รองรับ Ed25519)
ssh-keygen -t rsa -b 4096 -C "legacy-systems"

# เปลี่ยน Passphrase บน Private Key เดิม (โดยไม่ต้องสร้างคีย์ใหม่)
ssh-keygen -p -f ~/.ssh/id_ed25519

# แสดง Fingerprint และความยาวของไฟล์ Public Key
ssh-keygen -l -f ~/.ssh/id_ed25519.pub

# ดึง Public Key ออกมาจากไฟล์ Private Key (เมื่อทำไฟล์ .pub หาย)
ssh-keygen -y -f ~/.ssh/id_ed25519 > ~/.ssh/id_ed25519.pub

# คัดลอก Public Key ไปติดตั้งบนเซิร์ฟเวอร์ปลายทางอัตโนมัติ
ssh-copy-id -i ~/.ssh/id_ed25519.pub chubu@192.168.64.8
```

---

## 2. คำสั่งบริหารจัดการหน่วยความจำ (`ssh-add`, `ssh-agent`)

```bash
# โหลดคีย์เข้าสู่ Agent (ป้อน Passphrase เพียงครั้งเดียว)
ssh-add ~/.ssh/id_ed25519

# แสดงรายการ Fingerprints ของกุญแจทั้งหมดใน RAM
ssh-add -l

# พิมพ์เนื้อหา Public Key ทั้งหมดที่แคชไว้ใน RAM ออกมาดู
ssh-add -L

# ล้างกุญแจทั้งหมดออกจาก RAM ทันที (ไม่ลบไฟล์จริงบน Disk)
ssh-add -D

# ลบเฉพาะกุญแจดอกที่ระบุออกจาก RAM
ssh-add -d ~/.ssh/id_ed25519

# โหลดกุญแจพร้อมตั้งเวลาจำกัด (เช่น หมดอายุหลัง 2 ชั่วโมง)
ssh-add -t 2h ~/.ssh/id_ed25519
```

---

## 3. คำสั่งเชื่อมต่อและวิเคราะห์ข้อผิดพลาด (`ssh`)

```bash
# เชื่อมต่อผ่าน Host Alias ที่ตั้งไว้ใน ~/.ssh/config
ssh chubu

# เชื่อมต่อแบบระบุ IP, Port, และ Private Key ชัดเจน
ssh -p 22 -i ~/.ssh/id_ed25519 -o IdentitiesOnly=yes chubu@192.168.64.8

# โหมด Verbose ดูขั้นตอน Handshake และสาเหตุที่ล็อกอินไม่ผ่าน
ssh -v chubu      # ระดับปกติ
ssh -vvv chubu    # ระดับเจาะลึกสูงสุด (ดูระดับแพ็กเก็ต)

# รันคำสั่งทางไกลโดยไม่ต้องเปิด Interactive Shell
ssh chubu "df -h && uptime"

# เชื่อมต่อไปยัง Target Server ผ่าน Jump Host (แบบปลอดภัย)
ssh -J jumpuser@jump.corp.com chubu@10.0.1.50
```

---

## 4. คำสั่ง Port Forwarding และ Tunneling

```bash
# Local Port Forwarding: เปิดพอร์ต 8080 บน Mac พาไปเข้า PostgreSQL 5432 บนเครือข่ายของเซิร์ฟเวอร์
ssh -N -f -L 8080:10.0.0.5:5432 chubu

# Remote Port Forwarding: เปิดพอร์ต 9000 บน Ubuntu ส่งข้อมูลย้อนกลับมาหา Web Server 8000 บน Mac
ssh -N -f -R 9000:localhost:8000 chubu

# Dynamic Port Forwarding: เปิด SOCKS5 Proxy บนพอร์ต 1080 ของ Mac
ssh -N -f -D 1080 chubu

# ทดสอบยิง Request ผ่าน SOCKS5 Proxy โดยให้เซิร์ฟเวอร์เป็นผู้แปลง DNS
curl --socks5-hostname 127.0.0.1:1080 http://ifconfig.me
```

### สรุปตัวเลือกสำคัญ (Flags Cheatsheet)
- **`-N`:** ห้ามรันคำสั่งใด ๆ ปลายทาง (เหมาะสำหรับทำ Tunnel ล้วน ๆ)
- **`-f`:** สลับโปรเซสไปทำงานเป็น Background Daemon หลังผ่านการยืนยันตัวตน
- **`-L`:** Local Forwarding (เปิดพอร์ตฝั่งเรา ส่งไปฝั่งเขา)
- **`-R`:** Remote Forwarding (เปิดพอร์ตฝั่งเขา ส่งกลับมาฝั่งเรา)
- **`-D`:** Dynamic Forwarding (เปิด SOCKS Proxy รับส่งข้อมูลทุกเป้าหมาย)

---

## 5. ส่งและดึงไฟล์ (`scp`, `sftp`)

```bash
# ส่งไฟล์ Client → Server
scp ./local-file <alias>:/tmp/

# ดึงไฟล์ Server → Client
scp <alias>:/tmp/remote-file ./

# ส่ง/ดึงโฟลเดอร์
scp -r ./local-folder <alias>:/tmp/
scp -r <alias>:/tmp/remote-folder ./

# ระบุ SSH Port (ตัวใหญ่ -P)
scp -P 2222 ./file <alias>:/tmp/

# เปิด Session เพื่อ browse และจัดการไฟล์
sftp <alias>
```

ใน SFTP:

```text
sftp> pwd       # ดู Path บน Server
sftp> lpwd      # ดู Path บน Client
sftp> ls        # ดูไฟล์บน Server
sftp> lls       # ดูไฟล์บน Client
sftp> get file  # ดึงไฟล์
sftp> put file  # ส่งไฟล์
sftp> get -r dir
sftp> put -r dir
sftp> exit
```

ดูคู่มือแบบเต็มที่ [[SSH-SCP-File-Transfer]] และ [[SSH-SFTP-File-Transfer]]

---

## 🔗 โหนดความรู้ที่เกี่ยวข้อง (Related Nodes)
- [[SSH-Client-Configuration-and-Aliases]] — การย้ายคำสั่งยาว ๆ ไปไว้ใน `~/.ssh/config`
- [[SSH-Local-Port-Forwarding]] — กลไกเชิงลึกของ `-L`
- [[SSH-Remote-Port-Forwarding]] — กลไกเชิงลึกของ `-R`
- [[SSH-Dynamic-Port-Forwarding-and-SOCKS5]] — กลไกเชิงลึกของ `-D`
- [[SSH-SCP-File-Transfer]] — คัดลอกไฟล์แบบคำสั่งเดียว
- [[SSH-SFTP-File-Transfer]] — จัดการไฟล์แบบ Interactive
