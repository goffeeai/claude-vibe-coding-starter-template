# Supabase

## Overview
Open source Firebase alternative with PostgreSQL

## Setup

1. Create project at https://supabase.com
2. Get API URL and anon key from Settings > API

---

## Installation

```bash
npm install @supabase/supabase-js
```

```javascript
import { createClient } from '@supabase/supabase-js';

const supabase = createClient(
  process.env.SUPABASE_URL,
  process.env.SUPABASE_ANON_KEY
);
```

---

## Database (CRUD)

```javascript
// Create
const { data, error } = await supabase
  .from('users')
  .insert({ name: 'John', email: 'john@example.com' })
  .select();

// Read
const { data } = await supabase
  .from('users')
  .select('*');

const { data } = await supabase
  .from('users')
  .select('*')
  .eq('id', 1)
  .single();

// Update
const { data } = await supabase
  .from('users')
  .update({ name: 'Jane' })
  .eq('id', 1)
  .select();

// Delete
const { error } = await supabase
  .from('users')
  .delete()
  .eq('id', 1);
```

---

## Authentication

```javascript
// Sign up
const { data, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password123'
});

// Sign in
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'password123'
});

// Sign out
await supabase.auth.signOut();

// Get user
const { data: { user } } = await supabase.auth.getUser();
```

---

## Storage

```javascript
// Upload
const { data, error } = await supabase.storage
  .from('avatars')
  .upload('user-1.png', file);

// Get public URL
const { data } = supabase.storage
  .from('avatars')
  .getPublicUrl('user-1.png');

// Delete
await supabase.storage
  .from('avatars')
  .remove(['user-1.png']);
```

---

## Real-time

```javascript
const channel = supabase
  .channel('messages')
  .on('postgres_changes',
    { event: 'INSERT', schema: 'public', table: 'messages' },
    (payload) => console.log('New message:', payload.new)
  )
  .subscribe();

// Unsubscribe
supabase.removeChannel(channel);
```

---

## Row Level Security (RLS)

```sql
-- Enable RLS
ALTER TABLE users ENABLE ROW LEVEL SECURITY;

-- Policy: Users can only see their own data
CREATE POLICY "Users can view own data" ON users
  FOR SELECT USING (auth.uid() = user_id);
```

---

## Why Supabase?

- PostgreSQL (full SQL)
- Built-in Auth
- Real-time subscriptions
- Storage
- Edge Functions
- Free tier available
