# SEO / AEO / AI Mode Guide

## Overview
คู่มือทำเว็บให้ติด Google + AI อ่านเข้าใจ

---

## 1) เป้าหมาย

1. คนเข้ามา "ได้คำตอบ" ได้เร็ว
2. Google เข้าใจเว็บและจัดอันดับได้
3. AI/LLM อ่านแล้วตอบถูก (สรุปได้ + อ้างอิงได้)
4. ผู้ดูแล: เพิ่มหน้าใหม่ได้เรื่อยๆ โดยไม่พัง SEO

---

## 2) Site Architecture (โครงเว็บ)

### 2.1 โครงหมวดมาตรฐาน (แนะนำ)
- `/getting-started/` - เริ่มต้น/ติดตั้ง/ภาพรวม
- `/guides/` - วิธีทำ (How-to)
- `/troubleshooting/` - แก้ปัญหา (Error/อาการ/สาเหตุ/วิธีแก้)
- `/reference/` - อ้างอิง (พารามิเตอร์/คำศัพท์/ตาราง/ข้อกำหนด)

> หลัก: 1 หน้า = 1 intent (1 คำถาม/1 งาน) เพื่อให้ Google/AI จับประเด็นได้ง่าย

### 2.2 Slug/URL Rules (แนะนำ)
- ใช้ lowercase + hyphen: `how-to-reset-router`
- หลีกเลี่ยงภาษาไทยใน slug หากอยากเข้าถึง/อ้างอิงได้ง่าย
- ให้ slug สื่อ "คำกริยา+วัตถุ": `setup-xxx`, `fix-xxx`, `configure-xxx`

### 2.3 Internal Linking Strategy
ทุกหน้า "ต้องมี":
- **Parent link**: กลับหน้าหมวด (เช่น Guides)
- **Child/Related**: ลิงก์ไปบทที่เกี่ยวข้อง 2-5 บท
- **Troubleshooting** ต้องลิงก์กลับไป "How-to" ที่ใช้แก้สาเหตุ/วิธีทำที่ถูกต้อง

---

## 3) On-page SEO (มาตรฐานต่อหน้า)

### 3.1 Title ที่ดี
- รูปแบบ: `ทำ X ยังไง | ชื่อเว็บ/KB`
- สั้นกระชับ (ไม่ยาวเกิน)
- สื่อ outcome/ผลลัพธ์

### 3.2 Meta description ที่ดี
- 1-2 ประโยค สรุปคำตอบหรือผลลัพธ์
- ให้เหมือน snippet ที่คนอ่านแล้วคลิก

### 3.3 Headings (H1/H2/H3)
- H1 มีได้ 1 ครั้ง/หน้า
- H2/H3 สอดคล้อง "ขั้นตอน/คำถามย่อย"
- หลีกเลี่ยงหัวข้อว่างๆ เช่น "อื่นๆ"

### 3.4 E-E-A-T (ความน่าเชื่อถือ)
ใส่ในหน้า (อย่างน้อยอย่างหนึ่ง):
- Last updated
- เวอร์ชัน/สภาพแวดล้อมที่รองรับ
- ผู้เขียน/ทีม/ข้อมูลติดต่อ
- ลิงก์อ้างอิง (ถ้ามี)

---

## 4) AEO (Answer Engine Optimization)

### 4.1 TL;DR (ต้องมีบนสุด)
เริ่มหน้าเอกสารที่:
- "ทำอะไร" + "ผลลัพธ์" + "ข้อควรระวัง"
- 2-6 bullet

### 4.2 โครง How-to ที่แนะนำ
1. TL;DR
2. Preconditions (ต้องมีอะไรก่อน)
3. Steps (เป็นลิสต์ 1..N)
4. Expected result (ควรให้เห็นอะไร)
5. Common issues (เจออะไรได้บ้าง)
6. Related links

