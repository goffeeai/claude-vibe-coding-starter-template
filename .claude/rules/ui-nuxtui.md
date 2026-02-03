# NuxtUI

## Overview
Official UI library for Nuxt.js

## Installation

```bash
npx nuxi@latest module add ui
```

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  modules: ['@nuxt/ui']
})
```

---

## Components

### Button
```vue
<UButton>Default</UButton>
<UButton color="primary">Primary</UButton>
<UButton color="red">Red</UButton>
<UButton variant="outline">Outline</UButton>
<UButton variant="ghost">Ghost</UButton>
<UButton size="sm">Small</UButton>
<UButton size="lg">Large</UButton>
<UButton loading>Loading</UButton>
```

### Input
```vue
<UInput v-model="value" placeholder="Enter text" />
<UInput type="email" icon="i-heroicons-envelope" />
<UInput :ui="{ icon: { trailing: { pointer: '' } } }">
  <template #trailing>
    <UButton color="gray" variant="link" icon="i-heroicons-x-mark" />
  </template>
</UInput>
```

### FormGroup
```vue
<UFormGroup label="Email" name="email" required>
  <UInput v-model="email" type="email" />
</UFormGroup>
```

### Card
```vue
<UCard>
  <template #header>
    <h3>Card Title</h3>
  </template>

  <p>Card content here.</p>

  <template #footer>
    <UButton>Action</UButton>
  </template>
</UCard>
```

### Modal
```vue
<script setup>
const isOpen = ref(false)
</script>

<UButton @click="isOpen = true">Open Modal</UButton>

<UModal v-model="isOpen">
  <UCard>
    <template #header>
      <h3>Modal Title</h3>
    </template>

    <p>Modal content.</p>

    <template #footer>
      <UButton @click="isOpen = false">Close</UButton>
    </template>
  </UCard>
</UModal>
```

### Table
```vue
<script setup>
const columns = [
  { key: 'name', label: 'Name' },
  { key: 'email', label: 'Email' }
]
const rows = [
  { name: 'John', email: 'john@example.com' },
  { name: 'Jane', email: 'jane@example.com' }
]
</script>

<UTable :columns="columns" :rows="rows" />
```

### Select
```vue
<script setup>
const options = ['Option 1', 'Option 2', 'Option 3']
const selected = ref(null)
</script>

<USelect v-model="selected" :options="options" placeholder="Select..." />
```

### Notification
```vue
<script setup>
const toast = useToast()

function showToast() {
  toast.add({
    title: 'Success!',
    description: 'Your action was successful.',
    color: 'green'
  })
}
</script>

<UButton @click="showToast">Show Toast</UButton>
```

### Dropdown
```vue
<script setup>
const items = [
  [{ label: 'Profile', icon: 'i-heroicons-user' }],
  [{ label: 'Settings', icon: 'i-heroicons-cog' }],
  [{ label: 'Logout', icon: 'i-heroicons-arrow-right-on-rectangle' }]
]
</script>

<UDropdown :items="items">
  <UButton>Menu</UButton>
</UDropdown>
```

---

## Dark Mode

```vue
<script setup>
const colorMode = useColorMode()
const isDark = computed(() => colorMode.value === 'dark')
</script>

<UButton @click="colorMode.preference = isDark ? 'light' : 'dark'">
  Toggle Dark Mode
</UButton>
```

---

## Configuration

```ts
// app.config.ts
export default defineAppConfig({
  ui: {
    primary: 'blue',
    gray: 'slate',
    button: {
      default: {
        size: 'md'
      }
    }
  }
})
```
