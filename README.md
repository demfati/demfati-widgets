# Demfati Widget – Documentation

Zero-dependency drop-in JavaScript library that embeds **Demfati voting, ticket, and form widgets** into any website with:

- 🚀 Works with any stack (HTML, React, Vue, WordPress, etc.)
- ⚡ Lazy-loading support
- 🧩 Two lines of code to render widgets
- 🔒 Domain verification via meta tags
- 📱 Responsive, mobile-first design
- 🌍 Built-in i18n and currency formatting

---

## 📦 Installation

Add the domain verification meta tag inside `<head>`:

```html
<meta name="dmf-domain-verification" content="YOUR_SITE_TOKEN">
```

Then load the script:

```html
<script src="https://api.demfati.com/demfati-widget.js" defer></script>
```

---

## 🚀 Quick Start

```html
<!-- Voting widget -->
<div class="demfati-widget" data-type="voting" data-request="EVENT_CODE"></div>

<!-- Ticket store -->
<div class="demfati-widget" data-type="tickets" data-request="EVENT_CODE"></div>

<!-- Form plugin -->
<div class="demfati-widget" data-type="forms" data-request="FORM123"></div>
```

Optionally initialize with custom settings:

```js
document.addEventListener('DOMContentLoaded', () => {
  dmfwl.init({
    sort: 'votes',      // 'name' | 'code' | 'votes'
    search: true,       // enable search bar in voting widget
    customRenderContestant: (contestant, category, slug, isTop, percent) => {
      // return custom HTML string for each contestant
    }
  });
});
```

---

## 🔑 Domain Verification

Every domain must be verified with a token from the Demfati Dashboard.

| Attribute | Value |
|-----------|-------|
| name      | `dmf-domain-verification` |
| content   | Site token from Dashboard → Settings → Domains |

---

## 🧩 Available Widgets

### 1. Voting / Contest Gallery

```html
<div class="demfati-widget" data-type="voting" data-request="MISS_WORLD_2025"></div>
```

### 2. Ticket Store

```html
<div class="demfati-widget" data-type="tickets" data-request="TEDX_UNILAG"></div>
```

### 3. Forms

```html
<div class="demfati-widget" data-type="forms" data-request="FORM123"></div>
```

---

## ⚙️ Init Options

| Key                   | Type                        | Default   | Description |
|-----------------------|-----------------------------|-----------|-------------|
| `sort`                | `name - code - votes` | original  | Contestant sorting order |
| `search`              | `boolean`                   | true      | Toggle search bar in voting widget |
| `customRenderContestant` | `function`                | undefined | Custom contestant card renderer |

---

## 📚 API Reference

- `dmfwl.init(options?)` → Initializes widget loader
- `dmfwl.loadFromCache(key)` → Retrieve cached response (10 min TTL)
- `dmfwl.saveToCache(key, data)` → Store custom JSON into cache

---

## 💻 Framework Examples

### React (Next.js)

```tsx
useEffect(() => {
  import('https://api.demfati.com/demfati-widget.js').then(() => {
    dmfwl.init({ sort: 'votes' });
  });
}, []);
```

### Vue 3

```vue
<template>
  <div class="demfati-widget" data-type="voting" data-request="HACKATHON_2025"></div>
</template>

<script setup>
import { onMounted } from 'vue';

onMounted(() => {
  const script = document.createElement('script');
  script.src = 'https://api.demfati.com/demfati-widget.js';
  script.onload = () => dmfwl.init({ search: true });
  document.head.appendChild(script);
});
</script>
```

### WordPress

```html
<meta name="dmf-domain-verification" content="YOUR_TOKEN">
<script src="https://api.demfati.com/demfati-widget.js" defer></script>
<div class="demfati-widget" data-type="tickets" data-request="WORDCAMP_LAGOS"></div>
```

---

## 🎨 Styling & Theming

Widgets come with CSS variables for easy theming. Example:

```css
.dmf-ticket-header {
  background: linear-gradient(135deg, var(--primary), #ffffff);
}
.dmf-ticket-form .btn-primary {
  background: #7c3aed;
  box-shadow: 0 4px 14px rgba(124, 58, 237, .4);
}
```

---

## ❓ FAQ

**Widget not showing?**
- Ensure domain verification meta tag is present
- Confirm `data-request` is a valid event code
- Check browser console for errors

**Can I lazy-load the script?**
- Yes, it’s < 6kB gzipped and safe to load with `async`/`defer`

**Offline support?**
- Cached responses work online. Full Service Worker support coming soon.

---

## 📄 License

© 2025 Demfati – All rights reserved.
