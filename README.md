# Vital Kneads — website

Static site for **vitalkneadsmt.com**, migrated off Squarespace. Plain HTML + CSS,
no build step, hosted free on **GitHub Pages**. The domain stays registered at
Squarespace; only DNS is repointed here.

## Structure

```
index.html                Home
our-philosophy/index.html  Our Philosophy   (content image + hidden SEO text)
about/index.html           About            (bio + portraits)
new-page/index.html        Services         (slug kept for URL continuity)
testimonials/index.html    Testimonials
contact/index.html         Contact
404.html                   Not-found page
assets/css/styles.css      Shared stylesheet
assets/fonts/              Self-hosted Jost (woff2)
assets/img/                Images (webp)
```

Internal links and asset paths are **relative** (e.g. `../assets/...`), so the site
renders correctly both at the GitHub Pages project subpath (staging) and at the
custom-domain root (production).

Booking buttons link to MassageBook (`massagebook.com/biz/VitalKneadsLLC`) and gift
cards to Square — both unchanged and external.

## Editing

Open the relevant `index.html` and edit the text directly. Shared header/footer are
duplicated in each page (a nav change means updating each file). Brand color is
`#38abbc`; all styling lives in `assets/css/styles.css`.

## Local preview

```
python3 -m http.server 8080
```
Then open http://localhost:8080

## Deploy (GitHub Pages)

### 1. Staging (review before touching the domain)
1. Push to `main`.
2. Repo **Settings → Pages** → Source: *Deploy from a branch* → `main` / `/ (root)`.
3. Review at the project URL: `https://vital-kneads.github.io/vital-kneads-site/`
   (no custom domain yet — relative paths make this work).

### 2. Cutover (after approval)
1. **Settings → Pages → Custom domain** → enter `vitalkneadsmt.com`, Save.
   (This writes a `CNAME` file to the repo automatically.)
2. Update DNS at Squarespace (below).
3. Once DNS resolves, tick **Enforce HTTPS**.

## Squarespace → GitHub Pages DNS cutover

Keep the Squarespace site live until the new site is verified on the domain.
**Snapshot the current DNS records first.** Then set:

```
Type   Host   Value
A      @      185.199.108.153
A      @      185.199.109.153
A      @      185.199.110.153
A      @      185.199.111.153
CNAME  www    vital-kneads.github.io
```
(Verify current IPs against GitHub Pages docs at cutover.) Once
`https://vitalkneadsmt.com` serves this site with valid HTTPS, cancel the
Squarespace **website builder** subscription — the domain registration stays.

## Notes / intentional deviations from the original

- Fonts: original used Adobe Typekit `hypatia-sans-pro` / `adorn-smooth-slab-serif`
  (licensed, not redistributable). Replaced with self-hosted **Jost** as a close
  free match. Swap fonts in `styles.css` if exact Adobe fonts are wanted (needs an
  Adobe Fonts web project).
- Image-only pages (Philosophy, Contact) keep the original graphics verbatim, with
  the text transcribed into a hidden block for SEO / screen readers.
