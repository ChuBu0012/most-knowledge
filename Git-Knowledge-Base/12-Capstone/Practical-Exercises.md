---
title: Practical Exercises
tags:
  - git
  - capstone
  - lab
  - exercises
type: exercise
status: in-progress
---

# Practical Exercises: แบบฝึกหัดลงมือปฏิบัติจริง

แบบฝึกหัดชุดนี้ออกแบบมาเพื่อให้ผู้เรียนได้ทดสอบทักษะ Git ในสถานการณ์เสมือนจริง โดยมีขั้นตอนและ **Expected Results (ผลลัพธ์ที่คาดหวัง)** ชัดเจนในทุกข้อ

> [!important] สถานะการเรียน: In Progress
> ให้ผู้เรียนสร้าง Sandbox Repository แยกต่างหากเพื่อทดลองปฏิบัติการตามโจทย์เหล่านี้ทีละข้อ

---

## 🧪 Exercise 1: การจำลองและแก้ไข Detached HEAD

### วัตถุประสงค์:
ฝึกดึงงานออกจากสภาวะหัวขาดโดยไม่สูญเสีย Commit

### ขั้นตอนลงมือทำ:
```bash
# 1. เข้าไปในโฟลเดอร์ทดสอบ
mkdir /tmp/git-lab-detached && cd /tmp/git-lab-detached
git init
echo "version 1" > app.txt && git add . && git commit -m "commit 1"
echo "version 2" > app.txt && git add . && git commit -m "commit 2"
echo "version 3" > app.txt && git add . && git commit -m "commit 3"

# 2. กระโดดไป Commit ที่ 1 ตรงๆ เพื่อสร้างสภาวะ Detached HEAD
FIRST_COMMIT=$(git rev-list --max-parents=0 HEAD)
git checkout $FIRST_COMMIT

# 3. พิมพ์โค้ดและ Commit ในสถานะ Detached HEAD
echo "rescue me" > secret.txt
git add .
git commit -m "important detached work"

# 4. สลับกลับไปยัง main (งานจะหลุดการเชื่อมต่อ!)
git switch main
```

### คำสั่งแก้ปัญหาของผู้เรียน:
ให้ผู้เรียนใช้ `git reflog` และสร้าง Branch กู้คืนไฟล์ `secret.txt` กลับมา

### ผลลัพธ์ที่คาดหวัง (Expected Results):
- รัน `git branch` แล้วพบ Branch ใหม่ เช่น `salvaged-work`
- สลับไป Branch ดังกล่าวแล้วพบไฟล์ `secret.txt` พร้อมเนื้อหา `rescue me` อยู่ครบถ้วน

---

## 🧪 Exercise 2: จำลอง Merge Conflict และสางให้สะอาด

### วัตถุประสงค์:
ฝึกแก้ Conflict Markers และทำความเข้าใจ Three-way merge

### ขั้นตอนลงมือทำ:
```bash
mkdir /tmp/git-lab-conflict && cd /tmp/git-lab-conflict
git init
echo -e "Line 1\nLine 2\nLine 3" > file.txt
git add . && git commit -m "Initial lines"

# กิ่ง main แก้บรรทัด 2 เป็น "Line 2 from MAIN"
echo -e "Line 1\nLine 2 from MAIN\nLine 3" > file.txt
git commit -am "Update line 2 in main"

# สร้างกิ่ง feature แตกจาก Commit แรก
git branch feature HEAD~1
git switch feature
echo -e "Line 1\nLine 2 from FEATURE\nLine 3" > file.txt
git commit -am "Update line 2 in feature"

# ทำการ Merge กิ่ง main เข้ามา
git merge main
```

### ผลลัพธ์ที่คาดหวัง (Expected Results):
- Git รายงาน `CONFLICT (content): Merge conflict in file.txt`
- เปิดไฟล์ `file.txt` จะพบ Conflict markers `<<<<<<< HEAD`, `=======`, `>>>>>>> main`
- ผู้เรียนรวมเนื้อหาเป็น `Line 2 merged successfully`, สั่ง `git add file.txt` และ `git merge --continue`
- รัน `git log --graph --oneline` แล้วพบ Merge Commit เชื่อมโยง 2 สายงานเข้าด้วยกันอย่างถูกต้อง

---

## 🧪 Exercise 3: การรัน Git Worktree ร่วมกับ 2 กิ่ง

### วัตถุประสงค์:
ทดลองเปิด 2 โฟลเดอร์ทำงานคู่ขนานโดยใช้ `.git` เดียวกัน

### ขั้นตอนลงมือทำ:
```bash
mkdir /tmp/git-lab-worktree && cd /tmp/git-lab-worktree
git init
echo "Hello Core" > base.txt
git add . && git commit -m "chore: base commit"

# สร้าง Worktree กิ่ง feature-a
git worktree add ../wt-feature-a -b feature-a
```

### การทดสอบความเข้าใจ:
1. เข้าไปใน `../wt-feature-a` แล้วสร้างไฟล์ `echo "Work from A" > a.txt`, สั่ง `git add .` และ `git commit -m "feat: add A"`
2. กลับมาที่โฟลเดอร์หลัก `/tmp/git-lab-worktree`
3. รัน `git log feature-a --oneline`

### ผลลัพธ์ที่คาดหวัง (Expected Results):
- โฟลเดอร์หลักมองเห็น Commit `"feat: add A"` ทันที โดยไม่ต้องสั่ง Push หรือ Fetch เลย เพราะใช้ Object Database ร่วมกัน!

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[End-to-End-Git-Workflow]] — ภาพรวมเวิร์กโฟลว์ตั้งแต่ต้นจนจบ
- [[Troubleshooting-Scenarios]] — รวมวิธีรับมือข้อผิดพลาด\n