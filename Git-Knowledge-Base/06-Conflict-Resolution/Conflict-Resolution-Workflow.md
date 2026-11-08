---
title: Conflict Resolution Workflow
tags:
  - git
  - conflicts
  - workflow
  - team
type: tutorial
status: published
---

# Conflict Resolution Workflow

แนวทางปฏิบัติและเวิร์กโฟลว์เชิงระบบในการรับมือกับ Merge Conflicts ทั้งในกระบวนการ `git merge` และ `git rebase` อย่างเป็นมืออาชีพ

---

## 1. แผนภาพเวิร์กโฟลว์การแก้ปัญหา

```mermaid
flowchart TD
    Trigger[สั่ง git merge หรือ git rebase แล้วเกิด Conflict] --> Status[1. ตรวจสอบสถานะด้วย git status]
    Status --> Inspect[2. เปิดไฟล์ที่มีข้อขัดแย้งและวิเคราะห์ Intent ของทั้งสองฝั่ง]
    Inspect --> Edit[3. แก้ไขโค้ดและลบ Conflict Markers ให้หมด]
    Edit --> Test[4. รันชุดทดสอบ Build & Test]
    Test -- ผ่านฉลุย --> Stage[5. สั่ง git add เพื่อยืนยัน]
    Test -- พัง/มีปัญหา --> Edit
    Stage --> Type{คำสั่งต้นทางคืออะไร?}
    Type -- เป็น git merge --> FinishMerge[git merge --continue หรือ git commit]
    Type -- เป็น git rebase --> FinishRebase[git rebase --continue\n(ทำซ้ำถ้า Commit ถัดไปชนอีก)]
    FinishMerge --> Done([สำเร็จ!])
    FinishRebase --> Done
```

---

## 2. ความต่างในการรับมือระหว่าง Merge vs Rebase

### 2.1 เมื่อเกิด Conflict ตอน `git merge`
- **ลักษณะ:** เกิดขึ้นเพียง **ครั้งเดียว** ณ จังหวะรวมร่าง
- **การยกเลิก:** หากแก้ไม่ไหวหรือยังไม่พร้อม ให้สั่ง:
  ```bash
  git merge --abort
  ```
  เพื่อยกเลิกทุกอย่างกลับคืนสภาพเดิม 100%
- **การเดินหน้าต่อ:** เมื่อแก้และ `git add` ครบแล้ว สั่ง:
  ```bash
  git merge --continue
  ```

### 2.2 เมื่อเกิด Conflict ตอน `git rebase`
- **ลักษณะ:** อาจเกิด **หลายรอบ** ตามจำนวน Commit ที่นำมารีเพลย์ (Replay) ทับฐานใหม่
- **การยกเลิก:**
  ```bash
  git rebase --abort
  ```
- **การเดินหน้าต่อ:**
  ```bash
  git add <resolved-file>
  git rebase --continue
  ```
  *(ห้ามสั่ง `git commit` ระหว่าง Rebase เด็ดขาด เพราะจะทำให้ขั้นตอนสะดุด)*

---

## 3. กฎทอง 4 ข้อในการป้องกัน Conflict ล่วงหน้า (Conflict Prevention)

1. **Pull จาก Main บ่อยๆ:** อย่าสะสม Feature Branch ไว้นานเกินไป (หลีกเลี่ยง Long-lived branches) ให้ Rebase กับ `main` ทุกๆ 1-2 วัน
2. **ออกแบบ Modular Architecture:** แบ่งขอบเขตไฟล์ให้ชัดเจน หลีกเลี่ยง "God Files" หรือไฟล์รวมทุกอย่างที่ทุกคนต้องมาแก้ที่เดียวกัน
3. **ตกลง Code Formatter เดียวกันทั้งทีม:** ใช้ Prettier / ESLint อัตโนมัติ เพราะการจัดย่อหน้าคนละแบบ (Spaces vs Tabs) จะก่อให้เกิด Conflict ทุกบรรทัดโดยไร้ประโยชน์
4. **ประสานงานเมื่อเปลี่ยน Shared Contracts:** หากจำเป็นต้องแก้ Database Schema, Route กลาง หรือ Global Interface ให้แจ้งสมาชิกในทีมล่วงหน้าทันที (ดูเพิ่มเติมใน [[Integration-and-Coordination]])

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Merge-Conflict]] — เจาะลึก Conflict Markers
- [[Integration-and-Coordination]] — การประสานงานลดความเสี่ยง
- [[Parallel-Development-Concept]] — การพัฒนาคู่ขนาน\n