# MongoDB

## Overview
NoSQL document database

## Installation

### Docker
```bash
docker run --name mongodb -p 27017:27017 -d mongo
```

### MongoDB Atlas (Cloud)
Free tier: https://www.mongodb.com/atlas

---

## Connection

### Connection String
```
mongodb://localhost:27017/mydb
mongodb+srv://user:pass@cluster.mongodb.net/mydb
```

### Node.js (mongoose)
```bash
npm install mongoose
```

```javascript
import mongoose from 'mongoose';

await mongoose.connect(process.env.MONGODB_URI);

// Define Schema
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, unique: true },
  age: Number,
  createdAt: { type: Date, default: Date.now }
});

const User = mongoose.model('User', userSchema);

// CRUD
const user = await User.create({ name: 'John', email: 'john@example.com' });
const users = await User.find();
const oneUser = await User.findById(id);
await User.findByIdAndUpdate(id, { name: 'Jane' });
await User.findByIdAndDelete(id);
```

---

## Schema Types

```javascript
{
  string: String,
  number: Number,
  boolean: Boolean,
  date: Date,
  array: [String],
  nested: {
    field: String
  },
  reference: { type: mongoose.Schema.Types.ObjectId, ref: 'OtherModel' }
}
```

---

## Queries

```javascript
// Find
await User.find({ age: { $gte: 18 } });
await User.find({ name: /john/i });
await User.find().limit(10).skip(20).sort({ createdAt: -1 });

// Aggregation
await User.aggregate([
  { $match: { age: { $gte: 18 } } },
  { $group: { _id: '$country', count: { $sum: 1 } } }
]);
```

---

## When to Use

### ✅ Good for
- Flexible schema
- Document storage
- Rapid development
- Scaling horizontally

### ⚠️ Consider SQL for
- Complex relations
- Transactions
- Data integrity
