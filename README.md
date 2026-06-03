# clipbeam-site

Single-page static marketing site for **clipbeam** — one static Go binary that
beams a file / screenshot / clipboard from your laptop onto a remote box's disk
(over SSH or Tailscale) and prints the absolute path so a coding agent can read it.

## What's here

- `index.html` — the entire site. One file. Hand-written inline CSS + a tiny
  inline script. **Zero build step, zero runtime deps, no framework, no CDN, no
  analytics.** The one external request is the Google Fonts stylesheet
  (Space Grotesk + JetBrains Mono); it is `<link>`-loaded with `preconnect` and
  `font-display: swap`, and the CSS declares native system stacks as the
  fallback, so the page renders immediately and never blocks if fonts fail.
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

## Design — "Transmission"

A dark, terminal-grade direction built on one idea: the two endpoints are
**color-coded**. Cyan-mint (`#2ee6c5`) is the *local* laptop / sender; warm amber
(`#ffb347`) is the *remote* box / receiver. A beam (with a paper-plane riding it)
carries the payload left→right, and the printed remote **path** is rendered in the
remote's amber everywhere it appears — so the eye tracks the transmission from
laptop to box.

The hero is a live "transmission" panel: two labelled endpoint cards, an animated
beam + paper-plane between them, a two-prompt terminal showing the real
`clipbeam send → /remote/path → agent reads it` flow, and a literal
**"hand off to your agent"** control that copies `claude "describe … $(clipbeam last)"`.

Type: **Space Grotesk** (display) + **JetBrains Mono** (code/UI chrome), with
native system stacks as the fallback. Accessible: semantic HTML, visible focus
states, alt/aria text on the diagram and terminal, and `prefers-reduced-motion`
disables the beam animation.

## License

MIT © Sani / VYBZ
