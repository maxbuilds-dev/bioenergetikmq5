# bioenergetik-mq5.at

Single-page static website for Elke Bund — Bioenergetik / Mera Q5, Deutschlandsberg, Austria.
Plain HTML/CSS/JS, no build step, deployed via GitHub Pages.

## Structure

- `index.html` — the single-page site (Hero, Über mich, Zwei Verfahren, Die MERA Q5, IMEDIS
  Bioresonanz, Anwendungsbereiche, Kontakt)
- `impressum.html`, `datenschutz.html` — legally required pages, linked from the footer
- `404.html`, `robots.txt`, `sitemap.xml` — site hygiene, at the repo root
- `css/style.css` — all styling (design tokens at the top of the file)
- `css/fonts.css` — self-hosted `@font-face` rules (see Security below)
- `js/script.js` — cookie consent manager, consent-gated Google Maps embed, email
  de-obfuscation. No other JavaScript on the site.
- `assets/images/` — site photos (hero, portrait, device) and the favicon
- `assets/fonts/` — self-hosted Cormorant Garamond and Work Sans (`.woff2`)

## Security & cookies

The security baseline (CSP, cookie consent, consent-gated embeds) was ported from
`maxbuilds-dev/webpage-base` and adapted to this site's single Google Maps embed:

- **Content-Security-Policy** meta tag on every page (`default-src 'none'`, only
  same-origin scripts/styles/fonts/images; `frame-src` allows Google only on
  `index.html`, only for the consent-gated Maps embed). No inline `style="..."` or
  `<script>` blocks anywhere — CSP silently blocks both.
- **Cookie consent manager** (`js/script.js`): a `zustimmung` cookie (1 year,
  `SameSite=Lax`) stores the visitor's choice. Three equally-weighted buttons
  (Einstellungen / Alle ablehnen / Alle akzeptieren), per-category opt-in, Escape
  counts as refusal, consent is revisitable via the footer "Cookie-Einstellungen"
  button. Bump `CC_VERSION` in `js/script.js` if the category list ever changes.
- **Google Maps is blocked until consent**: the iframe doesn't exist in the HTML at
  all; `js/script.js` creates it only after the "Google Maps" category is granted.
  Before that, only a placeholder with a "Karte laden" button is shown.
- **Fonts are self-hosted** (`assets/fonts/`, wired up in `css/fonts.css`), never
  loaded from the Google Fonts CDN — that would leak every visitor's IP to Google
  before any consent step.
- **Email de-obfuscation**: the Kontakt section's mailto link is assembled by
  `js/script.js` from `data-mail`/`data-domain` attributes so it doesn't sit in the
  page source as plain text for scrapers. The Impressum's address stays in plain
  text on purpose — ECG § 5 requires immediate reachability there.
- **`datenschutz.html`** documents all of the above (the exact cookie, the Maps
  consent flow, self-hosted fonts) — keep it in sync if any of this changes.

## Local preview

No build tools needed — serve the folder with any static file server, e.g.:

```
python3 -m http.server 8000
```

## GitHub Pages

Pages is already deploying straight from this branch on every push (Settings →
Pages → Source is set to **Deploy from a branch**, not GitHub Actions) — no PR
merge is needed to see changes live. `.github/workflows/pages.yml` deploys on
push to `main` as a fallback once this branch is merged there; until then it
never runs, since `main` has no site files on it yet.

## Open items before going live

- Confirm pricing: `index.html` currently shows "Preis auf Anfrage" for MERA Q5 and IMEDIS — replace
  with real prices if they should be public.
- Final read-through of all copy with Elke Bund, one more time end to end.
- Point `robots.txt` / `sitemap.xml` / the Impressum's domain references at the final
  live domain if it ends up different from `bioenergetik-mq5.at`.
