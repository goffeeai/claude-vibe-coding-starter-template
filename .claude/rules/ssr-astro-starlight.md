# Astro + Starlight

## Overview
Astro = Web framework (static-first + SSR/SSG)
Starlight = Docs framework บน Astro สำหรับเว็บเอกสาร/คู่มือ (sidebar, toc, layout)

---

## Installation

```bash
# สร้างโปรเจค Astro ใหม่
npm create astro@latest

# เพิ่ม Starlight
npx astro add starlight
```

---

## Project Structure

```
my-docs/
├── astro.config.mjs      # Config หลัก
├── public/
│   ├── robots.txt
│   ├── og-default.png    # OG image default
│   └── llms.txt          # (Optional) สำหรับ AI
├── src/
│   ├── content/
│   │   └── docs/         # เนื้อหา Markdown
│   │       ├── getting-started/
│   │       ├── guides/
│   │       ├── troubleshooting/
│   │       └── reference/
│   ├── components/
│   │   └── SEO.astro     # SEO component
│   └── layouts/
└── package.json
```

---

## Configuration

### astro.config.mjs
```js
import { defineConfig } from "astro/config";
import starlight from "@astrojs/starlight";
import sitemap from "@astrojs/sitemap";

export default defineConfig({
  site: "https://example.com",  // สำคัญ! ใช้สร้าง canonical/sitemap
  integrations: [
    starlight({
      title: "My Docs",
      sidebar: [
        { label: "Getting Started", autogenerate: { directory: "getting-started" } },
        { label: "Guides", autogenerate: { directory: "guides" } },
        { label: "Troubleshooting", autogenerate: { directory: "troubleshooting" } },
        { label: "Reference", autogenerate: { directory: "reference" } },
      ],
    }),
    sitemap(),
  ],
});
```

---

## SEO Component

### src/components/SEO.astro
```astro
---
const {
  title,
  description,
  canonical,
  image,
  noindex = false,
  siteName = "My Docs",
  siteDescription = "คู่มือ/FAQ สำหรับ ...",
  lang = "th",
} = Astro.props;

const pageTitle = title ? `${title} | ${siteName}` : siteName;
const pageDescription = description ?? siteDescription;
const canonicalHref = canonical?.href ?? canonical;
const ogImage = image ?? "/og-default.png";
const robotsContent = noindex ? "noindex, nofollow" : "index, follow";
---

<title>{pageTitle}</title>
<meta name="description" content={pageDescription} />
<meta name="robots" content={robotsContent} />

{canonicalHref && <link rel="canonical" href={canonicalHref} />}

<!-- Open Graph -->
<meta property="og:type" content="article" />
<meta property="og:title" content={pageTitle} />
<meta property="og:description" content={pageDescription} />
<meta property="og:image" content={ogImage} />

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content={pageTitle} />
<meta name="twitter:description" content={pageDescription} />
<meta name="twitter:image" content={ogImage} />
```

### วิธีใช้ใน Layout
```astro
---
import SEO from "../components/SEO.astro";
---
<head>
  <SEO
    title="ทำ X ยังไง"
    description="สรุปคำตอบ 1-2 ประโยค..."
    canonical={Astro.url}
    image="/og/how-to-x.png"
  />
</head>
```

### กรณีหน้า "ยังไม่อยากให้ index"
```astro
<SEO
  title="Draft: หน้าเทส"
  description="หน้าเทส"
  canonical={Astro.url}
  noindex={true}
/>
```

---

## Sitemap

### ติดตั้ง
```bash
npm i @astrojs/sitemap
```

### เพิ่มใน config
```js
import sitemap from "@astrojs/sitemap";

export default defineConfig({
  site: "https://example.com",
  integrations: [sitemap()]
});
```

> sitemap จะ generate อัตโนมัติเมื่อ build

---

## robots.txt

### public/robots.txt
```txt
User-agent: *
Allow: /

Sitemap: https://example.com/sitemap-index.xml
```

