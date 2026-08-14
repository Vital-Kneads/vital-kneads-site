# Vital Kneads — site maintenance guide (for Claude Code)

This repo **is** the live website for **vitalkneadsmt.com** — a static site hosted
free on GitHub Pages, migrated off Squarespace. The owner, **Milly** (Emily
Anderson), is non-technical and makes periodic updates by describing them in plain
English. Your job: make the change faithfully, **preview it, and deploy only after
she confirms.**

## Working with Milly (the loop)
1. She describes a change in everyday language ("make the intro shorter", "swap the
   About photo", "add a testimonial", "make the teal a little darker").
2. You make the edit(s).
3. **Preview** — run the local server and take a screenshot so she can see it before
   it's public (or describe exactly what changed).
4. **Deploy only on her OK.** Deploy = commit + push to `main`; GitHub Pages
   rebuilds and it's live at https://vitalkneadsmt.com within ~1 minute.
5. Every change is a git commit, so **anything can be undone** — if she dislikes a
   change, revert it (`git revert` or restore the file and redeploy).

## Preview locally
```
python3 -m http.server 8080
```
Then open http://localhost:8080 . (The browser pane won't always re-composite after
scrolling — reload/navigate fresh, or check computed styles via JS if a screenshot
comes back blank.)

## Deploy
```
git add -A && git commit -m "describe the change" && git push
```
Push auth is already in the macOS keychain (gh, account `vitalkneadsco`). Live in
~1 min. Confirm with `curl -sI https://vitalkneadsmt.com/` if needed.

## Structure
- Plain **HTML + CSS, no build step**. Six pages, each a folder with `index.html`:
  `/` (`index.html`), `/our-philosophy/`, `/about/`, `/new-page/` (**Services**),
  `/testimonials/`, `/contact/`. Plus `404.html`.
- **The header (logo + nav) and footer are DUPLICATED in every page.** A nav/footer
  change means editing **all 7 HTML files** (the 6 pages + `404.html`).
- `assets/css/styles.css` — all styling. `assets/img/` — images (webp).
  `assets/fonts/` — self-hosted fonts. `_fonttest.html` is a git-ignored scratch
  file for comparing fonts; ignore it.
- Links and asset paths are **relative** (`../assets/...`) so the site works at any
  base path. **Keep them relative** — don't switch to root-absolute (`/assets/...`).

## Brand tokens (defined in `styles.css` `:root`)
- Teal (buttons/accents) `#38abbc`; heading teal `#318996`; nav-active cyan
  `#00eaff`; footer teal `#1d7f95`; ink `#0f1010`.
- **Body / headings / page titles** = **Source Sans 3** (self-hosted; free stand-in
  for the original licensed `hypatia-sans-pro`). Body is light (weight **300**) with
  **0.14em** letter-spacing and loose line-height — this airy typesetting is
  deliberate; keep it.
- **Whimsical display font (nav + buttons)** = **Neucha** (`--display`; stand-in for
  the licensed `silverstein` / `adorn-smooth-slab-serif`). This is what gives the
  site its personality. **Do not** reintroduce the licensed Adobe fonts.

## Conventions & gotchas
- This is a **faithful rebuild** of the old Squarespace site — match the existing
  look unless Milly explicitly wants a new direction.
- **Images:** prefer **webp**; always include `alt` text and `width`/`height`; use
  `loading="lazy"` for anything below the fold. Convert with `sips -s format webp`.
- **Booking buttons** → `massagebook.com/biz/VitalKneadsLLC`; **gift cards** →
  Square. External, keep as-is.
- The **Services page embeds a live MassageBook iframe** — the one external
  dependency. Don't remove it unless asked.
- **Philosophy & Contact are image-only pages**: their text is baked into graphics,
  with the real text mirrored in a `.visually-hidden` block for SEO. If a graphic's
  wording changes, update that hidden text too.
- Keep each page's `<title>`, `meta description`, `canonical`, and `og:` tags
  sensible when editing.
- **Do NOT touch:** the `CNAME` file (custom domain), DNS, or anything outside this
  repo. Domain is registered at Squarespace ($20/yr); DNS points to GitHub Pages;
  the site deploys from `main` / root with "Enforce HTTPS" on.

## Common tasks (cookbook)
- **Edit copy** → find the text in the page's `index.html`, edit it.
- **Add/replace a photo** → drop it in `assets/img/` (webp), reference it with `alt`
  + `width`/`height`.
- **Add a testimonial** → duplicate a `<figure class="testimonial">` block in
  `testimonials/index.html`.
- **Tweak a color / spacing / font** → edit the token or rule in `styles.css`
  (applies site-wide).
- **Change the nav or footer** → edit **all 7** HTML files identically.
