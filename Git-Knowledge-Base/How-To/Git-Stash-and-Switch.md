---
title: "How-To: พักงานไว้ก่อนแล้วสลับ Branch"
aliases:
  - stash
  - สลับ branch ไม่ได้
  - would be overwritten by checkout
  - เก็บงานชั่วคราว
tags: [git, how-to, stash]
type: how-to
status: published
---

# พักงานไว้ก่อนแล้วสลับ Branch

> **ใช้เมื่อ:** งานยังไม่เสร็จ (ไม่อยาก commit) แต่ต้องไปแก้ด่วนที่ branch อื่น
> หรือเจอ `error: Your local changes ... would be overwritten by checkout`

```bash
git stash push -u -m "wip: login page"    # -u = รวมไฟล์ใหม่ที่ยังไม่ track
git switch hotfix
# ... ทำงานด่วน ...
git switch feature/login-page
git stash pop                              # เอางานกลับมา
```

ดูว่ามีอะไรพักไว้บ้าง: `git stash list`

`stash pop` แล้ว conflict → แก้ตาม [[Git-Fix-Merge-Conflict]] (stash ยังไม่ถูกลบ จนกว่าจะ `git stash drop`)

ทางเลือก: ทำงานสอง branch พร้อมกันโดยไม่ต้อง stash → [[Worktree-Commands]]

## ลึกกว่านี้

[[Daily-Git-Commands]]
