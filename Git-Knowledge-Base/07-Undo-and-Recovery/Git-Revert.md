---
title: Git Revert
tags:
  - git
  - undo
  - collaboration
  - safe
type: concept
status: published
---

# Git Revert

**`git revert`** คือคำสั่งสำหรับการยกเลิกผลลัพธ์ของ Commit ในอดีตอย่างปลอดภัย โดย **ไม่ลบหรือเขียนทับประวัติศาสตร์เดิม แต่ใช้วิธีสร้าง Commit ใหม่ที่มีผลลัพธ์หักล้างกันในเชิงคณิตศาสตร์ (Inverted Patch)**

---

## 1. ทำไม Revert ถึงปลอดภัยกว่า Reset?

```mermaid
graph LR
    subgraph Git Reset (เขียนทับประวัติ)
        R1[C1] <-- R2[C2 (มีบั๊ก)]
        R_AFTER[C1]
        note1[C2 ถูกลบหายไปจากกิ่ง - ต้องใช้ Force Push]
    end
    subgraph Git Revert (สร้าง Commit ก้าวไปข้างหน้า)
        A1[C1] <-- A2[C2 (มีบั๊ก)] <-- A3["C3 (Revert C2)"]
        note2[ประวัติศาสตร์เดิมยังอยู่ครบ 100% ปลอดภัยต่อทีม]
    end
```

- **`git reset`** ขยับ Pointer ถอยหลัง ทำให้ Commit เก่าหายไปจากสายงาน ซึ่งหาก Push ขึ้น GitHub ไปแล้วจะถูกปฏิเสธ ต้องใช้ `--force` ซึ่งเสี่ยงต่อการทำลายงานของเพื่อนร่วมทีม
- **`git revert`** เดินหน้าต่อไปเรื่อยๆ (Forward-moving undo) จึงสามารถสั่ง `git push` ขึ้นเซิร์ฟเวอร์ได้อย่างราบรื่นโดยไม่ต้องฝืนระบบ

---

## 2. ตัวอย่างการใช้งานจริง

```bash
# 1. ยกเลิก Commit ล่าสุด
git revert HEAD

# 2. ยกเลิก Commit ในอดีตที่เจาะจง
git revert 8a4b2c1

# 3. ยกเลิก Commit โดยไม่เพิ่งบันทึกข้อความทันที (นำมาคัดกรองใน Staging ก่อน)
git revert -n 8a4b2c1
```

---

## 3. การ Revert Merge Commit (Special Case)

การ Revert Commit ที่เกิดจากการ Merge มีความพิเศษ เนื่องจาก Merge Commit มี Parent ถึง 2 ตัว Git จำเป็นต้องรู้ว่าคุณต้องการยึดกิ่งสายใดเป็นหลัก โดยใช้พารามิเตอร์ `-m` (Parent number):

```bash
# ยึดกิ่งสายหลัก (Mainline) เป็น Parent หมายเลข 1
git revert -m 1 <merge-commit-hash>
```

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-Reset]] — การถอยหลังประวัติ
- [[Undo-Command-Comparison]] — เปรียบเทียบ Reset vs Revert\n