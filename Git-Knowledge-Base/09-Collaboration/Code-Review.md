---
title: Code Review
tags:
  - git
  - collaboration
  - code-review
  - best-practices
type: concept
status: published
---

# Code Review

**Code Review (การตรวจทานโค้ด)** คือขั้นตอนทางวิศวกรรมที่สมาชิกในทีมช่วยกันตรวจสอบโค้ดที่เพื่อนร่วมทีมหรือ AI พัฒนาขึ้นมา ก่อนจะรวมเข้าสู่สายการผลิตจริง เพื่อเพิ่มคุณภาพ ป้องกันข้อผิดพลาด และถ่ายทอดองค์ความรู้ภายในทีม

---

## 1. วัตถุประสงค์ของการทำ Code Review

1. **ดักจับข้อผิดพลาด (Defect Detection):** ค้นหาตรรกะที่ผิดพลาด (Edge cases), ปัญหาความปลอดภัย (Security vulnerabilities), หรือ Performance bottlenecks ที่ Automated test อาจครอบคลุมไม่ถึง
2. **รักษามาตรฐานโค้ด (Maintainability & Consistency):** มั่นใจว่าโค้ดเป็นไปตาม Architecture guidelines, Design patterns และมาตรฐานการเขียนของทีม
3. **การแบ่งปันความรู้ (Knowledge Sharing):** ทำให้ไม่มีใครเป็น "คนเดียวในโลกที่เข้าใจโมดูลนี้" (ลด Bus factor)

---

## 2. จิตวิทยาและวัฒนธรรมการรีวิว (Review Etiquette)

- **วิจารณ์ที่โค้ด ไม่ใช่วิจารณ์ตัวบุคคล:** ใช้คำถามเชิงบวก เช่น *"ตรงนี้ถ้าเกิดเน็ตเวิร์กหลุด จะเกิดอะไรขึ้นกับ state ครับ?"* แทนที่จะใช้คำว่า *"ทำไมคุณเขียนโค้ดไม่ดัก error แบบนี้?"*
- **ใช้เกณฑ์กำกับระดับความเห็น (Conventional Comments):**
  - `praise:` ชื่นชมโค้ดที่ดี เช่น `praise: การแยก helper ฟังก์ชันตรงนี้ทำให้โค้ดอ่านง่ายมากครับ`
  - `nit:` (Nitpick) ประเด็นเล็กน้อย ไม่ซีเรียส ไม่บล็อกการ merge เช่น `nit: เว้นบรรทัดตรงนี้เกินไป 1 บรรทัดครับ`
  - `question:` คำถามเพื่อความเข้าใจ ไม่ได้บอกว่าผิด
  - `issue:` หรือ `blocker:` ปัญหาร้ายแรงที่ต้องแก้ไขก่อน merge เช่น บั๊กความปลอดภัยหรือ memory leak

---

## 3. เช็คลิสต์สำหรับผู้รีวิว (Reviewer Checklist)

```mermaid
checklist
    "Architecture: สอดคล้องกับโครงสร้างและ Layer ของระบบหรือไม่?"
    "Correctness: ทำงานได้ตามโจทย์ Acceptance Criteria ครบถ้วนหรือไม่?"
    "Edge Cases: ดักจับค่า null, undefined, empty array หรือกรณี network error หรือยัง?"
    "Security: มีการป้องกัน SQL Injection, XSS, หรือการเปิดเผย Token หรือไม่?"
    "Testing: มี Unit Tests / Integration Tests ครอบคลุมหรือไม่?"
```

---

## 🔗 โน้ตที่เกี่ยวข้อง
- [[Pull-Request-Workflow]] — กระบวนการเปิด PR
- [[GitHub-Merge-Strategies]] — การผสานโค้ดหลังผ่าน Review\n