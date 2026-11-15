---
title: "How-To: ทิ้งสิ่งที่แก้ไว้ (ยังไม่ commit)"
aliases:
  - discard changes
  - ทิ้งการแก้ไข
  - unstage
  - git restore
  - ลบไฟล์ที่ไม่ได้ track
tags: [git, how-to, undo]
type: how-to
status: published
---

# ทิ้งสิ่งที่แก้ไว้ (ยังไม่ Commit)

| อยากทำอะไร | คำสั่ง |
|---|---|
| ทิ้งการแก้ไขในไฟล์เดียว | `git restore <file>` |
| ทิ้งการแก้ไขทุกไฟล์ | `git restore .` |
| `git add` ไปแล้ว อยากเอาออก (งานยังอยู่) | `git restore --staged <file>` |
| ลบไฟล์ใหม่ที่ไม่เคย track | `git clean -n` (ดูก่อน) → `git clean -fd` |

> [!danger] `restore` และ `clean` กู้คืนไม่ได้
> ไม่แน่ใจ ใช้ `git stash push -u` แทน จะได้กู้คืนได้ภายหลัง

## ลึกกว่านี้

[[Git-Restore]] · [[Git-Add-and-Staging]]
