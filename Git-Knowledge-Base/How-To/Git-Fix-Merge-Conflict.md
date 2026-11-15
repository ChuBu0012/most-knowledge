---
title: "How-To: แก้ Merge Conflict"
aliases:
  - conflict
  - merge conflict
  - แก้ conflict
  - "<<<<<<< HEAD"
tags: [git, how-to, conflict]
type: how-to
status: published
---

# แก้ Merge Conflict

## 1. ดูว่าไฟล์ไหนชน

```bash
git status        # ไฟล์ที่ชนจะอยู่ใต้ "both modified"
```

## 2. เปิดไฟล์ แล้วเลือกเนื้อหาที่ถูก

```text
<<<<<<< HEAD
ของเรา
=======
ของอีกฝั่ง
>>>>>>> main
```

ลบบรรทัด `<<<<<<<`, `=======`, `>>>>>>>` ออกให้หมด เหลือแค่เนื้อหาที่ต้องการ
(VS Code มีปุ่ม *Accept Current / Incoming / Both* ให้กด)

เอาทั้งไฟล์จากฝั่งเดียว:

```bash
git checkout --ours <file>      # เอาของเรา
git checkout --theirs <file>    # เอาของอีกฝั่ง
```

## 3. ทำต่อ

```bash
git add <file>
git status                   # จะบอกว่าต้องใช้คำสั่งไหนต่อ
git merge --continue         # ถ้ากำลัง merge
git rebase --continue        # ถ้ากำลัง rebase
```

ยอมแพ้ กลับไปก่อนเริ่ม: `git merge --abort` / `git rebase --abort`

## ตรวจ

```bash
grep -rn "<<<<<<<" .     # ต้องไม่เจออะไร
```

## ลึกกว่านี้

[[Merge-Conflict]] · [[Conflict-Resolution-Workflow]]
