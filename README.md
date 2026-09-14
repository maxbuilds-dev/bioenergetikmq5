# bioenergetik-mq5.at

Single-page static website for Elke Bund — Bioenergetik / Mera Q5, Deutschlandsberg, Austria.
Plain HTML/CSS, no build step, deployed via GitHub Pages.

## Structure

- `index.html` — the single-page site (Hero, Über mich, Zwei Verfahren, Die MERA Q5, IMEDIS
  Bioresonanz, Anwendungsbereiche, Kontakt)
- `impressum.html`, `datenschutz.html` — legally required pages, linked from the footer
- `css/style.css` — all styling (design tokens at the top of the file)
- `assets/images/` — site photos (hero, portrait, device) and the favicon
- `.github/workflows/pages.yml` — deploys the repo root to GitHub Pages on every push to `main`

## Local preview

No build tools needed — serve the folder with any static file server, e.g.:

```
python3 -m http.server 8000
```

## Enabling GitHub Pages (one-time)

In the repo's **Settings → Pages**, set **Source** to **GitHub Actions**. The included workflow then
deploys automatically on every push to `main`.

## Open items before going live

- Confirm pricing: `index.html` currently shows "Preis auf Anfrage" for MERA Q5 and IMEDIS — replace
  with real prices if they should be public.
- Final read-through of all copy with Elke Bund, one more time end to end.
