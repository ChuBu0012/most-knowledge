---
title: "How-To: แก้ git push ถูก rejected"
aliases:
  - push rejected
  - failed to push some refs
  - fetch first
  - non-fast-forward
tags: [git, how-to, remote]
type: how-to
status: published
---

# แก้ `git push` ถูก Rejected

```text
! [rejected]  main -> main (fetch first)
```

แปลว่า Remote มี Commit ใหม่ที่เครื่องเรายังไม่มี

## แก้

```bash
git pull --rebase
# ถ้ามี conflict → แก้ไฟล์ → git add <file> → git rebase --continue
git push
```

ไม่แน่ใจ ยกเลิกกลางทาง: `git rebase --abort` (กลับสู่สภาพก่อน pull)

> [!danger] อย่าแก้ด้วย `git push --force` บน branch ที่คนอื่นใช้ด้วย
> จะเขียนทับงานเพื่อน ถ้าจำเป็นจริงบน branch ตัวเอง ใช้ `git push --force-with-lease`

## ลึกกว่านี้

[[Fetch-Pull-Push]] · [[Git-Fix-Merge-Conflict]] · [[Merge-vs-Rebase]]
