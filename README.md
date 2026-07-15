# raizintel-www

Public marketing site for **RaizIntel LLC** — a single hand-written static page.
No framework, no bundler, no build step. Just HTML, CSS, and static assets.

It exists to:

1. Give Apple Developer Program **org enrollment** a functional public website on
   the company's own domain (`raizintel.com`). Placeholders are refused.
2. Run a **waitlist** (hosted Tally form) that segments prospects by business type.

The site is **not** the product. RaizIntel RMS is the product.

## Files

```
index.html      the page
styles.css      styles (mobile-first, light/dark aware)
assets/         favicon.svg, favicon.ico, apple-touch-icon.png, og-image.png
robots.txt      allow all
sitemap.xml     single URL
```

## Editing the copy

All copy lives directly in `index.html` — edit the text between the tags. The
optional first-person line ("I'm a working private investigator myself…") can be
kept or removed.

## Before it goes fully live

### 1. Tally form ID  *(required — the form won't render until this is done)*

`index.html` ships with a placeholder. Search for **`PLACEHOLDER_TALLY_FORM_ID`**
(two places) and replace both with the real form ID.

1. Create the Tally form. Fields: **email**, **business segment** (solo operator /
   multi-investigator agency / process server / other), **optional name**,
   **optional agency name**. Nothing more.
2. Tally → **Integrations → Google Sheets**, authorize Google, pick/create the
   sheet. Responses land there — that's the point of the waitlist.
3. The form ID is the code in its share URL: `https://tally.so/r/<ID>`. Paste
   `<ID>` over both placeholders.

The free-tier "Made with Tally" badge stays — intentional, we're not paying to
remove it.

### 2. Hosting — Netlify (free tier)

Deploy from this repo. **No build command. Publish directory = repo root.**

### 3. Custom domain — external DNS only  ⚠️ READ THIS

The `raizintel.com` zone is authoritative at **Squarespace** and is load-bearing
(production `portal.`, `staging.`, `demo.`, Google Workspace mail, and Postmark
`mail.` which delivers MFA codes). **Do not move nameservers.**

- In Netlify, use the **external DNS** path. **Refuse** "Set up Netlify DNS" and
  any screen listing `*.nsone.net` nameservers — that delegates the whole zone
  away and takes production + mail + MFA down.
- Only two records are ever in scope, added at Squarespace by hand:
  - apex `@` → **A → 75.2.60.5**
  - `www` → **CNAME → <your-site>.netlify.app**
- Lower the TTL on those two records to ~300s **24–48h before** changing their
  values, so a bad cutover reverts in minutes. Touch nothing else in the zone.

## Contact

RaizIntel LLC · 2141 S. Mission St #1016 · Mount Pleasant, MI 48858 ·
admin@raizintel.com
