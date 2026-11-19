---
title: Knowledge Base Start Here
tags: [knowledge-base, start-here, navigation]
type: hub
status: published
---

# เริ่มตรงนี้: อยากทำอะไร?

> กำลังเลือก technology หรือเรียนรู้ภาพรวม → [[Technical-Knowledge/00-Home/Home|Technical Knowledge Home]] · [[Technical-Knowledge/00-Home/Technology-Index|Technology Index]]

> หาไม่เจอ → กด `Cmd+O` แล้วพิมพ์สิ่งที่นึกออก (เช่น "public key", "conflict", "render")
> ทุกหน้า How-To ตั้งชื่อเล่นภาษาไทย/อังกฤษไว้แล้ว

## Linux / Shell

| อยากทำ | เปิด |
|---|---|
| ดูข้อมูลเครื่อง (ชื่อ, OS, Kernel, CPU, RAM, Disk) | [[Linux-Check-System-Info]] |
| เปลี่ยนชื่อเครื่อง | [[Linux-Change-Hostname]] |
| ตั้ง alias / ตัวแปรให้ถาวร (ใส่ `.bashrc` หรือ `.profile`?) | [[Linux-Add-Alias-and-Env-Var]] |
| เพิ่มโฟลเดอร์เข้า PATH | [[Linux-Add-to-PATH]] |
| ใน Terminal ได้ แต่ script / ssh / cron ไม่ได้ | [[Linux-Fix-Command-Not-Found-in-Script]] |
| เช็กว่าอยู่ใน shell อะไร แบบไหน | [[Linux-Check-Shell-Type]] |
| ค้นคำสั่ง + option ที่ใช้บ่อย | [[Linux-Command-Cheatsheet]] |

## SSH

| อยากทำ | เปิด |
|---|---|
| ติดตั้ง / เปิด SSH Server บนเครื่องใหม่ | [[SSH-Install-and-Enable-Server]] |
| สร้าง SSH Key | [[SSH-Create-Key]] |
| **ใส่ Public Key ให้ Server (เข้าแบบไม่ใช้ Password)** | [[SSH-Add-Public-Key-to-Server]] |
| ตั้งชื่อเล่น Server (`ssh lab`) | [[SSH-Setup-Config-Alias]] |
| ปิด Login ด้วย Password | [[SSH-Disable-Password-Login]] |
| ถอน Key ออก (เครื่องหาย) | [[SSH-Remove-or-Revoke-Key]] |
| ใช้ Key กับ GitHub | [[SSH-Use-Key-with-GitHub]] |
| ส่ง / ดึงไฟล์ | [[SSH-Copy-Files]] |
| ต่อ Database / เว็บบน Server ผ่าน Tunnel | [[SSH-Tunnel-to-Remote-Service]] |
| แก้ `Permission denied (publickey)` | [[SSH-Fix-Permission-Denied-Publickey]] |
| แก้ `REMOTE HOST IDENTIFICATION HAS CHANGED` | [[SSH-Fix-Host-Key-Changed]] |
| ค้นคำสั่ง | [[SSH-Command-Reference-and-Cheatsheet]] |

## Git

| อยากทำ | เปิด |
|---|---|
| เริ่มงานใหม่ → Commit → เปิด PR | [[Git-Feature-Branch-to-PR]] |
| เอาโปรเจกต์ขึ้น GitHub ครั้งแรก | [[Git-Push-New-Project-to-GitHub]] |
| ย้อน / แก้ Commit ล่าสุด | [[Git-Undo-Last-Commit]] |
| ทิ้งสิ่งที่แก้ไว้ | [[Git-Discard-Changes]] |
| พักงานแล้วสลับ Branch | [[Git-Stash-and-Switch]] |
| แก้ Conflict | [[Git-Fix-Merge-Conflict]] |
| แก้ Push ถูก Rejected | [[Git-Fix-Push-Rejected]] |
| กู้งานที่หาย | [[Git-Recover-Lost-Work]] |
| `.gitignore` ไม่ทำงาน / Secret หลุด | [[Git-Stop-Tracking-File]] |
| ค้นคำสั่ง | [[Git-Command-Cheatsheet]] |

## Code-Generated Animation

ภาพรวมทั้งชุด: [[Code-Generated Animation/README|Code-Generated Animation Home]]


| อยากทำ | เปิด |
|---|---|
| เตรียมเครื่อง + สร้างโปรเจกต์ใหม่ | [[Anim-Setup-New-Project]] |
| สั่ง Claude ทำวิดีโอจนได้ MP4 | [[Anim-Make-Video-with-Claude]] |
| ตรวจงาน + เรนเดอร์ | [[Anim-Check-and-Render]] |
| วิดีโอมีปัญหา | [[Anim-Fix-Common-Problems]] |

---

## อยากรู้ว่ามันทำงานยังไง

ทุกหน้า How-To มีหัวข้อ **"ลึกกว่านี้"** ท้ายหน้า ชี้ไปบทอธิบายที่เกี่ยวข้อง หรือเริ่มจากแผนที่ของแต่ละเรื่อง:

- Linux → [[Linux-Knowledge-Base/README|Linux: แผนที่ความรู้]]
- SSH → [[SSH-Knowledge-Base/README|SSH: แผนที่ความรู้]]
- Git → [[Git-Knowledge-Base/README|Git: แผนที่ความรู้]] · [[Git-Learning-Roadmap]]
- Animation → [[00 - Code-Generated Animation]]
