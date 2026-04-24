# CMO Systems — cmosystems.co

Static marketing site for **CMO Systems** — Culture. Marketing. Operations. Matches the brand system in the April 2026 Offering Brief and PPT templates (pure black/white, condensed sans wordmark). Deploys the same way as `revfrictionscorecard.cmosystems.co` — GitHub → GitHub Pages → GoDaddy DNS.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole site (HTML + CSS + JS inline) |
| `logo-horizontal.png` | CMO Horizontal BOW — used in the nav |
| `logo-horizontal-inverse.png` | CMO Horizontal WOB — used in the dark footer |
| `logo-stacked.png` | CMO Stacked BOW — not used on-page, included for OG/sharing use if you want to swap |
| `CNAME` | Tells GitHub Pages to serve on `cmosystems.co` |
| `robots.txt` | Allows all crawlers, points at sitemap |
| `sitemap.xml` | Home + scorecard subdomain |
| `README.md` | This file |

No build step. No dependencies beyond Google Fonts (Oswald + Inter). Edit `index.html` and push.

## Copy source

All positioning, phase descriptions, deliverables, outcomes, and the target-client list come from **CMO Systems_Offering Brief_April2026.pdf**. If you revise the brief, update `index.html` to match — the copy is hand-written into the HTML, not pulled from a CMS.

## Brand system

| Element | Value |
|---|---|
| Primary | `#0B0B0B` (same as the deck background / wordmark) |
| Paper | `#FFFFFF` |
| Greys | `#2A2A2A` / `#545454` / `#8A8A8A` / `#C8C8C8` / `#E5E5E5` / `#F4F4F4` |
| Display font | Oswald (Google Fonts) — matches the condensed "SYSTEMS" wordmark |
| Body font | Inter (Google Fonts) |
| Rule weight | 2px solid black throughout (editorial / blueprint feel) |

All colors are defined as CSS variables at the top of the `<style>` block — change once, propagates everywhere.

## What to change before go-live

Search `index.html` for these values:

| Placeholder | Where | What to do |
|---|---|---|
| `#book-a-call` | 3 spots | Replace with your calendar URL (Calendly / SavvyCal / etc.) |
| `hello@cmosystems.co` | Nav CTA, CTA band, footer | Confirm — the April 2026 brief lists `hello.cmosystems@gmail.com`. Use whichever inbox you're monitoring. |
| `+1 (312) 489-1607` | Footer | From the brief — confirm this is still current |
| `linkedin.com/in/phillipryanblock` | Footer | Confirm this is the LinkedIn you want linked |
| `https://revfrictionscorecard.cmosystems.co` | Multiple | Already correct |

## Deploy: GitHub Pages → GoDaddy

Same pattern as the scorecard site.

### 1. Create the repo

```bash
cd /path/to/this/folder
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<your-username>/cmosystems-site.git
git push -u origin main
```

### 2. Turn on GitHub Pages

In the repo: **Settings → Pages**
- Source: **Deploy from a branch**
- Branch: **main** / folder: **/ (root)**
- Save. GitHub will read the `CNAME` file.

### 3. Point GoDaddy at GitHub Pages

GoDaddy → Domain Portfolio → `cmosystems.co` → DNS.

**Apex (`cmosystems.co`)** — four A records:

| Type | Name | Value            | TTL    |
|------|------|------------------|--------|
| A    | @    | 185.199.108.153  | 1 Hour |
| A    | @    | 185.199.109.153  | 1 Hour |
| A    | @    | 185.199.110.153  | 1 Hour |
| A    | @    | 185.199.111.153  | 1 Hour |

**`www` (optional):**

| Type  | Name | Value                        | TTL    |
|-------|------|------------------------------|--------|
| CNAME | www  | `<your-username>.github.io.` | 1 Hour |

Remove any old `A @` records first. Note: the `revfrictionscorecard` subdomain is a separate CNAME record already on this domain — don't touch it.

### 4. Enforce HTTPS

Back in GitHub → Settings → Pages. Once DNS propagates (10 min–few hours), tick **Enforce HTTPS**.

### 5. Verify

Open https://cmosystems.co in incognito. All CTAs should resolve:
- Scorecard links → `revfrictionscorecard.cmosystems.co`
- Email → `hello@cmosystems.co`
- Phone → `tel:` link on mobile

## Making edits later

Single HTML file — edit in any text editor, commit, push.

Common edits:
- **Hero headline**: search for `<h1>Align the system`
- **90-Day Program copy**: search for `id="program"` — each phase is a `<article class="phase">`
- **Deliverables**: three `<div class="deliverable">` blocks, one per phase
- **Outcomes grid**: search for `outcomes-grid`
- **Who this is for**: search for `who-list`
- **Colors**: `:root` block at top of `<style>` — edit once, propagates everywhere

## Notes

- Google Analytics 4 is wired up (Measurement ID `G-7Y8031VLY3`) — snippet is the first thing inside `<head>`. Verify traffic in Google Analytics → Reports → Realtime after the first live visit.
- Favicon is an inline SVG replica of the "CMO" block mark — no separate file needed.
- Open Graph preview image references `logo-horizontal.png` at the root — swap in a 1200×630 OG card for better social previews when you have one.
