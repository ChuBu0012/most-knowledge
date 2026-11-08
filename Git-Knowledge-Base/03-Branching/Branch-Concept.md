---
title: Branch Concept
tags:
  - git
  - branching
  - foundations
  - mental-model
type: concept
status: published
---

# Branch Concept

ในระบบควบคุมเวอร์ชันดั้งเดิม การสร้างกิ่ง (Branch) หมายถึงการคัดลอกไฟล์ทั้งหมดในโปรเจกต์ไปยังโฟลเดอร์ใหม่ ซึ่งกินพื้นที่ดิสก์และใช้เวลานาน แต่ใน Git **Branch เป็นเพียงตัวชี้ขนาดเบา (Lightweight Movable Pointer)** ไปยัง Commit ล่าสุดในสายงานนั้นๆ

---

## 1. นิยามเชิงลึก: Branch คืออะไรกันแน่?

โครงสร้างของ Git เก็บประวัติศาสตร์ในรูปแบบ **Directed Acyclic Graph (DAG)** โดย Commit แต่ละตัวจะชี้กลับไปยัง Parent Commit ของตนเอง

เมื่อเราสร้าง Branch ขึ้นมา 1 ตัว สิ่งที่ Git สร้างขึ้นมาจริงๆ คือ:
- ไฟล์ข้อความขนาดประมาณ 41 ไบต์ ในโฟลเดอร์ `.git/refs/heads/<branch-name>`
- ภายในไฟล์มีเพียงข้อความ String ของเลข Commit Hash 40 ตัวอักษร
- ไม่มีการสำเนาไฟล์ต้นฉบับซ้ำซ้อนแม้แต่ไฟล์เดียว!

```mermaid
graph LR
    subgraph CommitHistory["Commit Graph (DAG)"]
        C1["Commit C1\n(Initial)"] <-- C2["Commit C2"]
        C2 <-- C3["Commit C3\n(on main)"]
        C2 <-- C4["Commit C4\n(on feature)"]
    end

    MainBranch["Branch Ref: main"] --> C3
    FeatureBranch["Branch Ref: feature"] --> C4
    HEAD["HEAD"] --> FeatureBranch
```

จากแผนภาพ:
- Branch `main` ชี้ไปที่ Commit `C3`
- Branch `feature` ชี้ไปที่ Commit `C4`
- `HEAD` ชี้ไปที่ Branch `feature` หมายความว่าขณะนี้เรากำลังทำงานอยู่ในสายงาน `feature`

---

## 2. Fast-Forward Concept

เมื่อต้องการผสาน (Merge) สองกิ่งเข้าด้วยกัน หากสายงานปลายทางไม่ได้แตกแขนงแยกออกจากกัน แต่กิ่งหนึ่งเป็นเพียงส่วนต่อขยายเชิงเส้นตรงของอีกกิ่งหนึ่ง จะเกิดสิ่งที่เรียกว่า **Fast-Forward**:

```mermaid
graph LR
    subgraph ก่อน Merge
        A[Commit A] <-- B[Commit B (main)] <-- C[Commit C] <-- D[Commit D (feature)]
    end
```

ในสถานการณ์นี้:
- `main` อยู่ที่ `B` และไม่มี Commit อื่นใดเกิดขึ้นบน `main` เลยนับตั้งแต่แตกกิ่ง `feature` ออกไป
- เมื่อสั่ง `git merge feature` บนกิ่ง `main` Git จะไม่จำเป็นต้องสร้าง Commit ใหม่ขึ้นมา
- สิ่งที่ Git ทำคือเพียง **เลื่อน Pointer ของ `main` ให้วิ่งพรวดไปชี้ที่ `D` ตัวเดียวกับ `feature`** ทันที ซึ่งรวดเร็วมากระดับเสี้ยววินาที

---

## 3. ทำไมการแตกกิ่งใน Git จึงทรงพลัง?

1. **ต้นทุนต่ำเกือบเป็นศูนย์ (Zero Overhead):** การสร้าง สลับ หรือลบ Branch กินทรัพยากรดิสก์และเวลาเท่ากับการเขียนไฟล์ข้อความบรรทัดเดียว
2. **การแยกบริบทอย่างสมบูรณ์ (Context Isolation):** นักพัฒนาสามารถทดลองเขียนโค้ดใหม่ ทดสอบไอเดีย หรือแก้บั๊กเร่งด่วนได้โดยไม่รบกวนความเสถียรของกิ่งหลัก (`main`)
3. **ส่งเสริม Parallel Development:** ทำให้สมาชิกหลายคนสามารถพัฒนาคนละฟีเจอร์พร้อมๆ กันได้อย่างอิสระ (ศึกษาเพิ่มเติมใน [[Parallel-Development-Concept]])

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-References-and-HEAD]] — การทำงานของ Refs และ HEAD
- [[Branch-Commands]] — คำสั่งสร้าง สลับ และลบกิ่ง
- [[Detached-HEAD]] — สภาวะเมื่อ HEAD หลุดออกจาก Branch
- [[Git-Merge]] — การผสานกิ่งและการจัดการ Fast-forward\n