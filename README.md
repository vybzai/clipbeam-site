# clipbeam-site

Single-page static marketing site for **clipbeam** — one static Go binary that
beams a file / screenshot / clipboard from your laptop onto a remote box's disk
(over SSH or Tailscale) and prints the absolute path so a coding agent can read it.

## What's here

- `index.html` — the entire site. One file. Hand-written inline CSS + a tiny
  inline script. **Zero build step, zero runtime deps, zero external requests**
  (no web fonts, no CDN, no analytics). Uses system font stacks.
- `vercel.json` — optional static-deploy config.

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

## Design

A bright, airy, editorial direction: warm paper background, one saturated
"signal orange" accent (the beam), an electric-blue secondary, and a
paper-plane / beam motif rendered as clean geometric SVG. Big type, generous
whitespace, a dark terminal showing the real `send → /path → agent reads it`
flow in the hero. Accessible: semantic HTML, visible focus states, alt/aria text,
and `prefers-reduced-motion` respected.

## License

MIT © Sani / VYBZ
