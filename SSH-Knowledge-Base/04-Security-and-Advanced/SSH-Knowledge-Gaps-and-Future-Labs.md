---
title: "SSH Knowledge Gaps & Future Labs"
tags:
  - ssh
  - roadmap
  - future-study
  - enterprise
type: roadmap
status: draft
---

# SSH Knowledge Gaps & Future Labs

บันทึกขอบเขตเนื้อหาและหัวข้อการทดลองเชิงลึกระดับ Enterprise ที่ **ยังไม่ได้ทำการทดลองจริงใน Session นี้ (Unverified / Knowledge Gap)** สำหรับต่อยอดและศึกษาเพิ่มเติมในอนาคต

---

## 1. รายการหัวข้อที่ยังไม่ได้ทดลองในแล็บจริง

> [!WARNING] ⏳ ยังไม่ได้ทดลองในแล็บ (Unverified / Knowledge Gap)
> หัวข้อดังต่อไปนี้มีข้อมูลเชิงทฤษฎีรองรับ แต่ยังไม่ได้ถูกสร้างและยืนยันผลลัพธ์ผ่านสภาพแวดล้อม Mac/Ubuntu ในปัจจุบัน:

### 1. Hardware Security Keys (`ed25519-sk` & `ecdsa-sk`)
- **เป้าหมาย:** ทดลองสร้างและใช้งาน FIDO2 Hardware Token (เช่น YubiKey 5 Series) ร่วมกับ OpenSSH 8.2+
- **ประเด็นที่ต้องตรวจสอบ:** พฤติกรรมของ `ssh-agent` เมื่อเสียบและถอด USB Key, การตั้งค่า PIN, และการทำงานของ Resident Keys (`-O resident`)

### 2. SSH Certificates Authority (CA) vs `authorized_keys`
- **เป้าหมาย:** สถาปัตยกรรมการยืนยันตัวตนระดับองค์กรที่เลิกแจกจ่ายไฟล์ `authorized_keys`
- **ประเด็นที่ต้องศึกษา:**
  - การสร้าง SSH CA Keypair
  - การลงนาม Certificate ให้กับ User Keys (`ssh-keygen -s ca_key ...`)
  - การกำหนดสิทธิ์แบบ Role/Principals และกำหนดวันหมดอายุอัตโนมัติ (Short-lived Certificates)
  - การยกเลิกสิทธิ์ฉุกเฉินผ่าน Key Revocation Lists (KRL)

### 3. การจำลองการโจมตี SSH Agent Socket Hijacking
- **เป้าหมาย:** พิสูจน์ช่องโหว่ความปลอดภัยของการใช้ `ssh -A` บนเครื่อง Jump Host รวม
- **การทดลองที่วางแผน:** สร้าง Docker Container จำลองเป็น Jump Host แล้วใช้สิทธิ์ root แอบเชื่อมต่อ Socket ใน `/tmp/ssh-XXXXXX/agent.sock` เพื่อเจาะเข้า Container ปลายทางโดยที่ Mac ไม่รู้ตัว เพื่อเทียบกับความปลอดภัยของ `ProxyJump`

### 4. SSH Host Certificates เพื่อกำจัดคำเตือน `known_hosts`
- **เป้าหมาย:** การใช้ CA รับรอง Host Key ของเครื่องเซิร์ฟเวอร์
- **ประโยชน์:** ทำให้ Client ในองค์กรไม่ต้องกดยืนยัน `Are you sure you want to continue connecting (yes/no)?` อีกต่อไปเมื่อมีการเปิดเซิร์ฟเวอร์เครื่องใหม่

---

## 🔗 โหนดความรู้ที่เกี่ยวข้อง (Related Nodes)
- [[SSH-Key-Types-and-Algorithms]] — ภาพรวมของ Hardware Keys
- [[SSH-Agent-Forwarding-and-Security]] — ภัยคุกคามของ Agent Forwarding
- [[SSH-Command-Reference-and-Cheatsheet]] — รวบรวมคำสั่งพื้นฐานทั้งหมด
