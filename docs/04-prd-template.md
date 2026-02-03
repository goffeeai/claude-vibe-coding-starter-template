# PRD Template

## วิธีเขียน PRD (Product Requirements Document)

PRD คือเอกสารที่อธิบายว่าโปรเจคคืออะไร ทำอะไร สำหรับใคร

---

## Template

```markdown
# [ชื่อโปรเจค] - PRD

## Overview
อธิบายสั้นๆ 1-2 ประโยคว่าโปรเจคนี้คืออะไร

## Problem Statement
ปัญหาที่ต้องการแก้คืออะไร?

## Target Users
ใครจะใช้งาน?
- User type 1: ...
- User type 2: ...

## Core Features
### MVP (Must Have)
- [ ] Feature 1
- [ ] Feature 2
- [ ] Feature 3

### Nice to Have
- [ ] Feature 4
- [ ] Feature 5

## User Flows

### Flow 1: [ชื่อ Flow]
1. User ทำ X
2. System แสดง Y
3. User เลือก Z
4. Result: ...

## Technical Requirements

### Frontend
- Framework: ...
- UI Library: ...

### Backend
- Runtime: ...
- Framework: ...
- Database: ...

### Deployment
- Hosting: ...
- Domain: ...

## Timeline
- Phase 1: MVP
- Phase 2: Enhanced features
- Phase 3: Optimization

## Success Metrics
- Metric 1: ...
- Metric 2: ...
```

---

## ตัวอย่าง: E-commerce Dashboard

```markdown
# E-commerce Dashboard - PRD

## Overview
Dashboard สำหรับจัดการร้านค้าออนไลน์ ดูยอดขาย จัดการสินค้า และออเดอร์

## Problem Statement
เจ้าของร้านต้องการเครื่องมือที่ใช้ง่ายสำหรับดูภาพรวมธุรกิจและจัดการสินค้า

## Target Users
- เจ้าของร้านค้าออนไลน์ขนาดเล็ก-กลาง
- พนักงาน admin ที่ดูแลสินค้า

## Core Features

### MVP
- [x] Dashboard แสดงยอดขายรายวัน/เดือน
- [x] รายการสินค้า CRUD
- [x] รายการออเดอร์
- [x] Login/Logout

### Nice to Have
- [ ] Export รายงาน Excel
- [ ] แจ้งเตือน stock ใกล้หมด
- [ ] Multiple admin accounts

## User Flows

### Login Flow
1. User เข้าหน้า /login
2. กรอก email + password
3. System ตรวจสอบ credentials
4. Redirect ไป /dashboard

### Add Product Flow
1. User คลิก "Add Product"
2. กรอกข้อมูล: ชื่อ, ราคา, stock, รูป
3. คลิก Save
4. System บันทึกและแสดงในรายการ

## Technical Requirements

### Frontend
- Framework: Next.js 14
- UI: Tailwind + Shadcn/ui
- State: React Query

### Backend
- API: Next.js API Routes
- Database: PostgreSQL (Supabase)
- ORM: Prisma
- Auth: NextAuth.js

### Deployment
- Hosting: Vercel
- Database: Supabase
- Domain: dashboard.mystore.com

## Timeline
- Week 1-2: MVP Dashboard + Products
- Week 3: Orders management
- Week 4: Testing + Deploy

## Success Metrics
- เจ้าของร้านสามารถดูยอดขายได้ภายใน 3 คลิก
- เพิ่มสินค้าใหม่ได้ภายใน 1 นาที
```

---

## Tips

1. **เริ่มจาก MVP** - ทำแค่ที่จำเป็นก่อน
2. **User Flows ชัดเจน** - AI จะเข้าใจง่าย
3. **Technical Requirements ครบ** - ไม่ต้องถามซ้ำ
4. **อัพเดทบ่อยๆ** - เมื่อ requirements เปลี่ยน
