# bioenergetik-mq5.at

Single-page static website for Elke Bund — Bioenergetik / Mera Q5, Deutschlandsberg (Trahütten), Austria.
Plain HTML/CSS, no build step, deployed via GitHub Pages.

## Structure

- `index.html` — the single-page site (Hero, Über mich, Die MERA Q5, Anwendungsbereiche, Kontakt)
- `impressum.html`, `datenschutz.html` — legally required pages, linked from the footer
- `css/style.css` — all styling (design tokens at the top of the file)
- `assets/images/` — placeholder graphics for the hero, portrait and device photos
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

- Replace the three placeholder images in `assets/images/` (hero, portrait, device) with real photos.
- Final review of all copy, section by section, with Elke Bund — especially the "Über mich" bio text,
  which is currently a placeholder.
- Fill in the missing legal details in `impressum.html` (Gewerbeberechtigung, Kammer-Mitgliedschaft,
  UID-Nummer if applicable).
- Confirm pricing: `index.html` currently shows "Preis auf Anfrage" for the single session — replace
  with a real price if it should be public.
- Re-check all health-adjacent wording against what a non-medical practitioner may legally claim in
  Austria before publishing.
