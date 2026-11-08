---
title: Fetch Pull Push
tags:
  - git
  - remote
  - commands
  - synchronization
type: concept
status: published
---

# Fetch, Pull, and Push

สามคำสั่งหลักในการถ่ายโอนข้อมูลระหว่าง Local Repository และ Remote Repository คือ `git fetch`, `git pull`, และ `git push` ความเข้าใจที่ผิดพลาดเกี่ยวกับคำสั่งเหล่านี้มักเป็นสาเหตุหลักของปัญหา Merge Conflict โดยไม่จำเป็น

---

## 1. เปรียบเทียบชัดเจน: Fetch vs Pull vs Push

| มิติ | `git fetch` | `git pull` | `git push` |
| :--- | :--- | :--- | :--- |
| **ทิศทางข้อมูล** | Remote $\rightarrow$ Local Repo | Remote $\rightarrow$ Local Repo $\rightarrow$ **Working Tree** | Local Repo $\rightarrow$ Remote Repo |
| **ผลต่อ Working Tree** | **ไม่มีเลย (ปลอดภัย 100%)** | **มีทันที** (นำโค้ดมารวมและแก้ไฟล์ในเครื่อง) | ไม่มีผลต่อ Working Tree ในเครื่อง |
| **ความเสี่ยง Conflict** | ไม่มีทางเกิด Conflict | อาจเกิด Conflict ทันทีถ้าโค้ดชนกัน | อาจถูกปฏิเสธ (Rejected) ถ้า Remote ล้ำหน้า |
| **สมการการทำงาน** | `fetch = download objects` | `pull = fetch + merge` (หรือ rebase) | `push = upload objects + update refs` |

---

## 2. เจาะลึก `git fetch` — สายลับสำรวจสถานการณ์

- **คำสั่งคืออะไร:** การดาวน์โหลด Commit Objects, Tags, และ References ทั้งหมดจาก Remote ลงมาเก็บไว้ในฐานข้อมูล `.git` ของเครื่องคุณ
- **สิ่งที่เปลี่ยน:** Pointer ของ **Remote-tracking Branches** (เช่น `origin/main`) จะถูกปรับปรุงให้ตรงกับเซิร์ฟเวอร์
- **สิ่งที่คงเดิม:** Local Branch ปัจจุบัน และ Working Tree ของคุณจะไม่ขยับเขยื้อนแม้แต่น้อย!
- **ควรใช้เมื่อใด:** ก่อนตัดสินใจรวมโค้ด หรือเมื่อต้องการดูว่าเพื่อนร่วมทีม push อะไรขึ้นไปบ้างโดยไม่ต้องการให้โค้ดปัจจุบันของเราปั่นป่วน

```bash
# ดึงข้อมูลจากทุก Remote
git fetch --all

# ดูว่า Remote ไปไกลกว่าเรากี่ Commit
git log HEAD..origin/main --oneline
```

---

## 3. เจาะลึก `git pull` — ดึงและรวมร่างทันที

`git pull` คือชอร์ตคัตที่ทำงานสองขั้นต่อกัน:
$$\text{git pull} = \text{git fetch} + \text{git merge (หรือ git rebase)}$$

### รูปแบบการใช้งานที่ดี:
```bash
# แบบปกติ (สร้าง Merge Commit ถ้ามีประวัติแยกจากกัน)
git pull origin main

# แบบ Rebase (แนะนำสำหรับ Feature Branch เพื่อประวัติศาสตร์ที่เรียบตรง)
git pull --rebase origin main
```

> [!important] พฤติกรรม Pull Rebase
> การตั้งค่า `git config --global pull.rebase true` จะช่วยลดการเกิด "Merge branch 'main' of github.com..." รกใน Git Log ได้อย่างมหาศาล

---

## 4. เจาะลึก `git push` — ตีพิมพ์ผลงานสู่สากล

- **คำสั่งคืออะไร:** การส่งออบเจกต์ Commit ที่เราทำไว้ใน Local ขึ้นไปยังเซิร์ฟเวอร์ และเลื่อน Pointer ของ Branch บนเซิร์ฟเวอร์ให้มาชี้ที่เดียวกับเรา
```bash
# Push ครั้งแรกของ Branch พร้อมตั้งค่า Upstream Tracking
git push -u origin feature/user-profile

# Push ครั้งถัดไปสำหรับ Branch เดิมที่ผูก Tracking ไว้แล้ว
git push
```

### การถูกปฏิเสธ (Push Rejected):
หากเซิร์ฟเวอร์มี Commit ใหม่ที่เพื่อนร่วมทีมเพิ่ง Push ไปก่อนหน้า Git จะปฏิเสธการ Push ของเรา (Non-fast-forward reject):
- **วิธีแก้ที่ถูกต้อง:** ห้ามใช้ `--force` เด็ดขาด! ให้สั่ง `git pull --rebase` เพื่อดึงโค้ดเพื่อนมารองเป็นฐานในเครื่องก่อน แล้วจึงสั่ง `git push` อีกครั้ง

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Remote-Repository]] — สถาปัตยกรรมรีโมต
- [[Upstream-and-Tracking-Branch]] — ความสัมพันธ์ของ Tracking Branch
- [[Git-Merge]] — การรวมโค้ด
- [[Git-Rebase]] — การเรียงประวัติใหม่\n