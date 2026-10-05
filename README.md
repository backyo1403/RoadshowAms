# Vietnam Airlines — Roadshow Amsterdam 2026

A 26-slide presentation that runs as a web page. No build step, no
framework, no server-side code — it is plain HTML, CSS and JavaScript, so it can be
dropped onto any static host as-is.

## What's in here

```
index.html      the whole deck — markup, styles, script, images and fonts in one file
assets/         the source images, kept for editing (index.html has embedded copies),
                plus journey-clip.mp4, the corporate film slide 25 loads from here,
                and rehearsal/ — the spoken script used by rehearsal.html
  awards/       award badges, partner logotypes, lotus background
  icons/        the twelve milestone badges
  logos/        subsidiary and global-partner logos
og-cover.jpg    social preview image, shown when the link is shared
favicon.svg     browser tab icon
robots.txt      allows search engines
.nojekyll       tells GitHub Pages to serve the files untouched
```

## Viewing it locally

Double-click `index.html`. It opens in any modern browser and works fully offline —
every image and both typefaces (Be Vietnam Pro, Manrope) are embedded in the file. The one
exception is slide 25, whose film and music are read from `assets/`, so keep that folder
next to `index.html`.

`rehearsal.html` is a practice page, not part of the show: it puts the deck beside the
spoken script, highlights each word as a neural voice reads it, and keeps a running clock.
It needs a local server (`python -m http.server 8765`, then open
`http://localhost:8765/rehearsal.html`).

## Publishing it

The folder is the site. Upload `index.html` at the top level together with the `assets/`
folder — the page carries its own images and fonts, but slide 25's video and music live in
`assets/`.

**Netlify (quickest)** — go to app.netlify.com/drop and drag this whole folder onto
the page. You get a live URL in a few seconds.

**GitHub Pages** — commit the contents of this folder to a repository, then in
Settings → Pages choose the branch and the root folder. The `.nojekyll` file is
already here so nothing gets stripped.

**Vercel / Cloudflare Pages** — create a new project from the folder or repository
and leave the build command empty; the output directory is the folder itself.

**A company web server** — copy the folder into the web root, or into a
subdirectory such as `/roadshow/`. Nothing is linked externally, so it works at either depth.

## Presenting

- **Arrow keys**, **space**, or **swipe** move between slides. **Home** and **End**
  jump to the first and last.
- Clicking near the left or right edge of the screen also moves a slide.
- Each slide has its own build animation, which replays whenever you return to it.
- The deck is laid out on a fixed 1920×1080 stage and scaled to fit the window, so it
  looks the same on every screen; displays that aren't 16:9 get black bars.
- Moving between slides uses a morph transition: titles, labels and some panels glide
  from their place on one slide to their place on the next, like PowerPoint's Morph.
  This needs a browser with View Transitions (Chrome, Edge, Safari 18+, recent
  Firefox); elsewhere slides fade.
- Slide 25 runs by itself for about 3 minutes 35 seconds: "Let's begin your journey to Vietnam
  with Vietnam Airlines" (5s), the corporate film with its own English narration (3:15), then
  "See you in Vietnam" (5s), then black fades in with the Vietnam Airlines logo (10s).
  Browsers only allow sound after a key press or click, so arrive on it with the keyboard or
  the arrows rather than by loading `#25` directly.
- Slide 13 opens with a map intro of about 25 seconds (Vietnam, then the three hubs,
  then the routes). Pressing forward during it jumps to its end; the next press moves on.
- Animation plays even when the operating system asks for reduced motion. To turn all
  motion off, open the deck with `?calm` in the address, e.g. `index.html?calm#1`.
- The address bar carries the slide number (`…/#12`), so you can link straight to a
  slide or reload without losing your place.
- Press **F11** for full screen.

## Editing

Everything lives in `index.html`. Slides are `<section class="slide">` elements in
document order — the counter, progress bar and navigation all read that order, so
adding, removing or reordering a section is enough; no numbering to update by hand.
Design tokens (the teal and gold palette, the two typefaces) are the CSS custom
properties in the `:root` block at the top of the stylesheet. Images and fonts are
inlined as base64 `data:` URIs; to swap a photo, replace its `data:image/…` string
(the originals are in `assets/`).

Sizes inside slides are in px or container units (`cqw`/`cqh`, relative to the
1920×1080 stage) — don't use `vw`/`vh`, which follow the window instead. Content
slides use `slide-inner top` with a `slide-head` (eyebrow + title) and a `slide-body`,
which keeps every title at the same spot.

To morph an element into one on a neighbouring slide, give both the same `data-morph`
name, e.g. `data-morph="title"`. A name may appear only once per slide; an element can
list several (`data-morph="title ams-title"`) and pairs on the first one the other slide
also has. A morphed element skips its own entrance build.

## Slide order

| # | Slide | # | Slide |
|---|---|---|---|
| 1 | Cover | 12 | Network in numbers + growth chart |
| 2 | Who Are We? | 13 | International network map |
| 3 | Company overview | 14 | Domestic network |
| 4 | Key milestones | 15 | Network expansion plan (5–10 years) |
| 5 | Fleet | 16 | Hospitality, elevated to an art |
| 6 | Group companies | 17 | Business class |
| 7 | Key global partners | 18 | Premium Economy & Economy |
| 8 | Awards | 19 | Two capitals. One nonstop bridge. |
| 9 | Vision 2030 | 20 | The route |
| 10 | We keep on growing | 21 | Schedule |
| 11 | Our network still accelerating | 22 | New market, big opportunities |
|  |  | 23 | Strong commercial support |
|  |  | 24 | Our offices in Europe |
|  |  | 25 | Journey film — see you in Vietnam |
|  |  | 26 | Thank you |
