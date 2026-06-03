# clipbeam-site

Single-page static marketing site for **clipbeam** — one static Go binary that
beams a file / screenshot / clipboard from your laptop onto a remote box's disk
(over SSH or Tailscale) and prints the absolute path so a coding agent can read it.

## What's here

- `index.html` — the entire site. One file. Hand-written inline CSS + a tiny
  inline script. **Zero build step, zero runtime deps, no framework, no CDN, no
  web fonts, no analytics.** Type uses native system stacks only (`ui-sans-serif`
  / `ui-monospace`), so the page paints instantly with no network request and no
  FOUT.
- `llms.txt` — machine-readable summary for LLMs / agents.
- `favicon.svg` — the paper-plane brand mark (mint body, amber tail-fin).
- `og.png` — 1200×630 social-share card referenced from `og:image` / `twitter:image`
  (rendered from `og.svg`, which is kept as the editable source).
- `vercel.json` — optional static-deploy config (security headers, clean URLs).

## Run locally

Just open the file:

```sh
open index.html            # macOS
```

Or serve it (for correct relative behavior / mobile testing on LAN):

```sh
python3 -m http.server 8000
# → http://localhost:8000
```

## Deploy (the human does this — not automated here)

It's pure static output, so any static host works. With Vercel:

```sh
vercel            # preview
vercel --prod     # production
```

No framework, no `package.json`, no install step.

## Design — "Signal"

A dark operator-console aesthetic built on one idea: the two endpoints are
**color-coded** as a two-temperature system. Mint (`#7af7c0`) is *local* — you,
your laptop, the primary action. Amber (`#ffb347`) is *remote* — the box, the
receiver, and the **printed path** wherever it appears. Soft blue (`#8ab4ff`) is
the **SSH transport** between them. A mint→white→amber "beam" sweeps left→right
(the file traveling laptop→box), and a two-tone paper-plane glyph (mint body,
amber tail-fin) recurs at every scale, echoing the macOS app icon.

The hero's reason to exist is a live terminal showing the real, verified flow:
`clipbeam setup user@box` → `clipbeam send screenshot.png box` → the remote path
printed in amber → `claude "describe the image at $(clipbeam last)"`.

Type: native system **sans** (marketing voice) + native system **mono** (every
product moment) — no web fonts. Accessible: semantic HTML, visible focus states,
alt/aria text on the terminal and every icon, a real `<table>` exit-code surface
with `<th scope>`, and `prefers-reduced-motion` disables all motion (the beam
degrades to a static mint→amber bar).

## License

MIT © Sani / VYBZ
