# Accessibility Notes — Variant 1

Observations only. No layout or content changes were made as part of this
pass beyond the two isolated, near-zero-risk items marked "Applied" below.

## Already in good shape

- `lang="en"` set on every page.
- A working skip-to-content link (`.skip`, targets `#main`) on every page,
  and it does get a visible focus style (moves on-screen and gets a white
  background on `:focus`).
- Heading structure is a single `<h1>` per page with `<h2>`/`<h3>` used for
  sub-sections in a sensible order (checked across all five pages).
- `@media (prefers-reduced-motion: reduce)` in `css/site.css` disables
  `scroll-behavior` and transitions site-wide.
- The mobile nav toggle button has `aria-label="Open navigation"` and
  `aria-expanded` is kept in sync by `js/site.js`.
- No forms exist on this site, so form labeling is not applicable.

## Observations for future, deliberate fixes

- **Focus visibility beyond the skip link.** `css/site.css` defines a
  `:focus` style only for `.skip`. Buttons and links elsewhere rely on the
  browser's default focus ring (not removed, but not reinforced either).
  Consider adding a visible `:focus-visible` outline to `.btn`, `.nav-links
  a` and `.food-tile` so keyboard users always get a clear indicator,
  especially over the `.hero` image or the `.section-red` background where
  a thin default outline could be harder to see.
- **Color contrast on `.section-red`.** White text/eyebrow labels sit on
  `--red: #d8262a`. This looks likely to pass WCAG AA for large text but
  should be checked with a contrast tool for any smaller body text placed
  on that background before it's relied on for body copy.
- **Decorative vs. content images.** Most `<img>` tags carry descriptive
  alt text, but a few (e.g. the brand mark in the footer, `alt=""`) are
  correctly marked decorative. Continue that pattern: an image already
  described by adjacent text (like a logo next to the restaurant name)
  should stay `alt=""`, not get redundant alt text.
- **Menu jump bar overlap.** `.menu-jump` is `position: sticky; top: 78px`
  matching the header height — this is already accounted for, but if the
  header height ever changes, re-check that anchor-linked scrolling on
  `menu.html` doesn't hide content under the sticky bars.

## Applied (near-zero-risk only)

No content or layout changes were made. The two favicon/meta-description
gaps noted in `docs/SEO.md` were left as documented recommendations rather
than applied, since editing existing `<head>` content on
`locations.html`/`story.html`/`gallery.html` falls outside this pass's
scope of "infrastructure and documentation only."
