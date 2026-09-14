# FIX: "The code is not valid" in Systeme.io

You saw this because **Systeme.io strictly forbids** these tags inside the **Raw HTML element** (Help Article 306):

❌ `<html>` `</html>`  ❌ `<head>` `</head>`  ❌ `<body>` `</body>`  ❌ `<footer>` `</footer>`

Your previous file was a **full HTML document** (`<!DOCTYPE html><html><head>...<body>...`). When pasted into Raw HTML, Systeme rejects it.

Also forbidden inside Raw HTML: `<style>`, `<script>`, `<link>` — they must go in **Settings → Header / Footer**.

## Solution: Split into 3 places (30 seconds)

We have prepared 3 ready-to-paste files in `systeme-landing/`:

### 1️⃣ HEADER → Paste into `Settings → Header`
File: **`HEADER-1-paste-in-Settings-Header.html`**
- Contains Google Fonts `<link>` + your `<style>` (all CSS)
- In editor: Click **Settings** (top left) → scroll to **Tracking codes → Header** → paste → **Save**

### 2️⃣ RAW HTML → Paste into the page
File: **`RAW-2-paste-in-Raw-HTML-element.html`**
- Contains **ONLY** the page HTML (`<div>` blocks)
- **No** `<html>`, `<body>`, `<footer>`, `<style>`, `<script>`, `<link>`
- In editor: Drag **Raw HTML** onto page → **Edit code** → paste this file → **Save**
- Replace the placeholder form: find `SYSTEME FORM START` and replace the fallback `<form>` with your real embed:
  ```html
  <script src="https://flortranadvisory.systeme.io/public/remote/page/YOUR_ID.js"></script>
  ```
  (That `<script>` must go via Header/Footer OR keep it in Raw HTML after saving — test copy. If it still rejects, put the script in **Settings → Footer**.)

### 3️⃣ FOOTER → Paste into `Settings → Footer`
File: **`FOOTER-3-paste-in-Settings-Footer.html`**
- Contains `<script>` for form handling (toast + validation)
- In editor: **Settings → Tracking codes → Footer** → paste → **Save**

---

### Alternative: Single combined file
`flortran-valuation-toolkit-SYSTEME-SPLIT.html` contains all 3 parts with labels. Copy each labeled block to its place.

### Quick test
After pasting, click **Save**, then **View** (live page) — Raw HTML does NOT show in Preview, only on live page (per Systeme docs).

### Still shows "Code is not valid"?
- Make sure you did **not** paste the full `flortran-valuation-toolkit.html` (with `<!DOCTYPE>`) into Raw HTML.
- Make sure Raw HTML file does **not** contain `<style>` or `<footer>` tags.
- Try pasting **only** `RAW-2...` first, save, then add Header/Footer separately.

Full standalone page (for direct hosting at `www.flortran.com`) is still `flortran-valuation-toolkit.html`.
