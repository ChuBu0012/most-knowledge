---
title: Troubleshooting Scenarios
tags:
  - git
  - troubleshooting
  - debugging
  - emergency
type: reference
status: in-progress
---

# Troubleshooting Scenarios: ปัญหาฉุกเฉินและวิธีแก้เฉียบพลัน

รวบรวม 5 สถานการณ์วิกฤตที่วิศวกรซอฟต์แวร์มักพบเจอ พร้อมรูปแบบการวินิจฉัยและขั้นตอนแก้ปัญหาแบบเป็นขั้นเป็นตอน

---

## 🚨 Scenario 1: เผลอสั่ง `git reset --hard` งานทั้งวันหายหมด!

- **Symptoms:** พิมพ์คำสั่ง `git reset --hard` ผิด แล้วพบว่า Commit ที่ทำไว้หายไปจาก `git log`
- **Cause:** ตัวชี้ Branch ถูกเลื่อนถอยหลังไปในอดีต
- **Diagnosis:** ใช้ `git reflog` ตรวจสอบประวัติการเคลื่อนไหวของ HEAD
- **Solution:**
  ```bash
  # 1. ค้นหารหัส Commit ล่าสุดก่อนเกิดเหตุใน reflog
  git reflog
  # พบรายการ HEAD@{1}: commit: my lost feature (hash: 7c2a1b)

  # 2. กู้คืนด้วยการเลื่อนกิ่งกลับมารับ
  git reset --hard 7c2a1b
  ```
- **Prevention:** ตรวจสอบชื่อ Commit และสถานะทุกครั้งก่อนสั่งคำสั่งที่มีธง `--hard`

---

## 🚨 Scenario 2: Push งานขึ้น Remote แล้วถูก Reject (Non-fast-forward)

- **Symptoms:**
  ```text
  ! [rejected]        main -> main (fetch first)
  error: failed to push some refs to '...'
  hint: Updates were rejected because the remote contains work that you do not have locally.
  ```
- **Cause:** เพื่อนร่วมทีมเพิ่ง Push โค้ดใหม่ขึ้นเซิร์ฟเวอร์ ทำให้ประวัติบน Remote ก้าวนำหน้าเครื่องคุณ
- **Diagnosis:** รัน `git fetch` แล้วใช้ `git log HEAD..origin/main --oneline` ส่องดู
- **Solution (ปลอดภัยและสะอาดที่สุด):**
  ```bash
  git pull --rebase origin main
  # หากมี conflict ให้แก้ทีละจุด -> git add . -> git rebase --continue
  git push origin main
  ```
- **Prevention:** อย่าใช้ `git push --force` หากไม่ใช่กิ่งส่วนตัวที่มีข้อตกลงชัดเจน

---

## 🚨 Scenario 3: สลับกิ่งไม่ได้เพราะไฟล์ติดล็อก

- **Symptoms:**
  ```text
  error: Your local changes to the following files would be overwritten by checkout:
      src/app.ts
  Please commit your changes or stash them before you switch branches.
  ```
- **Cause:** ไฟล์ `src/app.ts` ในกิ่งปัจจุบันมีการแก้ไขค้างไว้ และกิ่งปลายทางมีเนื้อหาไฟล์นี้ต่างออกไป
- **Solution:**
  - **ทางเลือก A (พักงานไว้ก่อน):**
    ```bash
    git stash
    git switch <target-branch>
    # เมื่อกลับมา: git stash pop
    ```
  - **ทางเลือก B (เปิดโฟลเดอร์คู่ขนานโดยไม่ต้องสลับ):**
    ```bash
    git worktree add ../another-branch <target-branch>
    ```

---

## 🚨 Scenario 4: เผลอ Commit ข้อมูลความลับ (API Keys/Passwords) ลง Git

- **Symptoms:** พบไฟล์ `.env` หรือ Private Key ติดอยู่ในประวัติศาสตร์ Commit
- **Cause:** ไม่ได้ใส่ไฟล์ใน `.gitignore` ก่อนสั่ง `git add .`
- **Solution (หากยังไม่ได้ Push):**
  ```bash
  # ถอยหลัง Commit 1 ครั้งโดยยังรักษาไฟล์ไว้ในเครื่อง
  git reset --soft HEAD~1
  # เอาไฟล์ความลับออกจาก Staging
  git reset .env
  # ใส่ .env ลงใน .gitignore
  echo ".env" >> .gitignore
  git add .gitignore
  git commit -m "feat: commit code without secret"
  ```
- **Solution (หาก Push ขึ้น GitHub ไปแล้ว):**
  - **ต้องเพิกถอน (Revoke) และ Rotate คีย์ตัวนั้นทันทีที่ระบบผู้ให้บริการ!** เพราะไม่ว่าจะแก้ Git ประวัติอย่างไร บอทสแกนเนอร์บนอินเทอร์เน็ตอาจบันทึกคีย์ไปแล้ว
  - ใช้เครื่องมืออย่าง `git-filter-repo` หรือ BFG Repo-Cleaner เพื่อล้างคีย์ออกจากประวัติทั้งระบบ

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-Reflog]] — การกู้คืนด้วยกล่องดำ
- [[Undo-Command-Comparison]] — สรุปคำสั่ง Undo ทั้งหมด
- [[Gitignore]] — การป้องกันไฟล์หลุดเข้า Git\n