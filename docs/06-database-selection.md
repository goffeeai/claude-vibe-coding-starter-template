# Database Selection Guide

## เลือก Database อย่างไร?

### Quick Decision

| ต้องการ | เลือก |
|---------|------|
| เริ่มต้นง่ายสุด | **SQLite** |
| Free tier ดี | **Supabase** / **Neon** |
| Real-time sync | **Supabase** / **Firebase** |
| NoSQL flexible | **MongoDB** |
| Production scale | **PostgreSQL** |
| Caching | **Redis** |
| Edge/Serverless | **Turso** / **PlanetScale** |

---

## รายละเอียด

### SQLite
**ดีสำหรับ:** โปรเจคเล็ก, prototype, local development
**ข้อดี:** ไม่ต้อง setup, ไฟล์เดียว
**ข้อเสีย:** ไม่เหมาะกับ concurrent writes มากๆ

```javascript
// ใช้กับ better-sqlite3
import Database from 'better-sqlite3';
const db = new Database('app.db');
```

---

### PostgreSQL
**ดีสำหรับ:** Production apps, complex queries
**ข้อดี:** Reliable, feature-rich, JSON support
**ข้อเสีย:** ต้อง host เอง (หรือใช้ managed service)

**Managed Services:**
- Supabase (free tier)
- Neon (serverless)
- Railway
- Render

---

### Supabase
**ดีสำหรับ:** Full-stack apps, need auth + storage
**ข้อดี:** PostgreSQL + Auth + Storage + Realtime
**ข้อเสีย:** Vendor lock-in บางส่วน

**Free tier:**
- 500 MB database
- 1 GB file storage
- 50,000 monthly active users

---

### Firebase
**ดีสำหรับ:** Mobile apps, real-time apps
**ข้อดี:** Real-time sync, offline support
**ข้อเสีย:** NoSQL learning curve, pricing can scale

**Services:**
- Firestore (database)
- Authentication
- Cloud Storage
- Hosting

---

### MongoDB
**ดีสำหรับ:** Flexible schema, document storage
**ข้อดี:** JSON-like documents, horizontal scaling
**ข้อเสีย:** No relations, eventual consistency

```javascript
// ใช้กับ Mongoose
const userSchema = new Schema({
  name: String,
  email: String,
  orders: [{ type: Schema.Types.ObjectId, ref: 'Order' }]
});
```

---

### PlanetScale
**ดีสำหรับ:** Serverless MySQL, branching workflows
**ข้อดี:** Git-like branching, zero-downtime migrations
**ข้อเสีย:** No foreign keys (by design)

---

### Neon
**ดีสำหรับ:** Serverless PostgreSQL
**ข้อดี:** Branch databases, scale to zero
**ข้อเสีย:** Cold start latency

---

### Turso
**ดีสำหรับ:** Edge deployment, low latency
**ข้อดี:** SQLite at the edge, embedded replicas
**ข้อเสีย:** ใหม่, ecosystem ยังเล็ก

---

### Redis
**ดีสำหรับ:** Caching, sessions, queues
**ข้อดี:** Ultra-fast, in-memory
**ข้อเสีย:** Not for primary storage

**Use cases:**
- Session storage
- Rate limiting
- Real-time leaderboards
- Job queues

---

## Decision Matrix

```
┌─────────────────┬──────────┬──────────┬──────────┬──────────┐
│                 │ Free Tier│ Real-time│ Serverless│ Scale    │
├─────────────────┼──────────┼──────────┼──────────┼──────────┤
│ SQLite          │ ✅       │ ❌       │ ❌        │ ❌       │
│ PostgreSQL      │ ❌       │ ❌       │ ❌        │ ✅       │
│ Supabase        │ ✅       │ ✅       │ ✅        │ ✅       │
│ Firebase        │ ✅       │ ✅       │ ✅        │ ✅       │
│ MongoDB         │ ✅       │ ✅       │ ✅        │ ✅       │
│ PlanetScale     │ ✅       │ ❌       │ ✅        │ ✅       │
│ Neon            │ ✅       │ ❌       │ ✅        │ ✅       │
│ Turso           │ ✅       │ ❌       │ ✅        │ ✅       │
└─────────────────┴──────────┴──────────┴──────────┴──────────┘
```

---

## Recommendations

### Solo Developer / Learning
1. **Supabase** - ครบจบในที่เดียว
2. **SQLite** - ถ้าไม่ต้องการ cloud

### Startup / MVP
1. **Supabase** - Free tier เยอะ
2. **PlanetScale** - ถ้าชอบ MySQL

### Production / Scale
1. **PostgreSQL** (managed)
2. **MongoDB Atlas** (ถ้า NoSQL)

### Edge / Global
1. **Turso** - SQLite at edge
2. **Neon** - PostgreSQL serverless
