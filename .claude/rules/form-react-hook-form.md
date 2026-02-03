# React Hook Form + Zod

## Overview
Form management + validation ที่ดีที่สุดสำหรับ React

## Installation
```bash
npm install react-hook-form zod @hookform/resolvers
```

## Basic Form

```tsx
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { z } from 'zod'

// Schema
const loginSchema = z.object({
  email: z.string().email('อีเมลไม่ถูกต้อง'),
  password: z.string().min(8, 'รหัสผ่านต้องมีอย่างน้อย 8 ตัวอักษร'),
})

type LoginForm = z.infer<typeof loginSchema>

// Component
function LoginForm() {
  const {
    register,
    handleSubmit,
    formState: { errors, isSubmitting },
  } = useForm<LoginForm>({
    resolver: zodResolver(loginSchema),
  })

  const onSubmit = async (data: LoginForm) => {
    console.log(data)
    // await login(data)
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <div>
        <input {...register('email')} placeholder="Email" />
        {errors.email && <p>{errors.email.message}</p>}
      </div>

      <div>
        <input {...register('password')} type="password" placeholder="Password" />
        {errors.password && <p>{errors.password.message}</p>}
      </div>

      <button type="submit" disabled={isSubmitting}>
        {isSubmitting ? 'Loading...' : 'Login'}
      </button>
    </form>
  )
}
```

## Zod Schema Examples

```typescript
import { z } from 'zod'

// User registration
const registerSchema = z.object({
  name: z.string().min(2, 'ชื่อต้องมีอย่างน้อย 2 ตัวอักษร'),
  email: z.string().email('อีเมลไม่ถูกต้อง'),
  password: z.string()
    .min(8, 'รหัสผ่านต้องมีอย่างน้อย 8 ตัวอักษร')
    .regex(/[A-Z]/, 'ต้องมีตัวพิมพ์ใหญ่อย่างน้อย 1 ตัว')
    .regex(/[0-9]/, 'ต้องมีตัวเลขอย่างน้อย 1 ตัว'),
  confirmPassword: z.string(),
  age: z.number().min(18, 'ต้องอายุ 18 ปีขึ้นไป'),
  phone: z.string().regex(/^0[0-9]{9}$/, 'เบอร์โทรไม่ถูกต้อง'),
}).refine((data) => data.password === data.confirmPassword, {
  message: 'รหัสผ่านไม่ตรงกัน',
  path: ['confirmPassword'],
})

// Product
const productSchema = z.object({
  name: z.string().min(1, 'กรุณากรอกชื่อสินค้า'),
  price: z.number().positive('ราคาต้องมากกว่า 0'),
  quantity: z.number().int().min(0),
  category: z.enum(['electronics', 'clothing', 'food']),
  tags: z.array(z.string()).optional(),
  isActive: z.boolean().default(true),
})

// Optional fields
const profileSchema = z.object({
  bio: z.string().optional(),
  website: z.string().url().optional().or(z.literal('')),
  avatar: z.string().url().nullable(),
})
```

## With shadcn/ui

```tsx
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { z } from 'zod'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import {
  Form,
  FormControl,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from '@/components/ui/form'

const schema = z.object({
  username: z.string().min(2),
  email: z.string().email(),
})

function MyForm() {
  const form = useForm<z.infer<typeof schema>>({
    resolver: zodResolver(schema),
    defaultValues: {
      username: '',
      email: '',
    },
  })

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)}>
        <FormField
          control={form.control}
          name="username"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Username</FormLabel>
              <FormControl>
                <Input placeholder="username" {...field} />
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />
        <Button type="submit">Submit</Button>
      </form>
    </Form>
  )
}
```

## Dynamic Fields (useFieldArray)

```tsx
import { useForm, useFieldArray } from 'react-hook-form'

const schema = z.object({
  items: z.array(z.object({
    name: z.string().min(1),
    quantity: z.number().min(1),
  })),
})

function OrderForm() {
  const { control, register, handleSubmit } = useForm({
    resolver: zodResolver(schema),
    defaultValues: {
      items: [{ name: '', quantity: 1 }],
    },
  })

  const { fields, append, remove } = useFieldArray({
    control,
    name: 'items',
  })

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      {fields.map((field, index) => (
        <div key={field.id}>
          <input {...register(`items.${index}.name`)} />
          <input {...register(`items.${index}.quantity`, { valueAsNumber: true })} type="number" />
          <button type="button" onClick={() => remove(index)}>Remove</button>
        </div>
      ))}
      <button type="button" onClick={() => append({ name: '', quantity: 1 })}>
        Add Item
      </button>
      <button type="submit">Submit</button>
    </form>
  )
}
```

## Form State

```tsx
const {
  formState: {
    errors,           // Validation errors
    isSubmitting,     // Form is submitting
    isValid,          // Form is valid
    isDirty,          // Form has been modified
    dirtyFields,      // Which fields are dirty
    touchedFields,    // Which fields are touched
  },
  reset,              // Reset form
  setValue,           // Set single value
  getValues,          // Get all values
  watch,              // Watch value changes
} = useForm()
```

## Project Structure

```
src/
├── schemas/
│   ├── auth.ts        # Login, Register schemas
│   ├── user.ts        # User profile schemas
│   └── product.ts     # Product schemas
├── components/
│   └── forms/
│       ├── LoginForm.tsx
│       ├── RegisterForm.tsx
│       └── ProductForm.tsx
```

## Best Practices

1. **แยก schema ออกมา** - Reuse ได้ทั้ง frontend และ API validation
2. **ใช้ zodResolver** - Type-safe validation
3. **Handle loading state** - Disable button ขณะ submit
4. **แสดง error ชัดเจน** - ใช้ FormMessage

## Links
- [React Hook Form](https://react-hook-form.com/)
- [Zod](https://zod.dev/)
- [shadcn/ui Form](https://ui.shadcn.com/docs/components/form)
