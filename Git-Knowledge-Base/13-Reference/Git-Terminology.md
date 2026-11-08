---
title: Git Terminology
tags:
  - git
  - glossary
  - terminology
  - reference
type: reference
status: published
---

# Git Terminology: พจนานุกรมศัพท์เทคนิค Git

รวบรวมคำศัพท์เชิงเทคนิค สถาปัตยกรรม และคำศัพท์เฉพาะที่พบบ่อยในระบบ Git พร้อมคำอธิบายและบริบทการใช้งาน

---

## สารบัญคำศัพท์

- **Blob (Binary Large Object):** ออบเจกต์พื้นฐานของ Git ที่จัดเก็บเฉพาะเนื้อหาของไฟล์ (File Contents) ในรูปแบบบีบอัด โดยไม่เก็บชื่อไฟล์หรือสิทธิ์ ([[Git-Object-Model]])
- **Tree:** ออบเจกต์ของ Git ที่ทำหน้าที่แทนโฟลเดอร์หรือไดเรกทอรี บรรจุรายการของ Blobs และ Sub-trees พร้อมระบุชื่อไฟล์และโหมดสิทธิ์ ([[Git-Object-Model]])
- **Commit:** ออบเจกต์ที่ทำหน้าที่บันทึกภาพเสมือน (Snapshot) ของโปรเจกต์ ณ เวลาหนึ่ง ชี้ไปยัง Root Tree และเก็บ Parent Commit(s), วันที่, ผู้เขียน และ Commit Message ([[Git-Commit]])
- **Annotated Tag:** ออบเจกต์หมุดหมายที่เก็บชื่อผู้สร้าง วันที่ ข้อความกำกับ และชี้ไปยัง Commit นิยมใช้มาร์กเวอร์ชัน Release ([[Git-Object-Model]])
- **Repository (Repo):** แหล่งจัดเก็บข้อมูล ประวัติศาสตร์ Metadata และ Object Database ทั้งหมดของ Git อยู่ภายในโฟลเดอร์ `.git/` ([[Repository-and-Working-Tree]])
- **Working Tree (Working Directory):** โฟลเดอร์กายภาพบนฮาร์ดดิสก์ที่มีไฟล์โค้ดเปิดให้เราแก้ไขด้วย IDE ([[Repository-and-Working-Tree]])
- **Index / Staging Area:** ไฟล์ไบนารี `.git/index` ทำหน้าที่เป็นพื้นที่จัดเตรียม Snapshot ก่อนจะถูกกดบันทึกเป็น Commit ([[Git-Add-and-Staging]])
- **HEAD:** ตัวชี้พิเศษ (Symbolic Reference) ที่ระบุว่าในขณะนี้ Working Tree กำลังทำงานอยู่ที่ Commit หรือ Branch ใด ([[Git-References-and-HEAD]])
- **Branch:** ตัวชี้ขนาดเบาที่ขยับไปข้างหน้าได้อัตโนมัติ (Movable Pointer) ชี้ไปยัง Commit ล่าสุดของสายการพัฒนานั้นๆ ([[Branch-Concept]])
- **Detached HEAD:** สภาวะที่ตัวชี้ HEAD ชี้ตรงไปยัง Commit ใด Commit หนึ่งโดยตรง แทนที่จะเกาะอยู่กับชื่อ Branch ([[Detached-HEAD]])
- **Remote:** เซิร์ฟเวอร์สำเนาภายนอกที่โฮสต์ Git Repository เดียวกัน เช่น บน GitHub หรือ GitLab ([[Remote-Repository]])
- **Remote-tracking Branch:** ตัวแทนของกิ่งบน Remote ที่ถูกบันทึกไว้ในเครื่อง Local เช่น `origin/main` ([[Upstream-and-Tracking-Branch]])
- **Upstream:** ความสัมพันธ์การผูกโยง (Tracking) ระหว่าง Local Branch และ Remote Branch เพื่อให้ `git push` และ `pull` ทำงานได้โดยอัตโนมัติ ([[Upstream-and-Tracking-Branch]])
- **Merge Base:** จุดบรรพบุรุษร่วมกันล่าสุด (Lowest Common Ancestor) ของ 2 กิ่งที่กำลังจะถูกรวมเข้าหากัน ([[Git-Merge]])
- **Fast-Forward:** การผสานกิ่งที่ปลายทางเป็นส่วนต่อขยายเชิงเส้นตรง ทำให้ Git แค่เลื่อน Pointer ไปข้างหน้าโดยไม่ต้องสร้าง Commit ใหม่ ([[Git-Merge]])
- **Three-Way Merge:** การผสานโค้ดระหว่าง 2 กิ่งที่แยกสายออกจากกัน โดยอาศัย Merge Base ร่วมกับปลายกิ่งทั้งสอง แล้วสร้าง Merge Commit ใหม่ ([[Git-Merge]])
- **Rebase:** การนำชุด Commit จากกิ่งหนึ่ง ไปทยอยสร้างใหม่ (Replay) บนฐานของอีกกิ่งหนึ่ง ส่งผลให้ค่า Hash ของ Commit เปลี่ยนทั้งหมด ([[Git-Rebase]])
- **Cherry-Pick:** การคัดลอกเฉพาะผลต่างของ Commit ตัวใดตัวหนึ่งมาสร้างเป็น Commit ใหม่บนกิ่งปัจจุบัน ([[Git-Cherry-Pick]])
- **Reflog (Reference Logs):** บันทึกประวัติการขยับตัวทั้งหมดของ HEAD และ Branches ภายในเครื่อง Local ใช้สำหรับกู้คืนงานที่สูญหาย ([[Git-Reflog]])
- **Git Worktree:** สถาปัตยกรรมที่เปิดให้มี Working Directory ทำงานได้หลายโฟลเดอร์พร้อมกัน โดยใช้ Git Database ร่วมกัน ([[Worktree-Concept]])
- **Pull Request (PR):** กระบวนการบนแพลตฟอร์มคลาวด์เพื่อขอส่งมอบ ตรวจสอบ และอภิปรายโค้ดก่อนการรวมเข้าสู่กิ่งหลัก ([[Pull-Request-Workflow]])
- **Squash:** การยุบรวมหลาย Commit ย่อยเข้าด้วยกันเป็น Commit ขนาดใหญ่เพียงอันเดียวเพื่อให้ประวัติศาสตร์กระชับ ([[GitHub-Merge-Strategies]])

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Git-Command-Cheatsheet]] — รวมคำสั่งลัด
- [[Common-Mistakes]] — ข้อผิดพลาดที่พบบ่อย\n