---

## Schema JSON-LD

### เพิ่มใน Layout สำหรับหน้า FAQ
```astro
---
const faqSchema = {
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "คำถาม A คืออะไร?",
      "acceptedAnswer": { "@type": "Answer", "text": "คำตอบสั้นๆ ..." }
    }
  ]
};
---
<script type="application/ld+json" set:html={JSON.stringify(faqSchema)} />
```

### เพิ่มใน Layout สำหรับหน้า How-to
```astro
---
const howtoSchema = {
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "ติดตั้ง X ยังไง",
  "description": "สรุปสั้นๆของวิธีทำ",
  "step": [
    { "@type": "HowToStep", "name": "Step 1", "text": "ทำ ..." },
    { "@type": "HowToStep", "name": "Step 2", "text": "ทำ ..." }
  ]
};
---
<script type="application/ld+json" set:html={JSON.stringify(howtoSchema)} />
```

---

## Sidebar Configuration

### แนะนำโครงสร้าง
```js
sidebar: [
  {
    label: "Getting Started",
    items: [
      { label: "Overview", link: "/getting-started/" },
      { label: "Installation", link: "/getting-started/install/" },
    ],
  },
  {
    label: "Guides",
    autogenerate: { directory: "guides" },
  },
  {
    label: "Troubleshooting",
    autogenerate: { directory: "troubleshooting" },
  },
  {
    label: "Reference",
    items: [
      { label: "Glossary", link: "/reference/glossary/" },
      { label: "Parameters", link: "/reference/parameters/" },
    ],
  },
],
```

### ข้อกำหนดน้ำ
- หมวดหลักไม่เกิน 6
- ภายในหมวด บทไม่เกิน ~12 ต่อลุ่ม (ถ้าเกินให้แบ่ง group ย่อย)

---

## Frontmatter สำหรับ Markdown

```md
---
title: "ทำ X ยังไง"
description: "คำตอบสั้นๆ 1-2 ประโยค"
pubDate: 2026-01-18
updatedDate: 2026-01-18
---

เนื้อหา...
```

---

## llms.txt (Optional)

### public/llms.txt
```txt
# Site: My Knowledge Base
# Start here:
https://example.com/
https://example.com/getting-started/
https://example.com/guides/
https://example.com/troubleshooting/
https://example.com/reference/
https://example.com/reference/glossary/
```

> ช่วยให้ AI รู้ว่าควรเริ่มอ่านจากหน้าไหน

---

## Development Commands

```bash
# Dev server
npm run dev

# Build
npm run build

# Preview build
npm run preview
```

---

## Checklist ก่อน Deploy

- [ ] มี `SEO.astro` (title/meta/robots/canonical/OG/Twitter) และทุกหน้าใช้ผ่าน layout
- [ ] ตั้งค่า `site` ใน `astro.config.mjs` ให้ถูกต้อง (ใช้สร้าง canonical/sitemap)
- [ ] ติดตั้ง sitemap integration และ build แล้วเช็ค sitemap ถริง
- [ ] มี `public/robots.txt`
- [ ] มี OG image default (`public/og-default.png`)
- [ ] มี schema JSON-LD hook (เพิ่มได้ที่ layout ต่อบทิดหน้า)
- [ ] มี 404 page
- [ ] มี redirect policy (ถ้าเปลี่ยน slug ต้องทำ 301)

---

## Tips

1. **ใช้ Starlight built-in components**
   - `<Tabs>` สำหรับแสดงหลาย OS/วิธี
   - `<Card>` สำหรับ highlight
   - `<Aside>` สำหรับ note/warning

2. **Image optimization**
   - ใช้ `@astrojs/image` หรือ built-in image optimization
   - ใส่ `alt` ทุกรูป

3. **Performance**
   - Astro static build = เร็วมาก
   - หลีกเลี่ยง client-side JS ที่ไม่จำเป็น
