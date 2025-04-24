# 🔍 RAW HTML Processing Rules for DJ Maddox Gallery Pages

These rules define how structured data is generated from raw HTML on gallery pages.

---

## 📸 Image Extraction

**Use only the first two `<img>` tags** found inside:

```html
<div class="gllr_image_block">
  <img src="..." alt="..." />
</div>
```

- ✅ Extract exactly **two images**
- ✅ From each `<img>`:
  - `src` → used for the `image` array and `contentUrl` in `associatedMedia`
  - `alt` → used **verbatim** as the `caption` in `associatedMedia`
- ❌ Do not paraphrase or infer captions
- ❌ Do not extract from `<img>` outside `gllr_image_block`

---

## 📅 Event Date Extraction

Use the `article:published_time` `<meta>` tag from the page’s `<head>`:

```html
<meta property="article:published_time" content="YYYY-MM-DDTHH:MM:SS+00:00" />
```

- ✅ Extract only the `YYYY-MM-DD` part
- ✅ Use for both `startDate` and `endDate` in the JSON-LD `Event`
- ❌ Do not infer date from filename, gallery URL, or visible text

---

## 📌 Notes

- These extraction rules support strict validation of JSON-LD against Schema.org standards.
- Always combine extracted HTML data with a pre-approved JSON-LD template structure.