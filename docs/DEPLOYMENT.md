# Deployment — Variant 1

## Hosting assumptions

Static site hosted on Netlify. No backend, no database, no server-rendered
content.

## Build

- **Build command:** none. This is plain HTML/CSS/JS with no compile step.
- **Publish directory:** repository root (`.`), as set in `netlify.toml`.

Because the repository root is the Netlify publish directory, only
public-facing website material should be committed here — anything else
(like the `docs/*.md` files and `README.md`) is explicitly blocked from
being served by the redirects in `netlify.toml`, but keep that in mind
before adding new root-level files.

## Headers

`netlify.toml` sets:

- A one-year cache on `/images/*` (safe because image filenames change
  when the photo changes — see `docs/ASSETS.md`).
- A no-cache / must-revalidate policy on HTML, CSS and JS so edits show up
  immediately for returning visitors.
- Security headers on every response: `Content-Security-Policy`,
  `X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy`,
  `Permissions-Policy`, and `Strict-Transport-Security`.

The CSP is intentionally scoped to `'self'` (plus `'unsafe-inline'` for the
handful of inline `style=""` attributes already in the HTML) because this
variant currently loads no third-party scripts, fonts, or embeds. **If you
ever add Google Fonts, an analytics script, a map embed, or any other
third-party resource, you must widen the relevant CSP directive in
`netlify.toml` first** or that resource will silently fail to load.

## Redirects / custom domain

No redirects currently exist beyond the two that 404 stray Markdown/config
files (`README.md`, `netlify.toml`) so they aren't servable as public pages.
There is no confirmed production custom domain yet — `robots.txt` and
`sitemap.xml` both use a `REPLACE-WITH-PRODUCTION-DOMAIN` placeholder that
must be swapped for the real domain once one is assigned, rather than
guessed.

## 404 behavior

`404.html` is a static file at the repository root. Netlify serves it
automatically for any unmatched path on this site (this is Netlify's
default behavior for a file literally named `404.html` at the publish
root — no extra `[[redirects]]` rule is required for it to work).

## Deployment verification checklist

- [ ] `index.html`, `menu.html`, `locations.html`, `story.html`,
      `gallery.html` all return HTTP 200.
- [ ] An unknown path (e.g. `/does-not-exist`) returns HTTP 404 and renders
      `404.html`.
- [ ] `robots.txt` is served as `text/plain`, not as an HTML fallback.
- [ ] `sitemap.xml` is served as XML, not as an HTML fallback.
- [ ] Response headers include the security headers from `netlify.toml`
      (check with browser dev tools or `curl -I`).
- [ ] Every "Order" link on `index.html`, `menu.html` and `locations.html`
      goes to the correct location's ordering-system URL.
- [ ] Mobile nav toggle works on a small viewport.
