---
title: "How-To: กู้งานที่หาย (หลัง reset --hard / ลบ branch)"
aliases:
  - กู้ commit
  - งานหาย git
  - reset hard พลาด
  - กู้ branch ที่ลบ
  - reflog
tags: [git, how-to, recovery]
type: how-to
status: published
---

# กู้งานที่หาย

> ใช้ได้กับงานที่ **เคย Commit แล้ว** เท่านั้น (ไฟล์ที่ไม่เคย add/commit กู้ด้วย Git ไม่ได้)

## 1. หาจุดก่อนพัง

```bash
git reflog -15
```

```text
a1b2c3d HEAD@{0}: reset: moving to HEAD~3      ← จุดที่พัง
7c2a1b9 HEAD@{1}: commit: add login page        ← อยากกลับมาตรงนี้
```

## 2. กู้

```bash
# ย้อน branch ปัจจุบันกลับไปจุดนั้น
git reset --hard 7c2a1b9

# หรือปลอดภัยกว่า: แตก branch ใหม่ออกมาดูก่อน
git switch -c rescue 7c2a1b9
```

กู้ Branch ที่เผลอลบ: หา hash จาก `git reflog` แล้ว `git branch <ชื่อเดิม> <hash>`

## ตรวจ

```bash
git log --oneline -5
```

## ลึกกว่านี้

[[Git-Reflog]] · [[Git-References-and-HEAD]]
