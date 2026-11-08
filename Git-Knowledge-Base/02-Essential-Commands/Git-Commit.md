---
title: Git Commit
tags:
  - git
  - commands
  - commit
type: concept
status: published
---

# Git Commit

**Git Commit** คือการบันทึกภาพจำลองถาวร (Permanent Snapshot) ของ Staging Area ลงในฐานข้อมูลประวัติศาสตร์ของ Repository ทุก Commit เปรียบเสมือนจุดเช็คพอยต์บนไทม์ไลน์ที่ไม่สามารถเปลี่ยนแปลงได้ (Immutable)

---

## 1. คำสั่งนี้คืออะไรและสร้างผลกระทบอย่างไร?

เมื่อเรารัน `git commit`:
1. Git จะรวบรวมไฟล์ใน Staging Area (`.git/index`) มาสร้างเป็น **Tree Object** โครงสร้างไดเรกทอรี
2. สร้าง **Commit Object** ที่ระบุ Tree, Parent Commit (Commit ก่อนหน้า), ชื่อผู้เขียน, วันที่, และข้อความอธิบาย
3. คำนวณ SHA-1/SHA-256 Hash ของ Commit ใหม่นี้
4. ขยับ **Branch Pointer** ปัจจุบัน (และ HEAD) ให้มาชี้ที่ Commit ใหม่นี้

```mermaid
graph LR
    subgraph ก่อนสั่ง Commit
        C1[Commit C1] <-- Branch: main (HEAD)
    end
    subgraph หลังสั่ง git commit
        C1_2[Commit C1] <-- C2[Commit C2 ใหม่] <-- Branch: main (HEAD)
    end
```

---

## 2. ศิลปะของ Atomic Commit

> [!important] กฎของ Atomic Commit
> หนึ่ง Commit ควรเป็นการเปลี่ยนแปลงที่ **เล็กที่สุดที่เป็นเอกเทศ และทำงานได้สมบูรณ์ในตัวเอง (Single Logical Change)**
> - หากนำโค้ดไปรันหรือรัน Automated Test ที่จุด Commit นั้น โค้ดจะต้องคอมไพล์ผ่านและไม่มีข้อผิดพลาดร้ายแรง
> - ห้ามรวมการ Refactor โครงสร้างครั้งใหญ่ปนไปกับการแก้บั๊กเล็กๆ ใน Commit เดียวกันเด็ดขาด

---

## 3. มาตรฐานการเขียน Commit Message (Conventional Commits)

รูปแบบที่เป็นสากลและเป็นที่ยอมรับในระดับอุตสาหกรรม:
```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### ประเภทของ Commit (Type):
- `feat:` เพิ่มฟีเจอร์ใหม่สำหรับผู้ใช้งาน
- `fix:` แก้ไขข้อผิดพลาด (Bug fix)
- `docs:` แก้ไขเฉพาะเอกสารประกอบหรือ README
- `style:` ปรับแต่ง Formatting, เว้นวรรค, ลบช่องว่างที่ไม่มีผลต่อโค้ด
- `refactor:` ปรับโครงสร้างโค้ดโดยไม่เปลี่ยนพฤติกรรมการทำงานภายนอก
- `test:` เพิ่มเติมหรือแก้ไขชุดทดสอบ (Unit Tests / Integration Tests)
- `chore:` อัปเดต Build scripts, Dependencies หรือการตั้งค่าเครื่องมือ

### ตัวอย่างที่ดี:
```text
feat(auth): implement JWT refresh token rotation

- Add refreshToken endpoint in auth controller
- Store hashed refresh tokens in Redis with 7-day TTL
- Handle token revocation on logout

Closes #142
```

---

## 4. ตัวเลือกคำสั่งที่สำคัญ (Options)

```bash
# 1. บันทึกพร้อมข้อความในบรรทัดเดียว
git commit -m "feat: add user registration endpoint"

# 2. แก้ไข Commit ล่าสุด (Amend) - เช่น ลืมใส่ไฟล์ หรือสะกดข้อความผิด
git add forgotten-file.js
git commit --amend --no-edit

# 3. Add และ Commit ไฟล์ที่เคย Track แล้วในคำสั่งเดียว (ไม่รวม Untracked files)
git commit -am "fix: typo in button label"
```

> [!warning] ข้อควรระวังของ `--amend`
> `git commit --amend` จะทำการสร้าง Commit Object ใหม่ขึ้นมาแทนที่ตัวเดิม ทำให้ค่า Hash เปลี่ยนไป **ห้ามใช้คำสั่งนี้กับ Commit ที่คุณได้ push ขึ้นไปยัง Remote Server และมีคนอื่นใช้งานร่วมกันแล้ว** เพราะจะทำให้ประวัติแตกแถว

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-Add-and-Staging]] — การเตรียมของก่อน Commit
- [[Git-Object-Model]] — โครงสร้างภายในของ Commit Object
- [[Git-Reset]] — การยกเลิกหรือแก้ไขประวัติ Commit\n