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

- Hosted on GitHub Pages from `main` branch root. Pushes to `main` redeploy within ~1 minute.
- Custom domain `curavera.dk` via the `CNAME` file (do not delete it — GitHub treats removal as un-setting the custom domain).
- HTTPS is auto-provisioned by Let's Encrypt and Enforce HTTPS is on, so `http://` and `www.` both 301 to `https://curavera.dk`. Cert auto-renews ~30 days before expiry.
- DNS for `curavera.dk` is managed in Microsoft 365 admin (the domain is also used for the owner's M365 mailbox — don't touch MX/SPF/DKIM/autodiscover records when changing DNS).

### DNS records (for reference / restore)

Apex `curavera.dk` — four A and four AAAA records pointing at GitHub Pages:

```
A     185.199.108.153 / .109.153 / .110.153 / .111.153
AAAA  2606:50c0:8000::153 / 8001::153 / 8002::153 / 8003::153
CNAME www  →  mschristiansen.github.io
```

### If HTTPS cert provisioning hangs

GitHub sometimes silently fails to issue the Let's Encrypt cert after the custom domain is first set. Standard unstick:

```sh
echo '{"cname":null}' | gh api -X PUT repos/mschristiansen/curavera/pages --input -
sleep 10
gh api -X PUT repos/mschristiansen/curavera/pages -f cname=curavera.dk
# wait ~5–15 min, verify cert subject is curavera.dk:
echo | openssl s_client -servername curavera.dk -connect curavera.dk:443 2>/dev/null | openssl x509 -noout -subject -dates
gh api -X PUT repos/mschristiansen/curavera/pages -F https_enforced=true
```

Brief side effect: ~30s where the custom domain isn't bound. Plain HTTP at the apex IPs continues to serve.

## Responsive

- Single breakpoint at `max-width: 880px` for the mobile/tablet layout (everything below is "mobile" in this repo's vocabulary).
- The nav uses a hamburger toggle below 880px (`.nav__toggle` + `.nav--open` class). The toggle, panel transition, and link-tap-to-close are all wired up in the inline `<script>` at the bottom of `index.html` — keep them together.

## Working in this repo

- Don't add a build step, package manager, or framework without explicit confirmation.
- Don't commit `.claude/` — it's session-local settings.
