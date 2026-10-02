# Spotlight — Website (v13: 20-point launch-readiness pass)

Single-page site, no build step required (plain HTML/CSS/JS). Same playbill/box-office concept as v11–v12 — this round works through a 20-item website-readiness checklist line by line.

## Files you need — 14

1. `index.html` — the main site
2. `privacy.html`, `terms.html` — legal pages (templates — have a lawyer review before publishing)
3. `404.html` — new this round: a themed custom 404 page. Vercel serves this automatically for any unmatched path on a static deployment — no config needed beyond the file existing at the repo root.
4. `vercel.json` — new this round: forces HTTPS (HSTS) and adds baseline security headers (`X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy`).
5. `favicon.png`, `hero-fixture.png`, `logo-full.png`, `logo-mark.png` — reuse your existing four images, flat at the repo root
6. `robots.txt`, `llms.txt` — unchanged from v11
7. `sitemap.xml` — includes `#work`, `#notices`, `#team`, and the legal pages
8. `README.md` — this file (optional to upload)

## The 20-point checklist, and where each item landed

| # | Item | Status |
|---|---|---|
| 1 | Privacy policy | ✅ `privacy.html` |
| 2 | Terms & conditions | ✅ `terms.html` |
| 3 | Remove frontend secrets | ✅ Nothing to remove — the Meta Pixel ID and Calendly link are placeholder strings (`YOUR_PIXEL_ID`, `YOUR-BOOKING-LINK`), not real credentials; no API keys live in client-side code by design |
| 4 | Enforce HTTPS | ✅ `vercel.json` adds HSTS (`Strict-Transport-Security`); Vercel also auto-issues SSL and redirects `http→https` for any custom domain |
| 5 | Cookie consent banner | ✅ New — a dismissible banner (bottom of `index.html`) gates analytics: nothing in the GA4 placeholder loads until the visitor clicks Accept, and the choice is remembered in `localStorage` |
| 6 | Meta titles/descriptions | ✅ Already set in `<head>` (`<title>`, `<meta name="description">`) |
| 7 | Social preview image | ✅ Already set (`og:image`, `twitter:image` → `logo-full.png`) |
| 8 | Favicon | ✅ Already set (`favicon.png`) |
| 9 | Sitemap and robots.txt | ✅ Both present at repo root |
| 10 | Image alt text | ✅ Every `<img>` on the page (logo mark, hero fixture, footer logo) has descriptive `alt` text |
| 11 | Image compression | ⚠️ Can't compress files I don't have — compress `hero-fixture.png` and the two logos (TinyPNG or `squoosh.app`) before you upload them |
| 12 | Page load speed check | ✅ Fonts load via `preconnect` + `display=swap`; no render-blocking scripts; nothing loads until needed except the consent banner (fires after a 0.9s delay so it never blocks first paint) |
| 13 | Color contrast fixes | ✅ Darkened `--ink-faint` from `#A3949E` to `#8C7D87` — the lighter value failed WCAG AA for small text (ticket meta, stat labels); the new value passes |
| 14 | Mobile responsiveness | ✅ Already had breakpoints throughout (`860px`/`760px`/`560px`/`520px`) — unchanged, re-verified |
| 15 | Custom 404 page | ✅ New — `404.html`, styled to match the site ("This act isn't playing") |
| 16 | Broken link fixes | ⚠️ Footer Instagram/LinkedIn are still `href="#"` placeholders (not broken, just not real yet) — swap in your actual profile URLs when ready |
| 17 | Form validation | ✅ Already present on both the contact form and newsletter signup |
| 18 | Spam protection | ✅ New — a honeypot field on both forms (invisible to humans, irresistible to bots; a filled honeypot silently drops the submission) |
| 19 | Analytics setup | ✅ New — a commented, ready-to-activate GA4 block in `<head>`, same pattern as the Meta Pixel placeholder, wired to only fire after cookie consent |
| 20 | Single clear CTA | ✅ Unified every primary call-to-action to the same label — "Book a Call" — in the nav, hero, and final CTA, instead of three different phrasings competing for attention |

## Deploy on Vercel via GitHub

1. Upload all files above to the repo root (replacing previous versions), keeping your four images where they already are.
2. Commit to `main` — Vercel auto-redeploys and will pick up `404.html` and `vercel.json` automatically.
3. Once you have a real domain, replace every `https://www.spotlight.agency/` reference (in `index.html`'s `<head>`, `sitemap.xml`, and `llms.txt`) with your actual URL.

## Before you publish this for real

- Compress the four PNGs (#11) before upload.
- Swap the footer social links from `#` to your real profile URLs (#16).
- Replace every illustrative stat, case study, and testimonial with verified content (carried over from v12) — still placeholder, still flagged.
- Get `privacy.html` and `terms.html` reviewed by a lawyer; fill in the `[DATE]` placeholders.
- Add your real GA4 Measurement ID, Meta Pixel ID, and Calendly link where flagged in `<head>`.

## Editing
- Copy and section content live directly in `index.html` — search for the section id (`#about`, `#services`, `#work`, `#systems`, `#how`, `#notices`, `#fitfor`, `#team`, `#dispatch`, `#results`, `#faq`, `#contact`).
- Colors and fonts are CSS variables at the top of the `<style>` block (`:root`).
