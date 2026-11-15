---
title: "How-To: ย้อน / แก้ Commit ล่าสุด"
aliases:
  - undo commit
  - ย้อน commit
  - แก้ commit message
  - ลืม add ไฟล์
  - commit ผิด
tags: [git, how-to, undo]
type: how-to
status: published
---

# ย้อน / แก้ Commit ล่าสุด

เลือกตามสถานการณ์:

| อยากทำอะไร | คำสั่ง |
|---|---|
| แก้ข้อความ Commit | `git commit --amend -m "ข้อความใหม่"` |
| ลืมใส่ไฟล์ | `git add <file>` แล้ว `git commit --amend --no-edit` |
| ยกเลิก Commit แต่เก็บงานไว้ | `git reset --soft HEAD~1` |
| ยกเลิก Commit และทิ้งงานทิ้งเลย | `git reset --hard HEAD~1` ⚠️ |
| Commit ถูก Push ไปแล้ว อยากย้อน | `git revert HEAD` แล้ว `git push` |

> [!warning] ถ้า Push ไปแล้ว ห้ามใช้ `amend` / `reset`
> จะทำให้ประวัติไม่ตรงกับ Remote ใช้ `git revert` แทน (สร้าง Commit ใหม่ที่ย้อนของเดิม)

## ตรวจ

```bash
git log --oneline -3
git status
```

เผลอ `reset --hard` ไปแล้ว → [[Git-Recover-Lost-Work]]

## ลึกกว่านี้

[[Undo-Command-Comparison]] · [[Git-Reset]] · [[Git-Revert]]
