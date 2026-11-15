---
title: "How-To: แก้ Permission denied (publickey)"
aliases:
  - permission denied publickey
  - ssh เข้าไม่ได้
  - ssh key ไม่ทำงาน
  - ssh ยังถาม password
tags:
  - ssh
  - how-to
  - troubleshooting
type: how-to
status: published
---

# แก้ `Permission denied (publickey)`

> **ใช้เมื่อ:** ใส่ Key แล้วแต่ยังเข้าไม่ได้ หรือยังโดนถาม Password
> ไล่ตามลำดับ เจอข้อไหนผิดแก้ข้อนั้น แล้วลองใหม่

## ขั้น 1: ดูว่า Client ส่ง Key อะไรไป

💻 **เครื่องเรา**

```bash
ssh -v chubu@192.168.64.8 2>&1 | grep -Ei "offering|accepts|identity file|denied"
```

| เห็นบรรทัด | แปลว่า | แก้ |
|---|---|---|
| `Offering public key: ...id_ed25519` แล้วตามด้วย `denied` | ส่ง Key ไปแล้ว แต่ Server ไม่รู้จัก | ไปขั้น 2 |
| ไม่มี `Offering` เลย / Offering key อื่น | ส่ง Key ผิดดอก | ระบุ `-i ~/.ssh/id_ed25519` หรือแก้ `IdentityFile` ใน [[SSH-Setup-Config-Alias]] |
| `Server accepts key` | Key ผ่านแล้ว | ปัญหาอยู่ที่ Passphrase / Agent |

## ขั้น 2: เช็กว่า Key อยู่ใน Server จริงและเป็น User ที่ถูก

🖥️ **บน Server** (Login ด้วย Password หรือ Console)

```bash
whoami                                  # ต้องเป็น user เดียวกับที่ ssh เข้ามา
cat ~/.ssh/authorized_keys              # ต้องเห็น key บรรทัดเดียวที่ตรงกับเครื่องเรา
```

💻 เทียบกับเครื่องเรา: `cat ~/.ssh/id_ed25519.pub` — ส่วน `AAAA...` ต้องตรงกันทุกตัว
ไม่เจอ → ทำ [[SSH-Add-Public-Key-to-Server]] ใหม่

## ขั้น 3: Permission และ Owner (สาเหตุอันดับ 1)

🖥️ **บน Server**

```bash
ls -ld ~ ~/.ssh ~/.ssh/authorized_keys
```

ต้องได้ประมาณนี้ (Owner ต้องเป็น User นั้น ไม่ใช่ `root`):

```text
drwxr-xr-x  chubu chubu  /home/chubu          ← home ห้ามให้คนอื่นเขียนได้ (ไม่มี w ที่กลุ่ม/อื่น)
drwx------  chubu chubu  /home/chubu/.ssh     ← 700
-rw-------  chubu chubu  .../authorized_keys  ← 600
```

แก้:

```bash
chmod go-w ~
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
sudo chown -R "$USER":"$USER" ~/.ssh
```

## ขั้น 4: ถาม Server ตรงๆ ว่าทำไมปฏิเสธ

🖥️ **บน Server** แล้วลอง ssh จากเครื่องเราอีกครั้งระหว่างที่คำสั่งนี้รันอยู่

```bash
# Ubuntu / Debian
sudo journalctl -u ssh -f
# RHEL / Fedora / บางระบบ
sudo journalctl -u sshd -f
# ระบบเก่า
sudo tail -f /var/log/auth.log
```

ข้อความที่เจอบ่อย:

| Log | แก้ |
|---|---|
| `Authentication refused: bad ownership or modes` | กลับไปขั้น 3 |
| `User chubu not allowed because not listed in AllowUsers` | เพิ่มชื่อใน `AllowUsers` ของ `/etc/ssh/sshd_config` |
| ไม่มี log เลย | ต่อผิดเครื่อง/ผิด Port หรือ Firewall กั้น |

## ขั้น 5: Server ปิด Public Key Auth ไว้หรือเปล่า

```bash
sudo sshd -T | grep -Ei "pubkeyauthentication|authorizedkeysfile"
```

ต้องได้ `pubkeyauthentication yes` และ `authorizedkeysfile .ssh/authorized_keys ...`

## ลึกกว่านี้

- [[SSH-Handshake-and-Authentication-Anatomy]] — อ่าน verbose log เป็น
- [[SSH-Common-Misconceptions-and-Troubleshooting]] — Error อื่นๆ
