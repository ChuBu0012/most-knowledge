---
title: "Foundational Networking & Sockets"
tags:
  - networking
  - tcp
  - sockets
  - nat
  - dns
type: concept
status: published
---

# Foundational Networking & Sockets

การทำความเข้าใจ SSH และ Port Forwarding ในระดับลึก จำเป็นต้องเข้าใจกลไกเครือข่ายพื้นฐานระดับล่าง (Layer 3 และ Layer 4) ซึ่งเป็นรากฐานที่โปรโตคอล SSH อาศัยทำงานอยู่

---

## 1. TCP 3-Way Handshake & Socket Lifecycle

ก่อนที่โปรแกรมจะเริ่มแลกเปลี่ยนข้อมูลผ่านโปรโตคอล SSH ได้ ตัว Kernel ต้องเจรจาสร้างท่อเชื่อถือได้ (Reliable Stream) ตามมาตรฐาน TCP:

```mermaid
sequenceDiagram
    autonumber
    participant C as Client Socket (Ephemeral Port 52140)
    participant S as Server Socket (Listening Port 22)

    Note over S: 1. socket() -> bind(0.0.0.0:22) -> listen()<br/>สถานะ: LISTEN
    C->>S: 2. [SYN] Seq=1000
    Note over S: 3. บันทึกคำขอเข้าคิว SYN_RCVD
    S-->>C: 4. [SYN, ACK] Seq=5000, Ack=1001
    Note over C: 5. สถานะ: ESTABLISHED
    C->>S: 6. [ACK] Ack=5001
    Note over S: 7. accept() ดึงคำขอออกมาแตก Worker Socket ใหม่<br/>สถานะ: ESTABLISHED
```

### นิยามของ Socket และ 4-Tuple
การเชื่อมต่อหนึ่งท่อจะถูกระบุเอกลักษณ์ด้วย **4-Tuple (Socket Quadruple)**:
$$\text{Connection ID} = (\text{Source IP}, \text{Source Port}, \text{Destination IP}, \text{Destination Port})$$

---

## 2. NAT (Network Address Translation) & Private IP Isolation

ทำไมเครื่องภายในบ้านหรือ Virtual Machine ส่วนใหญ่จึงไม่สามารถรับ Connection ตรง ๆ จากภายนอกอินเทอร์เน็ตได้?

```mermaid
flowchart LR
    subgraph LAN_A ["Private Network A (192.168.1.0/24)"]
        ClientHost["MacBook<br/>Private IP: 192.168.1.50"]
        RouterA["Router A (NAT Gateway)<br/>Public WAN IP: 203.0.113.10"]
        ClientHost --> RouterA
    end

    subgraph WAN ["The Internet (Public Routing Space)"]
        PublicNet["เราเตอร์สาธารณะทั่วโลก<br/>(Drop แพ็กเก็ตที่จ่าหน้าด้วย Private IP ทิ้งทันที)"]
    end

    subgraph LAN_B ["Private Network B (192.168.64.0/24)"]
        RouterB["Router B (NAT Gateway)<br/>Public WAN IP: 198.51.100.25"]
        ServerHost["Ubuntu Server<br/>Private IP: 192.168.64.8"]
        RouterB --> ServerHost
    end

    RouterA --> PublicNet
    PublicNet --> RouterB
```

- **RFC 1918 Private Ranges:** บล็อก IP ได้แก่ `10.0.0.0/8`, `172.16.0.0/12`, และ `192.168.0.0/16` ถูกสงวนไว้ใช้ภายในเท่านั้น
- **NAT Table:** เราเตอร์จะทำการแปลง Source IP และ Port ของแพ็กเก็ตขาออกให้กลายเป็น Public IP ของเราเตอร์
- **ข้อจำกัด:** เมื่อมีแพ็กเก็ตจากภายนอกพยายามยิงเข้ามาหา Server โดยที่เราเตอร์ไม่มีกฎ Port Forwarding หรือไม่ได้เปิด Connection รอไว้ก่อน เราเตอร์จะ Drop แพ็กเก็ตนั้นทิ้งทันที
- **ทางแก้ด้วย SSH:** การใช้ **SSH Remote Port Forwarding (`-R`)** เป็นเทคนิคทรงพลังในการเจาะทะลุ NAT (NAT Traversal) เพราะเครื่องหลัง NAT เป็นผู้เปิดท่อขาออกไปหา Server ก่อนด้วยตนเอง

---

## 3. Network Namespace ในระบบปฏิบัติการ

ใน Linux Kernel และเทคโนโลยี Container (เช่น Docker, LXC, Podman):
- แต่ละ **Network Namespace** จะมี Network Stack เป็นของตนเอง: มี Loopback Interface แยกเด็ดขาด, ตาราง Routing แยก, Firewall แยก, และพื้นที่หมายเลข Port แยก
- นี่คือเหตุผลที่ Container หนึ่งสามารถรันโปรแกรมบนพอร์ต `80` ได้โดยไม่ชนกับโปรเซสอื่นบนเครื่อง Host

---

## 🔗 โหนดความรู้ที่เกี่ยวข้อง (Related Nodes)
- [[Localhost-Loopback-and-Port-Binding]] — ความเข้าใจเรื่อง Loopback และการ Bind Port
- [[SSH-Handshake-and-Authentication-Anatomy]] — ลำดับขั้น Handshake หลังเปิด TCP
- [[SSH-Remote-Port-Forwarding]] — การเจาะทะลุ NAT ด้วย Reverse Tunnel
- [[SSH-Dynamic-Port-Forwarding-and-SOCKS5]] — การส่งข้อมูลข้ามเน็ตเวิร์กด้วย SOCKS5
