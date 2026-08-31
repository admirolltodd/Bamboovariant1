# Content Guide — Variant 1

Practical rules for editing this variant's content without breaking its
design or its accuracy.

## Menu content

- Menu items live directly in `menu.html`, grouped into sections with
  anchor IDs: `#starters`, `#sushi`, `#specialty`, `#sashimi`, `#hibachi`,
  `#noodles`, `#more`, plus `#order`.
- The menu carries **no prices**. Do not add them — the online ordering
  system (linked from each location) is the source of truth for pricing and
  availability.
- If you add or rename a menu section, also update the sticky jump-bar
  links at the top of `menu.html` (`.menu-jump`) so they still point at a
  real anchor, and update `sitemap.xml`/`docs/SEO.md` only if the change
  affects a whole page rather than an in-page section.

## Location content

- Location details (address, phone, hours) appear in three places:
  `locations.html`, the location cards on `index.html`, and (as a data
  object, currently unused by any page) `data/restaurant-facts.js`. Keep
  all three in sync when hours or an address change.
- Each location's "Order" button links directly to that location's own
  ordering-system URL. Never point a location's Order button at another
  location's URL or at a generic/shared ordering page.

## Gallery / photography

- Do not invent a dish name for a gallery photo. Use the same generic,
  descriptive alt text style already used on this site (e.g. "Prepared
  seafood dish", "Bamboo dining room") unless the site's own existing copy
  already names the dish.
- New gallery photography goes in `images/gallery/`; new plated-food
  photography goes in `images/food/` (see `docs/ASSETS.md`).

## Voice and tone

Existing copy is short, declarative, and slightly stylized (e.g. "Sushi.
Hibachi. Bamboo.", "Come hungry.", "Local since 2007."). Match that
brevity — this variant relies on large type and short lines, not long
paragraphs, so new copy should stay short enough to fit the existing
layout without introducing new wrapping/overflow issues.
