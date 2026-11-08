---
title: "SSH Client Configuration & Host Aliases"
tags:
  - ssh
  - configuration
  - productivity
  - security
type: concept
status: published
---

# SSH Client Configuration & Host Aliases

ไฟล์คอนฟิกูเรชันหลักของ Client อยู่ที่ **`~/.ssh/config`** (และของระบบที่ `/etc/ssh/ssh_config`) ช่วยลดความซับซ้อนในการพิมพ์คำสั่ง ลดข้อผิดพลาด และเพิ่มความปลอดภัยอย่างมาก

---

## 1. ตัวอย่างคอนฟิกูเรชันจากแล็บจริง

```sshconfig
# คอนฟิกูเรชันส่วนกลาง (มีผลกับทุกเซิร์ฟเวอร์)
Host *
    AddKeysToAgent yes
    UseKeychain yes
    ServerAliveInterval 60
    ServerAliveCountMax 3

# คอนฟิกูเรชันเฉพาะสำหรับ Ubuntu Server ในแล็บ
Host chubu
    HostName 192.168.64.8
    User chubu
    Port 22
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
```

### เปรียบเทียบการพิมพ์คำสั่ง

- **แบบเดิม (ไม่มี Config):**
  ```bash
  ssh -i ~/.ssh/id_ed25519 -o IdentitiesOnly=yes -p 22 chubu@192.168.64.8
  ```
- **แบบใช้ Host Alias:**
  ```bash
  ssh chubu
  ```

---

## 2. เจาะลึกความสำคัญของ Directives แต่ละตัว

| Directive | ค่าที่ตั้ง | เหตุผลและความสำคัญ |
| :--- | :--- | :--- |
| **`Host`** | `chubu` | ชื่อเล่น (Alias) ที่เราต้องการใช้เรียกใน Terminal |
| **`HostName`** | `192.168.64.8` | IP Address จริง หรือ FQDN ของเครื่องแม่ข่ายปลายทาง |
| **`User`** | `chubu` | บัญชีผู้ใช้บนเครื่องแม่ข่าย (ไม่ต้องพิมพ์ `chubu@` อีกต่อไป) |
| **`IdentityFile`** | `~/.ssh/id_ed25519` | ชี้ไปยังไฟล์ Private Key ที่เจาะจงสำหรับเซิร์ฟเวอร์นี้ |
| **`IdentitiesOnly`** | **`yes`** | **สำคัญมาก:** บังคับให้ SSH Client ส่งเฉพาะคีย์ที่ระบุในไฟล์นี้เท่านั้น ห้ามหยิบคีย์อื่นใน `ssh-agent` ไปลองสุ่มส่งเด็ดขาด |
| **`ServerAliveInterval`** | `60` | ส่ง Null Packet ทุก 60 วินาที ป้องกันไฟร์วอลล์หรือเราเตอร์ตัดการเชื่อมต่อเพราะ Idle |
| **`UseKeychain`** | `yes` | (macOS Only) เก็บและดึง Passphrase จาก Apple Keychain โดยอัตโนมัติ |

> [!CAUTION] 📚 ปัญหา "Too many authentication failures" จากการไม่ใส่ IdentitiesOnly
> หากเครื่องของคุณมีกุญแจหลายชุด (เช่น คีย์ GitHub, คีย์บริษัท, คีย์เซิร์ฟเวอร์เก่า) ที่โหลดอยู่ใน `ssh-agent` ตัว OpenSSH Client จะพยายามไล่เสนอคีย์ทั้งหมดให้เซิร์ฟเวอร์ลองตรวจ
> - เซิร์ฟเวอร์ส่วนใหญ่จำกัดจำนวนครั้งการลองผิด (MaxAuthTries) ไว้ที่ 3 หรือ 6 ครั้ง
> - หากกุญแจที่ถูกต้องอยู่อันดับท้าย ๆ เซิร์ฟเวอร์จะตัดสายทิ้งทันทีพร้อมข้อความ **`Received disconnect: Too many authentication failures`**
> - **การตั้ง `IdentitiesOnly yes` คือเกราะป้องกันปัญหานี้ที่ดีที่สุด**

---

## 🔗 โหนดความรู้ที่เกี่ยวข้อง (Related Nodes)
- [[SSH-Architecture-and-Fundamentals]] — พื้นฐานการทำงานของ Client และ Daemon
- [[SSH-Passphrase-and-Key-Protection]] — การจัดการไฟล์กุญแจที่ระบุใน IdentityFile
- [[SSH-Agent-and-Memory-Security]] — การทำงานร่วมกับ `AddKeysToAgent` และ `UseKeychain`
- [[SSH-Common-Misconceptions-and-Troubleshooting]] — แนวทางแก้ปัญหา Permission Denied