### 4.3 โครง Troubleshooting ที่แนะนำ
1. TL;DR
2. Symptoms (อาการ)
3. Root causes (สาเหตุ)
4. Fix steps (วิธีแก้)
5. Verification (ตรวจว่าหายจริง)
6. Prevention (กันไม่ให้เกิดอีก)
7. Related links

### 4.4 FAQ page แนวทางที่ดีที่สุด
- คำถามใช้ H2/H3
- แต่ละคำตอบเริ่มด้วย 1-2 ประโยคสรุป
- อย่ารวมคำถามคนละ intent ในคำถามเดียว

---

## 5) "AI Mode" (ทำให้ LLM อ่านแล้วตอบได้)

### 5.1 ทำ "Context Graph" ด้วยลิงก์
- Parent/Child/Related links ทำให้ AI เล่าบริบทได้
- Reference pages (glossary, parameter tables) เป็นศูนย์กลางคำศัพท์

### 5.2 Consistency (ศัพท์ต้องตรงกันทั้งเว็บ)
- สร้าง `glossary.md` และลิงก์กลับมาทุกครั้งที่ใช้ศัพท์เฉพาะ
- ตั้งชื่อฟอร์ม/เมนูให้เหมือนกันทั้งเว็บ (อย่าใช้หลายคำเป็นสุ่มๆ)

### 5.3 Tables + Checklists (AI ชอบ)
- ตาราง "ค่า/ความหมาย/ค่าแนะนำ/ตัวอย่าง"
- เช็คลิสต์ "ต้องทำ/หลังทำ"

### 5.4 llms.txt (Optional แต่มีประโยชน์)
เพิ่มไฟล์ `public/llms.txt` เพื่อบอกทางหน้าเริ่มอ่าน (เหมาะกับเว็บคู่มือ)

ตัวอย่าง:
```txt
# Site: Your Knowledge Base
# Start here:
https://example.com/
https://example.com/getting-started/
https://example.com/guides/
https://example.com/troubleshooting/
https://example.com/reference/
https://example.com/reference/glossary/
```

---

## 6) Structured Data (Schema JSON-LD)

> ใส่ใน `<head>` หรือท้าย `<body>` ของหน้า (ตาม layout)

### 6.1 FAQPage (สำหรับหน้า FAQ)
```html
<script type="application/ld+json">
{
  "@context":"https://schema.org",
  "@type":"FAQPage",
  "mainEntity":[
    {
      "@type":"Question",
      "name":"คำถาม A คืออะไร?",
      "acceptedAnswer":{"@type":"Answer","text":"คำตอบสั้นๆ ..."}
    }
  ]
}
</script>
```

### 6.2 HowTo (สำหรับหน้า How-to)
```html
<script type="application/ld+json">
{
  "@context":"https://schema.org",
  "@type":"HowTo",
  "name":"ติดตั้ง X ยังไง",
  "description":"สรุปสั้นๆของวิธีทำ",
  "step":[
    {"@type":"HowToStep","name":"Step 1","text":"ทำ ..."},
    {"@type":"HowToStep","name":"Step 2","text":"ทำ ..."}
  ]
}
</script>
```

### 6.3 BreadcrumbList (ขั้นเว็บ)
```html
<script type="application/ld+json">
{
  "@context":"https://schema.org",
  "@type":"BreadcrumbList",
  "itemListElement":[
    {"@type":"ListItem","position":1,"name":"Home","item":"https://example.com/"},
    {"@type":"ListItem","position":2,"name":"Guides","item":"https://example.com/guides/"},
    {"@type":"ListItem","position":3,"name":"บทนี้","item":"https://example.com/guides/this-page/"}
  ]
}
</script>
```

---

## 7) Technical SEO (ต้องมี)

### 7.1 sitemap.xml
- ต้อง generate sitemap อัตโนมัติ
- ส่ง sitemap ไปยัง Google Search Console

### 7.2 robots.txt
```txt
User-agent: *
Allow: /

Sitemap: https://example.com/sitemap.xml
```

