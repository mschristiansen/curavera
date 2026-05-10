# Cura Vera — agent notes

One-page Danish-language site for a psychotherapist (Vera von Hacht). See `README.md` for the public-facing summary.

## What this codebase is

Static site, no framework, no build step. Three meaningful files: `index.html`, `styles.css`, and the inline `<script>` at the bottom of `index.html` (FAQ accordion + footer year). Two image assets. That's the whole thing — keep it that way unless there's a strong reason otherwise.

## Origin

Originally a React + Babel-in-the-browser prototype exported from Claude Design (claude.ai/design). The runtime React/Babel was stripped during implementation because the site is fundamentally static and the only interactivity (FAQ open/close) is ~10 lines of vanilla JS. Don't reintroduce React.

## Design system

All tokens live in `:root` in `styles.css`. The active palette is **Salvie & terracotta** — the prototype originally supported four palettes (Guld, Salvie, Ler, Skov) but only Salvie shipped. If the owner wants a palette change, swap the `:root` values; don't reintroduce a runtime switcher.

Fonts: Cormorant Garamond (display serif) + Inter (body sans), loaded from Google Fonts. Don't self-host without checking with the owner.

## Content notes

- Content is Danish. Some bilingual messaging (Dansk · Deutsch) appears in copy but the page itself is Danish-only.
- Previous edits explicitly removed mentions of "coaching" and "hesteassisteret arbejde" — don't reintroduce those terms.
- Section numbering is roman numerals I–V (Om mig, Ydelser, Priser, FAQ, Kontakt). If you add or remove a section, renumber the rest.
- CVR is `44 40 89 02` in the footer.
- Phone `+45 50 13 90 99`, email `vera@curavera.dk`.

## Deployment

- Hosted on GitHub Pages from `main` branch root.
- Custom domain `curavera.dk` via the `CNAME` file (do not delete it — GitHub treats removal as un-setting the custom domain).
- HTTPS is auto-provisioned by Let's Encrypt; "Enforce HTTPS" should be on in repo Settings → Pages.
- DNS for `curavera.dk` is managed in Microsoft 365 admin (the domain is also used for the owner's M365 mailbox — don't touch MX/SPF/DKIM/autodiscover records when changing DNS).

## Working in this repo

- Pushes to `main` go live within ~1 minute.
- Don't add a build step, package manager, or framework without explicit confirmation.
- Don't commit `.claude/` — it's session-local settings.
