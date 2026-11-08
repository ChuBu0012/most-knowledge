---
title: Gitignore
tags:
  - git
  - configuration
  - security
type: concept
status: published
---

# Gitignore

ไฟล์ `.gitignore` คือไฟล์ข้อความธรรมดาที่วางไว้ใน Repository เพื่อระบุให้ Git เพิกเฉยและละเว้น (Ignore) ไฟล์หรือโฟลเดอร์ที่ไม่ต้องการให้ถูกติดตาม (Untracked Files) เข้าสู่ระบบควบคุมเวอร์ชัน

---

## 1. ทำไมต้องใช้ `.gitignore`?

หากไม่มีการกำหนด `.gitignore` นักพัฒนามักเผลอ commit ไฟล์ที่ไม่สมควรเข้าไป:
1. **ไฟล์ที่เกิดจากการ Build/Compile:** เช่น `dist/`, `build/`, `*.class`, `*.o` ซึ่งมีขนาดใหญ่และเปลี่ยนแปลงตลอดเวลา
2. **Dependencies และไลบรารีภายนอก:** เช่น `node_modules/`, `vendor/` ซึ่งควรติดตั้งผ่าน Package Manager แทนที่จะนำมาเก็บใน Git
3. **ไฟล์ความลับและคอนฟิกเฉพาะเครื่อง (Secrets & Environment):** เช่น `.env`, `credentials.json`, Private Keys ซึ่งหากหลุดเข้า Git อาจก่อให้เกิดความเสียหายด้านความปลอดภัยระดับร้ายแรง
4. **ไฟล์ขยะของระบบปฏิบัติการและ IDE:** เช่น `.DS_Store` (macOS), `Thumbs.db` (Windows), `.idea/` หรือ `.vscode/`

---

## 2. ไวยากรณ์และรูปแบบแพทเทิร์น (Pattern Matching Syntax)

```gitignore
# 1. ความคิดเห็น (Comment) เริ่มต้นด้วยเครื่องหมาย #
# ละเว้นไฟล์เดียวระบุชื่อตรงๆ
secrets.env

# 2. เครื่องหมาย Wildcard (*) แทนตัวอักษรใดๆ
*.log
*.tmp

# 3. ละเว้นทั้งโฟลเดอร์ ลงท้ายด้วยเครื่องหมายทับ (/)
node_modules/
dist/
coverage/

# 4. เครื่องหมาย Double Asterisk (**) ค้นหาในโฟลเดอร์ย่อยทุกลำดับชั้น
logs/**/*.log

# 5. ข้อยกเว้นด้วยเครื่องหมายอัศเจรีย์ (!) — ละเว้นทั้งหมดแต่ยกเว้นไฟล์นี้
*.pdf
!important-guide.pdf
```

---

## 3. ปัญหาคลาสสิก: ใส่ชื่อใน `.gitignore` แล้ว แต่ Git ยังคงฟ้องว่าไฟล์เปลี่ยน!

> [!warning] กฎเหล็กของ Gitignore
> `.gitignore` มีผลเฉพาะกับ **Untracked Files (ไฟล์ที่ Git ยังไม่เคยบันทึกมาก่อน)** เท่านั้น!
> หากไฟล์ใดเคยถูกสั่ง `git add` และ `git commit` บันทึกเข้าประวัติศาสตร์ไปแล้ว แม้ภายหลังจะนำชื่อไปเขียนลงใน `.gitignore` Git จะยังคงติดตาม (Track) การเปลี่ยนแปลงของไฟล์นั้นต่อไปเรื่อยๆ

### วิธีแก้ไข (The Fix):
ต้องสั่งให้ Git ลบไฟล์นั้นออกจาก Staging Area/Index โดยไม่ต้องลบไฟล์จริงบนฮาร์ดดิสก์:
```bash
# 1. นำไฟล์ออกจาก Git Index (คงไฟล์จริงไว้ในเครื่อง)
git rm --cached .env

# หรือหากเป็นทั้งโฟลเดอร์
git rm -r --cached node_modules/

# 2. ทำการ Commit การเปลี่ยนแปลงนี้
git commit -m "chore: stop tracking .env and untracked files"
```

---

## 4. ระดับการ Ignore: Local vs Global

- **Repository Level (`.gitignore` ในรากโปรเจกต์):** แชร์ร่วมกับทุกคนในทีมผ่านการ Commit เข้า Git
- **Personal Local Level (`.git/info/exclude`):** มีผลเฉพาะ Repository นี้บนเครื่องคุณคนเดียว และจะไม่ถูก Commit แชร์ให้ผู้อื่น
- **Global Level (`~/.gitignore_global`):** มีผลกับทุกโปรเจกต์ในเครื่องของคุณ เหมาะสำหรับใส่ `.DS_Store` หรือ `.vscode/`
  ```bash
  git config --global core.excludesfile ~/.gitignore_global
  ```

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Repository-and-Working-Tree]] — โครงสร้าง Working Tree
- [[Git-Basic-Workflow]] — การคัดกรองไฟล์ก่อนเข้าสู่วงจรการทำงาน
- [[Common-Mistakes]] — ข้อผิดพลาดที่พบบ่อยเกี่ยวกับการจัดการไฟล์\n