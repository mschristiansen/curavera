# Cura Vera

One-page website for Vera von Hacht — psykoterapeut og sexolog, Multihuset Broager.

**Live:** https://curavera.dk

## Stack

Pure HTML, CSS, and a small inline `<script>` for the FAQ accordion. No framework, no build step. Fonts (Cormorant Garamond + Inter) load from Google Fonts.

## Files

- `index.html` — full markup
- `styles.css` — all styles; design tokens live in `:root`
- `vera-portrait-cropped.jpg`, `cura-vera-logo.png` — image assets
- `CNAME` — GitHub Pages custom domain (`curavera.dk`)

## Local preview

Open `index.html` in a browser, or serve the directory:

```sh
python3 -m http.server 8000
```

## Deployment

GitHub Pages serves the repo root from `main`. Pushing to `main` redeploys automatically; SSL is handled by Let's Encrypt via GitHub.
