---
title: "How-To: เอาไฟล์ที่ commit ไปแล้วออก (.gitignore ไม่ทำงาน / secret หลุด)"
aliases:
  - gitignore ไม่ทำงาน
  - untrack file
  - commit .env
  - secret หลุด
  - git rm --cached
tags: [git, how-to, gitignore, security]
type: how-to
status: published
---

# เอาไฟล์ที่ Commit ไปแล้วออกจาก Git

> `.gitignore` มีผลกับไฟล์ที่ **ยังไม่เคยถูก track** เท่านั้น ไฟล์ที่ commit ไปแล้วต้องเอาออกเอง

## กรณีทั่วไป (เช่น `node_modules/`, `.DS_Store`)

```bash
echo "node_modules/" >> .gitignore
git rm -r --cached node_modules     # ลบออกจาก Git แต่ไฟล์ในเครื่องยังอยู่
git commit -m "chore: stop tracking node_modules"
```

## กรณี Secret หลุด (`.env`, API key)

1. **Rotate / เปลี่ยน key ทันที** ← สำคัญที่สุด ถือว่า key นั้นหลุดแล้วแม้จะลบจากประวัติ
2. หยุด track:
   ```bash
   echo ".env" >> .gitignore
   git rm --cached .env
   git commit -m "chore: stop tracking .env"
   ```
3. ถ้ายังไม่ Push: ลบออกจาก commit ล่าสุดได้ด้วย `git commit --amend` หลังขั้น 2
4. ถ้า Push ไปแล้วและต้องล้างประวัติ: ใช้ `git filter-repo` (ต้องประสานทีม เพราะเปลี่ยนประวัติทั้งหมด)

## ตรวจ

```bash
git ls-files | grep -E "\.env|node_modules"   # ต้องไม่เจอ
git check-ignore -v .env                       # ต้องบอกว่าถูก ignore โดยบรรทัดไหน
```

## ลึกกว่านี้

[[Gitignore]]
