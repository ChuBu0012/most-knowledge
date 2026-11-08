---
title: "SSH Common Misconceptions & Troubleshooting"
tags:
  - ssh
  - troubleshooting
  - debugging
  - misconceptions
type: guide
status: published
---

# SSH Common Misconceptions & Troubleshooting

รวบรวมความเข้าใจผิดเชิงมโนทัศน์ (Mental Model Errors) และคู่มือการวินิจฉัยแก้ไขปัญหาที่พบบ่อยที่สุดในการใช้งาน SSH

---

## 1. สรุปความเข้าใจผิดที่พบบ่อย (Myths vs Reality)

| ความเข้าใจผิด (Myth) | ความจริงทางเทคนิค (Reality) | โหนดที่เกี่ยวข้อง |
| :--- | :--- | :--- |
| **"Private Key จะถูกส่งไปให้ Server ตรวจสอบ"** | **ผิด:** Private Key ไม่เคยหลุดออกจาก Client สิ่งที่ส่งไปคือ Digital Signature ที่คำนวณจาก Challenge Data เท่านั้น | [[Asymmetric-Cryptography-and-Key-Generation]] |
| **"Passphrase ทำให้เน็ตช้าลง"** | **ผิด:** Passphrase ใช้ถอดรหัสกุญแจในเครื่อง Local ก่อนโหลดขึ้น RAM เท่านั้น ไม่มีการส่งผ่านเครือข่ายและไม่กระทบความเร็วท่อ SSH | [[SSH-Passphrase-and-Key-Protection]] |
| **"`localhost` คือเครื่องไหนก็ได้ที่อยู่ในท่อ SSH"** | **ผิด:** `localhost` เป็นเพียงชื่อเรียกแทน Loopback Interface (`127.0.0.1`) ของ **เครื่องที่กำลังประมวลผลคำสั่งนั้น ๆ** เท่านั้น | [[Localhost-Loopback-and-Port-Binding]] |
| **"`ssh -D` ทำให้ทุกโปรแกรมในเครื่องเข้าเน็ตผ่าน Server ทันที"** | **ผิด:** `ssh -D` เพียงแค่เปิด SOCKS5 Port รอรับการเชื่อมต่อ แต่ละแอปพลิเคชันต้องกำหนดค่า Proxy ชี้มาที่พอร์ตนี้เอง | [[SSH-Dynamic-Port-Forwarding-and-SOCKS5]] |
| **"`ssh-add -D` จะลบไฟล์คีย์ในเครื่องทิ้ง"** | **ผิด:** เป็นเพียงการล้างคีย์ที่แคชไว้ใน RAM ของ `ssh-agent` เท่านั้น ไฟล์จริงบนดิสก์ (`~/.ssh/id_...`) ยังคงอยู่ครบถ้วน | [[SSH-Agent-and-Memory-Security]] |

---

## 2. คู่มือวิเคราะห์และแก้ไขปัญหา (Troubleshooting Guide)

### ปัญหาที่ 1: `Permission denied (publickey)`
- **สาเหตุที่เป็นไปได้:**
  1. ไม่ได้ใส่ Public Key ลงใน `~/.ssh/authorized_keys` บนเซิร์ฟเวอร์
  2. สิทธิ์ของโฟลเดอร์/ไฟล์บนเซิร์ฟเวอร์เปิดกว้างเกินไป (OpenSSH จะปฏิเสธเพื่อความปลอดภัย)
- **วิธีแก้:**
  - รันบนเซิร์ฟเวอร์:
    ```bash
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized_keys
    ```
  - ตรวจสอบว่าไฟล์ Private Key บน Client มีสิทธิ์ `chmod 600 ~/.ssh/id_ed25519`

---

### ปัญหาที่ 2: `Received disconnect: Too many authentication failures`
- **สาเหตุ:** `ssh-agent` มีกุญแจโหลดอยู่หลายดอก และพยายามส่งเสนอคีย์ทั้งหมดไปให้เซิร์ฟเวอร์จนเกินขีดจำกัด `MaxAuthTries`
- **วิธีแก้:** กำหนด `IdentitiesOnly yes` ใน `~/.ssh/config` เพื่อบังคับให้ส่งเฉพาะคีย์ที่ตรงกับเซิร์ฟเวอร์นั้นเท่านั้น ([[SSH-Client-Configuration-and-Aliases]])

---

### ปัญหาที่ 3: `WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!`
- **สาเหตุ:** กุญแจประจำเครื่องแม่ข่าย (Host Key) ไม่ตรงกับค่าที่บันทึกไว้ใน `~/.ssh/known_hosts` (อาจเกิดจากการ Reinstall OS เซิร์ฟเวอร์ใหม่ หรือเกิดการโจมตี Man-In-The-Middle)
- **วิธีแก้:**
  - หากแน่ใจว่าเกิดจากการลง OS เซิร์ฟเวอร์ใหม่ ให้ลบ Fingerprint เดิมออกด้วยคำสั่ง:
    ```bash
    ssh-keygen -R 192.168.64.8
    ```

---

## 🔗 โหนดความรู้ที่เกี่ยวข้อง (Related Nodes)
- [[SSH-Handshake-and-Authentication-Anatomy]] — วิเคราะห์ขั้นตอนด้วย `ssh -v`
- [[SSH-Client-Configuration-and-Aliases]] — การตั้งค่าคอนฟิกเพื่อป้องกันปัญหาคีย์
- [[Localhost-Loopback-and-Port-Binding]] — การวิเคราะห์สาเหตุ `Connection refused`
