---
title: Git Rebase
tags:
  - git
  - integration
  - rebase
type: concept
status: published
---

# Git Rebase

**Git Rebase** คือกระบวนการนำชุด Commit จากกิ่งหนึ่ง ไปวางต่อท้ายยอดสุดของอีกกิ่งหนึ่ง (Re-applying commits on top of another base tip) เพื่อสร้างประวัติศาสตร์การพัฒนาที่เป็นเส้นตรงสวยงาม (Linear History)

---

## 1. คำสั่งนี้ทำงานอย่างไรในระดับ Concept?

เมื่อเรารัน `git rebase main` ขณะอยู่บนกิ่ง `feature`:
1. Git จะหา Merge Base ระหว่างสองกิ่ง
2. นำ Commit บนกิ่ง `feature` ทั้งหมดมาเก็บไว้ใน Temporary Storage ชั่วคราว
3. ย้ายกิ่ง `feature` ให้ไปตั้งต้นที่ Commit ปลายสุดของ `main`
4. นำ Commit ที่เก็บไว้มาทยอยสร้างขึ้นใหม่ (Re-play) ทีละตัวบนฐานใหม่

```mermaid
graph TD
    subgraph ก่อน Rebase
        Base[Base C1] --> M1[Commit M1 บน main]
        Base --> F1[Commit F1 บน feature]
        F1 --> F2[Commit F2 บน feature]
    end
    subgraph หลัง Rebase
        M1_2[Commit M1 บน main] --> F1_NEW["Commit F1' (Hash ใหม่!)"]
        F1_NEW --> F2_NEW["Commit F2' (Hash ใหม่!)"]
    end
```

> [!important] Commit Hash เปลี่ยนไปเสมอ
> สังเกตเครื่องหมาย Prime (`F1'` และ `F2'`): แม้โค้ดจะเหมือนเดิม แต่เนื่องจาก Parent Commit และ Timestamp เปลี่ยนไป **ค่า SHA Hash ของทุก Commit ที่ถูก Rebase จะกลายเป็นเลขใหม่ทั้งหมด**

---

## 2. กฎทองข้อห้ามของการ Rebase (The Golden Rule of Rebase)

> [!warning] ห้าม Rebase กิ่งที่เป็น Shared Public History เด็ดขาด!
> **"Never rebase commits that exist outside your repository and that people may have based work on."**
> - หากคุณ Rebase Branch ส่วนตัวในเครื่องของคุณเอง: **ทำได้อย่างเต็มที่**
> - หากกิ่งนั้นถูก Push ขึ้น GitHub และมีเพื่อนร่วมทีมกำลังแตกกิ่งทำงานต่อจาก Commit เหล่านั้น: **ห้าม Rebase เด็ดขาด** เพราะจะทำให้ประวัติของเพื่อนและคุณแตกออกจากกันอย่างรุนแรง ก่อให้เกิด Endless Conflict Loop

---

## 3. Interactive Rebase (`git rebase -i`)

หนึ่งในฟีเจอร์ที่ทรงพลังที่สุดสำหรับการขัดเกลาประวัติศาสตร์ก่อนเปิด Pull Request:
```bash
# ขัดเกลา Commit 3 ตัวล่าสุด
git rebase -i HEAD~3
```
Git จะเปิด Editor ขึ้นมาให้เลือกจัดการแต่ละ Commit:
- `pick`: ใช้งาน Commit นั้นตามปกติ
- `reword`: แก้ไขเฉพาะข้อความ Commit Message
- `edit`: หยุดที่ Commit นี้เพื่อแก้ไฟล์หรือแยก Commit
- `squash` หรือ `fixup`: ยุบ Commit นี้รวมเข้ากับตัวก่อนหน้า (ทำให้ประวัติกระชับ)
- `drop`: ทิ้ง Commit นั้นไปเลย

---

## 4. การจัดการระหว่าง Rebase

- หากมี Conflict: แก้ไขไฟล์ $\rightarrow$ `git add <file>` $\rightarrow$ `git rebase --continue`
- ข้าม Commit ที่ว่างเปล่าหรือไม่จำเป็น: `git rebase --skip`
- ขอยกเลิกกลับไปสถานะเดิม: `git rebase --abort`

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-Merge]] — การผสานด้วย Merge
- [[Merge-vs-Rebase]] — วิเคราะห์เปรียบเทียบแบบเจาะลึก
- [[Merge-Conflict]] — การแก้ไข Conflict\n