### 7.3 Canonical URL
- ทุกหน้าควรมี canonical ที่กลับ URL หลักของหน้าเอง
- ป้องกัน duplicate (เช่น trailing slash / query)

### 7.4 Open Graph + Twitter Card
ทำให้แชร์แล้วสวย:
- og:title
- og:description
- og:image
- twitter:card

### 7.5 404 / Redirects
- ทำหน้า 404 ดีๆ + ลิงก์กลับหมวดหลัก
- ถ้าเปลี่ยน slug ให้ทำ redirect 301

---

## 8) Performance/UX ที่ส่งผลต่อ SEO

- รูป: ใช้ขนาดเหมาะสม, lazy-load, มี alt
- ลด JS ที่ไม่จำเป็น
- เลี่ยงการใหลตองข้อหนัก
- ทำ TOC/Sidebar ให้คลิกง่าย (ลด bounce)

---

## 9) Checklist ก่อน Deploy

### Per-page Checklist
- [ ] Title ดี + ไม่ยาวเกิน
- [ ] Description สรุป 1-2 ประโยค
- [ ] TL;DR อยู่บนสุด
- [ ] มี steps/ตาราง/เช็คลิสต์ (ตามประเภทหน้า)
- [ ] มี Related links อย่างน้อย 2 ลิงก์
- [ ] รูปมี alt
- [ ] มี updatedDate (ถ้าแก้ไข)

### Site Checklist
- [ ] ตั้ง site URL ถูกต้อง
- [ ] มี sitemap.xml
- [ ] มี robots.txt
- [ ] มี canonical ทุกหน้า
- [ ] มี OG image default
- [ ] มี 404 page
- [ ] มี glossary/reference page (ช่วย AI + consistency)
- [ ] (Optional) มี `llms.txt`

---

## 10) Content Templates

### Template: How-to Page
```md
---
title: "ทำ X ยังไง (สรุปเร็ว + ขั้นตอน)"
description: "คำตอบสั้นๆ 1-2 ประโยค สำหรับบทความการทำ X ที่นี่"
---

## สรุปเร็ว (TL;DR)
- ผลลัพธ์ที่ได้: ...
- ใช้เวลา: ...
- ต้องมี/เงื่อนไข: ...
- ข้อควรระวัง: ...

## ต้องมีอะไรก่อน (Preconditions)
- ...

## ขั้นตอน (Steps)
1. ...
2. ...
3. ...

## ผลลัพธ์ที่ควรให้เห็น (Expected result)
- ...

## ปัญหาที่พบบ่อย (Common issues)
### อาการ: ...
- สาเหตุ: ...
- วิธีแก้: ...

## อ่านต่อ (Related)
- [หน้าหมวด Guides](/guides/)
- ...
```

### Template: Troubleshooting Page
```md
---
title: "แก้ปัญหา: X (Error/อาการ)"
description: "สรุปสาเหตุและวิธีแก้ X ให้เร็วที่สุด"
---

## สรุปเร็ว (TL;DR)
- สาเหตุที่พบบ่อย: ...
- วิธีแก้เร็ว: ...
- วิธีตรวจว่าหาย: ...

## อาการ (Symptoms)
- ...

## สาเหตุ (Root causes)
- ...

## วิธีแก้ (Fix)
1. ...
2. ...

## ตรวจสอบ (Verification)
- ...

## ป้องกัน (Prevention)
- ...

## อ่านต่อ (Related)
- [หน้าหมวด Troubleshooting](/troubleshooting/)
- ...
```

### Template: FAQ Page
```md
---
title: "FAQ: หัวข้อ X"
description: "คำถามที่พบบ่อยเกี่ยวกับ X พร้อมคำตอบสั้นๆและลิงก์ไปวิธีทำ"
---

## คำถาม: A คืออะไร?
คำตอบสั้นๆ: ...
รายละเอียด: ...

## คำถาม: ทำ B ยังไง?
คำตอบสั้นๆ: ...
รายละเอียด: ... (ลิงก์ไป How-to)

## อ่านต่อ
- ...
```
