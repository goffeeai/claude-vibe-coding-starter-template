# Google Analytics & Tracking

## Overview
เครื่องมือวัดผลจาก Google - **ใช้ได้กับทุกเว็บ ทุก Framework**

---

## เครื่องมือหลัก

| เครื่องมือ | หน้าที่ | ต้องมี |
|-----------|--------|--------|
| **GA4** | วัดพฤติกรรมผู้ใช้ | ✅ ต้องมี |
| **GSC** | วัดผล SEO | ✅ ต้องมี |
| **GTM** | จัดการ Tags | แนะนำ |
| **Google Ads** | ลงโฆษณา | ถ้าทำ Ads |
| **Ads Pixels** | วัด Conversion จาก Ads | ถ้าทำ Ads |

---

## 1. Google Analytics 4 (GA4)

### วัดอะไรได้
- ผู้เข้าชม (Users, Sessions)
- แหล่งที่มา (Google, Facebook, Direct)
- พฤติกรรม (หน้าที่ดู, เวลาที่อยู่)
- Conversion (สมัคร, ซื้อของ)

### วิธีติดตั้ง (ใช้ได้ทุกเว็บ)

Copy โค้ดนี้ใส่ใน `<head>` ของทุกหน้า:

```html
<!-- GA4 - ใช้ได้กับทุกเว็บ ทุก Framework -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

> **หมายเหตุ:** เปลี่ยน `G-XXXXXXXXXX` เป็น Measurement ID ของคุณ (ได้จาก GA4 Admin → Data Streams)

### Track Custom Events

```javascript
// ปุ่มสมัคร
gtag('event', 'sign_up', { method: 'email' });

// ซื้อสินค้า
gtag('event', 'purchase', {
  transaction_id: 'T12345',
  value: 1500,
  currency: 'THB'
});

// กรอกฟอร์ม
gtag('event', 'form_submit', { form_name: 'contact' });

