---
title: "Asymmetric Cryptography & Key Generation"
tags:
  - cryptography
  - ssh
  - security
  - ed25519
type: concept
status: published
---

# Asymmetric Cryptography & Key Generation

ระบบยืนยันตัวตนของ SSH ขับเคลื่อนด้วยวิทยาการรหัสลับแบบกุญแจอสมมาตร (**Asymmetric Cryptography**) ซึ่งใช้คู่กุญแจที่สัมพันธ์กันทางคณิตศาสตร์: **Private Key** (กุญแจส่วนตัว) และ **Public Key** (กุญแจสาธารณะ)

---

## 1. ทำไม Private Key ต้องเกิดก่อน และทำไมถึงย้อนกลับไม่ได้?

คำถามสำคัญ: *เราสามารถสร้าง Private Key จาก Public Key ได้หรือไม่?* คำตอบคือ **"เป็นไปไม่ได้ในทางปฏิบัติ"**

```mermaid
flowchart TD
    Entropy["CSPRNG (High-Entropy Noise)<br/>ตัวกำเนิดความสุ่มระดับฮาร์ดแวร์ 256 bits"]
    PrivateKey["Private Key (Secret Scalar 'd')<br/>เก็บเป็นความลับสูงสุดบน Client"]
    OneWay["One-Way Trapdoor Function<br/>(Elliptic Curve Point Multiplication: Q = d × G)"]
    PublicKey["Public Key (Curve Point 'Q')<br/>แจกจ่ายได้ ปลอดภัยต่อการเผยแพร่"]

    Entropy -->|"สุ่มตัวเลขขนาดใหญ่"| PrivateKey
    PrivateKey -->|"คำนวณไปข้างหน้าได้เร็วมาก O(1)"| OneWay
    OneWay --> PublicKey
    PublicKey -. "เป็นไปไม่ได้ที่จะย้อนกลับ (Discrete Logarithm Problem)" .-> PrivateKey
```

> [!INFO] 📚 กลไกทางทฤษฎี: One-Way Trapdoor Function
> 1. **Private Key ($d$):** เริ่มต้นจากการดึงตัวเลขสุ่มระดับความปลอดภัยสูง (CSPRNG) ขนาด 256 บิตจากระบบปฏิบัติการ ตัวเลขนี้คือ Scalar ลับ
> 2. **Public Key ($Q$):** ถูกคำนวณผ่านฟังก์ชันทางเดียว (One-Way Function) โดยนำ $d$ ไปคูณกับจุดฐานที่ตกลงกันไว้ (Generator Point $G$) บนเส้นโค้งวงรี:
>    $$Q = d \times G$$
> 3. **ทำไมคำนวณย้อนกลับไม่ได้?** การหาค่า $d$ จาก $Q$ และ $G$ เรียกว่าปัญหา **Elliptic Curve Discrete Logarithm Problem (ECDLP)** ซึ่งในปัจจุบันไม่มีสูตรคณิตศาสตร์หรือคอมพิวเตอร์ใดในโลกที่สามารถแก้ได้ภายในเวลาช่วงอายุขัยมนุษย์

---

## 2. การทำงานของ Digital Signature: ความลับที่ไม่เคยออกจากเครื่อง

คำถามที่พบบ่อย: *ตอนต่อ SSH เครื่อง Client ส่ง Private Key ไปให้ Server ตรวจสอบหรือไม่?*

> [!IMPORTANT] 📚 Private Key ไม่เคยเดินทางผ่าน Network
> **Private Key ถูกเก็บรักษาและใช้งานเฉพาะใน Client เท่านั้น** สิ่งที่ถูกส่งผ่านท่อเครือข่ายมีเพียง **Digital Signature (ลายเซ็นดิจิทัล)**

```mermaid
sequenceDiagram
    autonumber
    participant Client as SSH Client (Mac)
    participant Server as SSH Server (Ubuntu)

    Note over Client,Server: ท่อส่งข้อมูลได้รับการเข้ารหัสเรียบร้อยแล้ว (Session Key พร้อม)
    Client->>Server: 1. Offering Public Key (เสนอ Public Key จาก id_ed25519.pub)
    Server->>Server: 2. ตรวจสอบใน ~/.ssh/authorized_keys
    alt ไม่พบ Public Key
        Server-->>Client: ปฏิเสธการเข้าถึง (Permission Denied)
    else พบ Public Key ตรงกัน
        Server-->>Client: 3. Server Accepts Key + ส่ง Challenge (Session ID + Nonce)
    end

    Note over Client: 4. นำ Challenge มาทำการ Sign ด้วย Private Key<br/>Signature = Sign(Challenge, PrivateKey)
    Client->>Server: 5. ส่งเฉพาะ "Digital Signature" กลับไป

    Note over Server: 6. ใช้ Public Key ที่มีใน authorized_keys ตรวจสอบ:<br/>Verify(Signature, Challenge, PublicKey) == VALID?
    alt ตรวจสอบผ่าน
        Server-->>Client: 7. Authenticated Using "publickey" (เปิดรับ Shell)
    else ลายเซ็นไม่ตรง
        Server-->>Client: 8. Permission Denied
    end
```

---

## 3. ความปลอดภัยของไฟล์และการปกป้องกุญแจ
- ไฟล์ Private Key เช่น `~/.ssh/id_ed25519` จะต้องถูกตั้งสิทธิ์เคร่งครัดที่ `chmod 600` (เฉพาะเจ้าของเท่านั้นที่อ่าน/เขียนได้) หากเปิดสิทธิ์กว้างเกินไป OpenSSH Client จะปฏิเสธการใช้งานทันที
- เพื่อป้องกันกรณีไฟล์ถูกขโมยจากเครื่อง เราจะทำการเข้ารหัสไฟล์บนดิสก์ซ้ำอีกชั้นด้วย [[SSH-Passphrase-and-Key-Protection]]

---

## 🔗 โหนดความรู้ที่เกี่ยวข้อง (Related Nodes)
- [[SSH-Key-Types-and-Algorithms]] — เปรียบเทียบ ED25519, RSA, ECDSA, และ DSA
- [[SSH-Passphrase-and-Key-Protection]] — การเข้ารหัส Private Key at-rest ด้วย Passphrase
- [[SSH-Agent-and-Memory-Security]] — การแคชคีย์ใน RAM เพื่อเซ็น Digital Signature โดยไม่ต้องพิมพ์รหัสซ้ำ
- [[SSH-Handshake-and-Authentication-Anatomy]] — ถอดรหัสข้อความ `Offering public key` ใน Verbose Logs
