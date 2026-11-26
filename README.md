# Subhajit Pal — Portfolio (GitHub Pages)

A single-file static portfolio. No build step, no dependencies, no CI. Push it and it is live.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole site — markup, CSS and a ~15-line theme script |
| `Subhajit-Pal-CV.pdf` | The "Download CV" link target |
| `README.md` | This file (safe to delete before publishing) |

## Preview locally

Any static server works:

```bash
python -m http.server 8123
```

Then open <http://127.0.0.1:8123>. Theme override for testing: `?theme=light` or `?theme=dark`.

## Publish

This folder is already a git repo on `main`, committed, with `origin` set to
`https://github.com/subhajitpal7/subhajitpal7.github.io.git`.

### One-time: create the repo and push

1. On GitHub create a repo named **exactly** `subhajitpal7.github.io`, set to **Public**.
   Do not initialise it with a README — this repo already has history.
2. From this folder:

```bash
git push -u origin main
```

3. Live at <https://subhajitpal7.github.io> in a minute or two. A user-site repo enables
   Pages automatically; no Settings toggle needed.

### After that, every update

```bash
git add -A
git commit -m "what changed"
git push
```

Live about 30 seconds later. No build step.

### If you ever want it under a subpath instead

Push the same files to any repo and enable **Settings → Pages → Source: Deploy from a
branch → main / (root)**. The site appears at `https://subhajitpal7.github.io/<repo>/`.
All asset links are relative, so both shapes work unchanged.

## Custom domain

1. Buy a domain and point DNS at GitHub:
   - `CNAME  @    subhajitpal7.github.io`
   - `CNAME  www  subhajitpal7.github.io`
2. Add a file named `CNAME` containing just your domain, e.g. `subhajit.dev`
3. Repo **Settings → Pages → Enforce HTTPS**

## Editing content

Everything is in `index.html`, in document order:

| Section | Find |
|---|---|
| Name / role / intro | `<section class="hero"` |
| Stat cards | `<ul class="stats">` |
| Project entries | `<article class="card">` |
| Jobs | `<article class="job">` |
| Skill chips | `<span class="chip">` |
| Education | `<div class="edu">` |
| Contact links | `<footer>` |

To swap the CV, replace `Subhajit-Pal-CV.pdf` with a new file **of the same name**, or update the `href` in the footer.

## Design notes

Ported from the reference layout, recoloured to **teal**: cool off-white surfaces, a deep teal primary,
`Poppins` body with `Instrument Serif` accents, `JetBrains Mono` for section eyebrows, cards at 1rem radius
with a soft shadow, sticky blurred header. Colours are defined once as CSS custom properties in `:root` and
overridden under `html.dark`.

### Changing the accent colour

One place controls the whole scheme. In `:root`, set `--primary` (the accent) plus `--chart-1..3` (the cursor
trail gradient), and the same four in `html.dark`. Everything else — links, eyebrows, chips, card hover,
selection — derives from `--primary`.

### Cursor trail

A full-screen `<canvas>` sits behind the content (`z-index:0`, `pointer-events:none`). Fourteen strands of
fifty spring-linked nodes chase the pointer and are stroked as tapered ribbons, thin and faint at the outer
edge. Stroke colour is read live from `--chart-1..3`, so it recolours when the theme flips.

It is off automatically for touch pointers and `prefers-reduced-motion`, pauses when the tab is hidden or
blurred, and can be switched off with the sparkle button in the header (stored in `localStorage` under
`trail`).
