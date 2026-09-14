# Flortran — Systeme.io Landing Page

Host a new landing page for **any offer** on **Systeme.io** in under 5 minutes — matching your current Flortran branding (`#0E1A2B` / `#C49A2A` / `#FAF7F2`).

You have **2 files**:

| File | Purpose |
|------|---------|
| `flortran-systeme-landing.html` | **Main landing page** — universal, conversion-optimized. Paste into Systeme.io or host standalone. |
| `flortran-systeme-thankyou.html` | **Thank-you page** — set as funnel success step after form submit. |

Both are **100% self-contained** (no build, no npm). Open in a browser to preview; what you see is what Systeme.io will show.

---

## Option A — Host on Systeme.io (recommended, 5 steps)

### 1. Create the funnel
1. Systeme.io → **Funnels** → **Create funnel**
2. Choose goal: `Build an audience` or `Custom funnel`
3. Name it: e.g. `Flortran — Investor Audit Preview`

### 2. Create a funnel step
- Click **Create step** → Name: `Landing` → Type: **Funnel step** → Template: pick any (we will overwrite)
- Click **Edit page**

### 3. Paste the landing page
1. In the Systeme.io editor, drag a **Raw HTML** element onto the canvas (left sidebar → Elements → Raw HTML)
2. Stretch it to full width
3. Double-click it → **Edit code**
4. Open `flortran-systeme-landing.html` locally, copy **all** source (`Cmd+A → Cmd+C`) and paste into the Raw HTML code box
5. **Save**

> **Why Raw HTML?** Systeme.io's visual blocks can't reproduce Flortran's exact gold/navy styling without custom CSS. Raw HTML gives you pixel-perfect control and keeps your branding identical to `www.flortran.com`.

> **Alternative if Raw HTML is limited on your plan:** In the funnel step → **Settings → Tracking codes → Header code**, paste the `<style>` block, and in **Footer code** paste the `<body>` contents. Or host the file externally and link to it.

### 4. Connect your form (so leads go to Systeme.io)

Inside `flortran-systeme-landing.html`, find:

```html
<!-- ===== SYSTEME FORM START ===== -->
<div class="systeme-form-wrap">
  <!-- <script src="https://flortranadvisory.systeme.io/...js"></script> -->
  <form class="fallback-form">...</form>
</div>
<!-- ===== SYSTEME FORM END ===== -->
```

Replace the placeholder with your **real Systeme.io form script**:

1. Systeme.io → **Funnels → your funnel step → Edit page → Form** (or **Contacts → Forms**)
2. Create a form (fields: Name, Email, Role — or whatever you want)
3. Set **Action**: `Add tag` + `Send email` automation
4. Copy the **embed script**: `https://flortranadvisory.systeme.io/public/remote/page/XXXXXXXX.js`
5. Paste it inside `.systeme-form-wrap` — **delete the `<form class="fallback-form">`** once your script is in place.

The fallback form is only there so the page looks complete before you connect Systeme.io. Once pasted, submissions go to **Systeme.io → Contacts** automatically.

### 5. Set Thank-You page + domain

1. **Thank-You step**: Funnel → **Create step** → Name: `Thank You` → Paste `flortran-systeme-thankyou.html` into another Raw HTML element.
2. In the **Landing** step → **Automation rules** → **When form is submitted → Redirect to step: Thank You**
3. **Custom domain** (optional but recommended for trust):
   - Systeme.io → **Settings → Custom domains** → Add `go.flortran.com` or `landing.flortran.com`
   - Add the CNAME Systeme.io gives you at your DNS provider (where `www.flortran.com` is)
   - Assign the domain to your funnel in **Funnel settings → Domain**

You’re live at `https://go.flortran.com/investor-audit` (or your chosen path).

---

## Option B — Host standalone (no Systeme.io builder needed)

If you prefer to host on your current GitHub Pages (`www.flortran.com`):

```bash
cp systeme-landing/flortran-systeme-landing.html landing-offer.html
git add landing-offer.html
git commit -m "Add new offer landing"
git push origin main
```

Access at `https://www.flortran.com/landing-offer.html`. Leads still go to Systeme.io if you embedded the form script. This is useful for **ads that need a fast, custom URL** outside the funnel.

---

## How to create "another stuff" in 3 minutes

This template is built to be cloned. To launch a **second landing page** for a different offer:

1. Duplicate `flortran-systeme-landing.html` → `flortran-workshop.html`
2. Edit **5 spots** (marked `[A]`–`[E]` in the file header comment):
   - `[A]` Hero headline + subheadline
   - `[B]` Offer stack bullets + bonuses + values
   - `[C]` Benefits grid
   - `[D]` Systeme.io form script URL (create a new form if you want a different tag)
   - `[E]` Final CTA link
3. Create a new funnel step in Systeme.io and paste the new file.

**Presets included in comments** — search for `EDIT HEADLINE` and you’ll find examples for:
- Lead magnet (this default)
- Workshop/webinar
- Waitlist for new service

### Quick customizations
- **Logo**: Replace `src="https://www.flortran.com/flortran-logo-header.png"` with your Systeme.io file manager URL or keep absolute. If logo fails, fallback text `FLORTRAN` shows automatically.
- **Colors**: At top of `<style>`, change `--gold`, `--navy`, etc. — whole page updates.
- **Price**: Edit `.price-row` — change “Free” to `$490` or whatever; `Save $441` badge auto-hides if you remove it.
- **Urgency**: Change `Next slot closes Friday` or remove the `.urgency` div.
- **Proof bar**: Edit `.proof-bar` to add real customer logos (upload to Systeme.io → Files → copy URL).

---

## Systeme.io quirks — already handled

- **Sticky header**: Uses `position: sticky` (safe inside Systeme.io's wrapper). If Systeme.io adds extra padding, header stays visible without overlapping.
- **All CSS in one `<style>` tag** — no external stylesheet needed, won’t be stripped by Systeme.io.
- **No fixed heights** — works in Systeme.io’s responsive preview and on mobile.
- **Form fallback hidden automatically** when Systeme.io script loads (MutationObserver).
- **Fonts**: Loaded from Google Fonts; if blocked, falls back to system sans/serif — still on-brand.

---

## Preview locally

```bash
# from repo root
open systeme-landing/flortran-systeme-landing.html
open systeme-landing/flortran-systeme-thankyou.html
```

Or run a quick server:

```bash
python3 -m http.server 8000
# → http://localhost:8000/systeme-landing/flortran-systeme-landing.html
```

---

## Need a custom version?

Tell me the new offer name (e.g., “Valuation Accelerator”, “CFO Office Hours”, “Private Capital Workshop”) and I’ll pre-fill the headline, bullets, and automation copy for you — ready to paste.

— Built to match `index.html` / `services.html` / `free-resource.html` branding. `Finance. Advice. Transcend.`
