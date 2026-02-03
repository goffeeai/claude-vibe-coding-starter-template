# Vuetify

## Overview
Vue Component Library ที่ใช้ Material Design จาก Google

---

## Installation

### Nuxt 3
```bash
npm install vuetify @mdi/font
```

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  modules: ['vuetify-nuxt-module'],
  vuetify: {
    moduleOptions: {
      /* module options */
    },
    vuetifyOptions: {
      /* vuetify options */
    },
  },
});
```

```bash
# หรือใช้ module
npm install -D vuetify-nuxt-module
```

### Vue 3
```bash
npm install vuetify
```

```ts
// main.ts
import { createApp } from 'vue';
import { createVuetify } from 'vuetify';
import 'vuetify/styles';
import '@mdi/font/css/materialdesignicons.css';

const vuetify = createVuetify();
const app = createApp(App);
app.use(vuetify);
app.mount('#app');
```

---

## Theme Customization

```ts
// plugins/vuetify.ts
import { createVuetify } from 'vuetify';

export default createVuetify({
  theme: {
    defaultTheme: 'light',
    themes: {
      light: {
        colors: {
          primary: '#1976D2',
          secondary: '#424242',
          accent: '#82B1FF',
          error: '#FF5252',
          info: '#2196F3',
          success: '#4CAF50',
          warning: '#FFC107',
        },
      },
      dark: {
        colors: {
          primary: '#2196F3',
          secondary: '#424242',
        },
      },
    },
  },
});
```

---

## Common Components

### Button
```vue
<template>
  <v-btn color="primary">Primary</v-btn>
  <v-btn variant="outlined">Outlined</v-btn>
  <v-btn variant="text">Text</v-btn>
  <v-btn color="secondary">Secondary</v-btn>
  <v-btn disabled>Disabled</v-btn>
  <v-btn prepend-icon="mdi-content-save">Save</v-btn>
</template>
```

### Text Field
```vue
<template>
  <v-text-field label="Name" variant="outlined" />
  <v-text-field label="Email" variant="filled" />
  <v-text-field label="Password" type="password" />
  <v-text-field label="Error" error :error-messages="['Invalid input']" />
  <v-textarea label="Multiline" rows="4" />
</template>
```

### Card
```vue
<template>
  <v-card>
    <v-card-title>Card Title</v-card-title>
    <v-card-text>
      Card content goes here.
    </v-card-text>
    <v-card-actions>
      <v-btn variant="text">Learn More</v-btn>
    </v-card-actions>
  </v-card>
</template>
```

### App Bar & Navigation
```vue
<template>
  <v-app-bar>
    <v-app-bar-nav-icon @click="drawer = !drawer" />
    <v-app-bar-title>App Name</v-app-bar-title>
    <v-spacer />
    <v-btn variant="text">Login</v-btn>
  </v-app-bar>

  <v-navigation-drawer v-model="drawer">
    <v-list>
      <v-list-item
        v-for="item in items"
        :key="item.title"
        :prepend-icon="item.icon"
        :title="item.title"
        :to="item.to"
      />
    </v-list>
  </v-navigation-drawer>
</template>
```

---

## Layout

### Grid System
```vue
<template>
  <v-container>
    <v-row>
      <v-col cols="12" md="6">
        Column 1
      </v-col>
      <v-col cols="12" md="6">
        Column 2
      </v-col>
    </v-row>
  </v-container>
</template>
```

### Breakpoints
| Name | Range |
|------|-------|
| xs | < 600px |
| sm | 600px - 960px |
| md | 960px - 1280px |
| lg | 1280px - 1920px |
| xl | > 1920px |

---

## Icons (MDI)

```vue
<template>
  <v-icon>mdi-home</v-icon>
  <v-icon color="primary">mdi-account</v-icon>
  <v-icon size="large">mdi-email</v-icon>
  <v-icon color="error">mdi-delete</v-icon>
</template>
```

หา icon ได้ที่: https://pictogrammers.com/library/mdi/

---

## Form Validation

```vue
<template>
  <v-form v-model="valid" @submit.prevent="submit">
    <v-text-field
      v-model="email"
      label="Email"
      :rules="emailRules"
      required
    />
    <v-text-field
      v-model="password"
      label="Password"
      type="password"
      :rules="passwordRules"
      required
    />
    <v-btn type="submit" :disabled="!valid">Submit</v-btn>
  </v-form>
</template>

<script setup>
const valid = ref(false);
const email = ref('');
const password = ref('');

const emailRules = [
  v => !!v || 'Email is required',
  v => /.+@.+\..+/.test(v) || 'Email must be valid',
];

const passwordRules = [
  v => !!v || 'Password is required',
  v => v.length >= 8 || 'Password must be at least 8 characters',
];
</script>
```

---

## Data Table

```vue
<template>
  <v-data-table
    :headers="headers"
    :items="items"
    :items-per-page="10"
  >
    <template #item.actions="{ item }">
      <v-btn icon="mdi-pencil" size="small" @click="edit(item)" />
      <v-btn icon="mdi-delete" size="small" color="error" @click="remove(item)" />
    </template>
  </v-data-table>
</template>

<script setup>
const headers = [
  { title: 'Name', key: 'name' },
  { title: 'Email', key: 'email' },
  { title: 'Actions', key: 'actions', sortable: false },
];

const items = ref([
  { name: 'John', email: 'john@example.com' },
  { name: 'Jane', email: 'jane@example.com' },
]);
</script>
```

---

## Dialog

```vue
<template>
  <v-btn @click="dialog = true">Open Dialog</v-btn>

  <v-dialog v-model="dialog" max-width="500">
    <v-card>
      <v-card-title>Dialog Title</v-card-title>
      <v-card-text>
        Dialog content here.
      </v-card-text>
      <v-card-actions>
        <v-spacer />
        <v-btn variant="text" @click="dialog = false">Cancel</v-btn>
        <v-btn color="primary" @click="confirm">Confirm</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script setup>
const dialog = ref(false);
</script>
```

---

## Dark Mode Toggle

```vue
<template>
  <v-btn
    :icon="isDark ? 'mdi-weather-sunny' : 'mdi-weather-night'"
    @click="toggleTheme"
  />
</template>

<script setup>
import { useTheme } from 'vuetify';

const theme = useTheme();
const isDark = computed(() => theme.global.current.value.dark);

function toggleTheme() {
  theme.global.name.value = isDark.value ? 'light' : 'dark';
}
</script>
```

---

## Best Practices

### 1. ใช้ v-container สำหรับ layout
```vue
<!-- ✅ Good -->
<v-container>
  <v-row>
    <v-col>Content</v-col>
  </v-row>
</v-container>

<!-- ❌ Bad -->
<div class="container">
  <div class="row">Content</div>
</div>
```

### 2. ใช้ props แทน class
```vue
<!-- ✅ Good -->
<v-btn color="primary" size="large" rounded>Button</v-btn>

<!-- ❌ Bad -->
<v-btn class="bg-primary large rounded">Button</v-btn>
```

### 3. ใช้ v-spacer สำหรับ flex spacing
```vue
<!-- ✅ Good -->
<v-app-bar>
  <v-app-bar-title>Title</v-app-bar-title>
  <v-spacer />
  <v-btn>Action</v-btn>
</v-app-bar>
```

---

## Resources

- Docs: https://vuetifyjs.com/
- Components: https://vuetifyjs.com/en/components/all/
- Icons (MDI): https://pictogrammers.com/library/mdi/
