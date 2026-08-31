# Bamboo Sushi Bar & Hibachi Express — Variant 1 (Usability Concept)

This repository is one of three parallel design concepts for the Bamboo Sushi
Bar & Hibachi Express website. **Variant 1 is the multi-page,
usability-focused concept**: a traditional multi-page architecture (separate
Menu, Locations, Story and Gallery pages) built around a dark background with
red accent color, clear page-level navigation, and a sticky in-page jump bar
on the Menu page.

This README documents this variant only. It does not describe Variant 2
(bright black/white/red concept) or Variant 3 (premium dark concept) — those
live in their own repositories.

## Design concept

- Dark UI (`--black: #080808`) with a red accent (`--red: #d8262a`) used for
  calls to action, section dividers and the eyebrow labels.
- Multi-page structure rather than a single long-scrolling homepage — each
  major topic (menu, locations, story, gallery) gets its own page and URL.
- A sticky secondary navigation bar (`.menu-jump`) on the Menu page lets
  visitors jump directly to a menu section (sushi, hibachi, noodles, etc.).
- No frameworks, no build step: plain HTML, one shared stylesheet, and one
  small vanilla JS file for the mobile nav toggle.

## Page structure

| Page | File | Purpose |
|---|---|---|
| Home | `index.html` | Hero, food category tiles, story teaser, location cards, gallery teaser |
| Menu | `menu.html` | Full menu by section (starters, sushi, specialty, sashimi, hibachi, noodles, more) with an `#order` section |
| Locations | `locations.html` | All three locations with address, phone and hours |
| Our Story | `story.html` | Restaurant history/timeline |
| Gallery | `gallery.html` | Photo gallery |
| 404 | `404.html` | Custom not-found page (added as part of this infrastructure pass) |

Primary navigation (present on every page): Home · Menu · Locations · Our
Story · Gallery, plus a persistent "Order Online" button.

## Running locally

This is a static site with no build step, no package manager, and no server
dependency. To preview it locally, serve the repository root with any static
file server, for example:

```
python3 -m http.server 8080
```

or

```
npx serve .
```

Then open `http://localhost:8080/`. Opening `index.html` directly via
`file://` also works for a quick look, but a local server more accurately
reflects how Netlify serves the site (correct MIME types, no CORS quirks).

## Primary directories

```
/
├── index.html
├── menu.html
├── locations.html
├── story.html
├── gallery.html
├── 404.html
├── css/
│   └── site.css        # single shared stylesheet for every page
├── js/
│   └── site.js          # mobile nav toggle only
├── data/
│   └── restaurant-facts.js   # structured location/hours data (see note below)
├── images/
│   ├── awards/
│   ├── brand/
│   ├── food/
│   ├── gallery/
│   ├── menu/
│   └── press/
├── docs/                # infrastructure & production documentation (this pass)
├── robots.txt
├── sitemap.xml
└── netlify.toml
```

## Where content actually lives

- **Menu content** is written directly into `menu.html` (no CMS, no JSON
  feed). Item names/descriptions are grouped into sections with `id`
  attributes (`#starters`, `#sushi`, `#specialty`, `#sashimi`, `#hibachi`,
  `#noodles`, `#more`) that the sticky jump bar links to. The menu
  intentionally carries no prices — the ordering system is the source of
  truth for pricing.
- **Location data** (address, phone, hours) is written directly into
  `locations.html` and repeated in the location cards on `index.html`.
  `data/restaurant-facts.js` defines the same three locations as a
  `window.BAMBOO_FACTS` object, but note: **no HTML page currently loads
  this script** (it isn't referenced by a `<script src>` anywhere). Treat it
  as a maintained reference/data file for future use, not as the live source
  the pages render from today — if you update hours or an address, update
  `locations.html`, the home page cards, and `data/restaurant-facts.js`
  together so they don't drift apart.
- **Order links** are direct links to each location's own ordering-system
  URL (`menu-6161.orderexperience.net/...`), inline in `index.html`,
  `locations.html` and `menu.html`. There is no generic/shared "order now"
  destination — each location's button points at that location's own menu.

## JavaScript behavior

`js/site.js` is a single small script: it toggles the `.open` class on the
mobile nav drawer when `.menu-toggle` is clicked, sets `aria-expanded`
accordingly, and closes the drawer again when a nav link inside it is
clicked. There is no other client-side behavior (no analytics, no map
embeds, no third-party widgets) on this variant today.

## Deployment

Deployed as a static site on Netlify. See `docs/DEPLOYMENT.md` for the full
checklist. In short: publish directory is the repository root, there is no
build command, and `netlify.toml` carries caching and security headers.

## Production checklist

Before promoting a deploy of this variant:

- [ ] Click every nav link and every "Order" link on all three locations.
- [ ] Confirm addresses, phone numbers and hours match across
      `index.html`, `locations.html` and `data/restaurant-facts.js`.
- [ ] Test the mobile nav toggle (`js/site.js`) at a narrow viewport.
- [ ] Test the Menu page's sticky jump bar against every section anchor.
- [ ] Confirm `robots.txt` is served as plain text and `sitemap.xml` as XML.
- [ ] Confirm `404.html` renders for an unknown path and returns HTTP 404.
- [ ] Confirm Netlify applies the headers defined in `netlify.toml`.

## Known limitations

- No Open Graph, Twitter Card, canonical link, or JSON-LD structured data on
  any page. See `docs/SEO.md` for specific, non-destructive recommendations.
- `story.html` and `gallery.html` have no `<meta name="description">`, and
  `locations.html`/`story.html`/`gallery.html` have no `<link rel="icon">`
  (only `index.html` and `menu.html` set a favicon link). See
  `docs/SEO.md`.
- `data/restaurant-facts.js` is not loaded by any page (see above) — it's
  effectively documentation-as-code today, not live data.
- No automated tests or link checker; verification is manual (see checklist
  above and `docs/MAINTENANCE.md`).

## Related repositories

- Variant 2 (bright black/white/red concept) — separate repository.
- Variant 3 (premium dark, combined/final concept) — separate repository.
- `828bamboosushi` — production-engineering reference repository used to
  inform the infrastructure and documentation patterns in this `docs/`
  folder. Its page content and visual design are not part of this variant.