// ดาวน์โหลด
gtag('event', 'file_download', { file_name: 'brochure.pdf' });
```

---

## 2. Google Search Console (GSC)

### วัดอะไรได้
- Keywords ที่คนค้นหาเจอเว็บ
- อันดับในผลค้นหา (Position)
- จำนวนคลิก (Clicks)
- Index Status (หน้าไหนถูก index แล้ว)

### วิธี Setup (3 ขั้นตอน)

#### ขั้นตอน 1: เพิ่มเว็บ
```
1. ไปที่ https://search.google.com/search-console
2. Add Property
3. ใส่ URL เว็บ (เช่น https://example.com)
```

#### ขั้นตอน 2: Verify (เลือก 1 วิธี)

**วิธี A: HTML File (ง่ายที่สุด)**
```
1. Download file จาก GSC (ชื่อ googleXXXXXX.html)
2. Upload ไปที่ root ของเว็บ (โฟลเดอร์ public/)
3. ตรวจสอบว่าเข้าถึงได้ที่ https://example.com/googleXXXXXX.html
4. กด Verify
```

**วิธี B: HTML Meta Tag**
```html
<!-- ใส่ใน <head> -->
<meta name="google-site-verification" content="XXXXXXXXXX" />
```

**วิธี C: DNS TXT Record**
```
Type: TXT
Name: @
Value: google-site-verification=XXXXXXXXXX
```

#### ขั้นตอน 3: ส่ง Sitemap
```
1. ไปที่ GSC → Sitemaps (เมนูซ้าย)
2. ใส่ URL: sitemap.xml
3. กด Submit
```

> รอ 1-3 วัน ข้อมูลจะเริ่มเข้า

---

## 3. Google Tag Manager (GTM)

### ทำไมต้องใช้
- จัดการหลาย tags ในที่เดียว (GA4, Ads, Pixels)
- แก้ไข tags โดยไม่ต้องแก้โค้ด
- ทดสอบก่อน publish ได้

### วิธีติดตั้ง (ใช้ได้ทุกเว็บ)

**ส่วนที่ 1: ใส่ใน `<head>` (สูงสุด)**
```html
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-XXXXXXX');</script>
```

**ส่วนที่ 2: ใส่หลัง `<body>` เปิด**
```html
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
```

> **หมายเหตุ:** เปลี่ยน `GTM-XXXXXXX` เป็น Container ID ของคุณ

### DataLayer Events

```javascript
// ส่ง event ไป GTM
window.dataLayer = window.dataLayer || [];

dataLayer.push({
  event: 'form_submit',
  form_name: 'contact'
});

dataLayer.push({
  event: 'purchase',
  value: 1500
});
```

---

## 4. Google Ads Conversion (ถ้าใช้)

### Setup ผ่าน GTM
```
1. สร้าง Conversion ใน Google Ads
   Google Ads → Tools → Conversions → New

2. ติดตั้งใน GTM
   Tags → New → Google Ads Conversion Tracking
   ใส่ Conversion ID + Label
   เลือก Trigger (เช่น form_submit)

3. สร้าง Conversion Linker (สำคัญ!)
   Tags → New → Conversion Linker
   Trigger: All Pages
```

---

## 5. Ads Pixels (ถ้ายิงโฆษณา)

> **แนะนำ**: ติดตั้งผ่าน GTM จะง่ายกว่าติดโค้ดตรง

### Meta Pixel (Facebook/Instagram Ads)

**ติดตั้งตรง (ใส่ใน `<head>`):**
```html
<script>
!function(f,b,e,v,n,t,s)
{if(f.fbq)return;n=f.fbq=function(){n.callMethod?
n.callMethod.apply(n,arguments):n.queue.push(arguments)};
if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
n.queue=[];t=b.createElement(e);t.async=!0;
t.src=v;s=b.getElementsByTagName(e)[0];
s.parentNode.insertBefore(t,s)}(window, document,'script',
'https://connect.facebook.net/en_US/fbevents.js');
fbq('init', 'YOUR_PIXEL_ID');
fbq('track', 'PageView');
</script>
```

**Track Events:**
```javascript
// Lead
fbq('track', 'Lead');

// สมัครสมาชิก
fbq('track', 'CompleteRegistration');

// ซื้อของ
fbq('track', 'Purchase', {value: 1500, currency: 'THB'});
```

> **Pixel ID**: ได้จาก Meta Events Manager → Data Sources → Pixels

---

### TikTok Pixel

**ติดตั้งตรง (ใส่ใน `<head>`):**
```html
<script>
!function (w, d, t) {
  w.TiktokAnalyticsObject=t;var ttq=w[t]=w[t]||[];
  ttq.methods=["page","track","identify","instances","debug","on","off","once","ready","alias","group","enableCookie","disableCookie"];
  ttq.setAndDefer=function(t,e){t[e]=function(){t.push([e].concat(Array.prototype.slice.call(arguments,0)))}};
  for(var i=0;i<ttq.methods.length;i++)ttq.setAndDefer(ttq,ttq.methods[i]);
  ttq.instance=function(t){for(var e=ttq._i[t]||[],n=0;n<ttq.methods.length;n++)ttq.setAndDefer(e,ttq.methods[n]);return e};
  ttq.load=function(e,n){var i="https://analytics.tiktok.com/i18n/pixel/events.js";
  ttq._i=ttq._i||{};ttq._i[e]=[];ttq._i[e]._u=i;ttq._t=ttq._t||{};ttq._t[e]=+new Date;ttq._o=ttq._o||{};ttq._o[e]=n||{};
  var o=document.createElement("script");o.type="text/javascript";o.async=!0;o.src=i+"?sdkid="+e+"&lib="+t;
  var a=document.getElementsByTagName("script")[0];a.parentNode.insertBefore(o,a)};
  ttq.load('YOUR_PIXEL_ID');
  ttq.page();
}(window, document, 'ttq');
</script>
```

**Track Events:**
```javascript
// Lead
ttq.track('SubmitForm');

// สมัครสมาชิก
ttq.track('CompleteRegistration');

// ซื้อของ
ttq.track('CompletePayment', {value: 1500, currency: 'THB'});
```

> **Pixel ID**: ได้จาก TikTok Ads Manager → Assets → Events

---

### Line Tag

**ติดตั้งตรง (ใส่ใน `<head>`):**
```html
<script>
(function(g,d,o){
  g._ltq=g._ltq||[];g._lt=g._lt||function(){g._ltq.push(arguments)};
  var h=d.getElementsByTagName(o)[0];
  var s=d.createElement(o);s.async=1;
  s.src='https://d.line-scdn.net/n/line_tag/public/release/v1/lt.js';
  h.parentNode.insertBefore(s,h);
})(window,document,'script');
_lt('init', {
  customerType: 'lap',
  tagId: 'YOUR_TAG_ID'
});
_lt('send', 'pv', ['YOUR_TAG_ID']);
</script>
```

**Track Events:**
```javascript
// Conversion
_lt('send', 'cv', {
  type: 'Conversion'
}, ['YOUR_TAG_ID']);
```

> **Tag ID**: ได้จาก Line Ads Manager → Tracking → Line Tag

---

## Checklist ก่อน Launch

### GA4
- [ ] ติดตั้ง GA4 tag แล้ว
- [ ] ทดสอบด้วย GA4 DebugView (Realtime)
- [ ] ตั้งค่า Conversion events

### GSC
- [ ] Verify ownership แล้ว
- [ ] ส่ง sitemap แล้ว
- [ ] ไม่มี errors ใน Pages

### GTM (ถ้าใช้)
- [ ] ติดตั้ง GTM container แล้ว
- [ ] ทดสอบด้วย Preview mode
- [ ] Publish container แล้ว

### Ads Pixels (ถ้ายิงโฆษณา)
- [ ] Meta Pixel ติดตั้งแล้ว (ถ้าใช้ Facebook/IG Ads)
- [ ] TikTok Pixel ติดตั้งแล้ว (ถ้าใช้ TikTok Ads)
- [ ] Line Tag ติดตั้งแล้ว (ถ้าใช้ Line Ads)
- [ ] ทดสอบ events ทำงานถูกต้อง

---

## Debug Tools

| เครื่องมือ | ใช้ทำอะไร |
|-----------|-----------|
| **GA4 DebugView** | ดู events แบบ realtime |
| **GTM Preview** | ทดสอบ tags ก่อน publish |
| **Tag Assistant** | Chrome extension ตรวจ tags |
| **GSC URL Inspection** | ตรวจสอบ index status |
| **Meta Pixel Helper** | Chrome extension ตรวจ Meta Pixel |
| **TikTok Pixel Helper** | Chrome extension ตรวจ TikTok Pixel |

---

## Tips

1. **เริ่มจาก GA4 + GSC ก่อน** - 2 ตัวนี้ฟรีและจำเป็น
2. **ใช้ GTM ถ้ามีหลาย tags** - จัดการง่ายกว่า (รวม Ads Pixels ได้ด้วย)
3. **ดู GSC เป็นประจำ** - แก้ปัญหาก่อนกระทบ SEO
4. **ทดสอบก่อน publish** - ใช้ Preview/DebugView
5. **Ads Pixels ติดผ่าน GTM** - ไม่ต้องแก้โค้ดเว็บทุกครั้ง
