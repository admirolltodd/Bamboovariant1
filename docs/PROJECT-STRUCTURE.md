# Project Structure — Variant 1

This reflects the actual repository layout. It is documentation only; no
files were moved or renamed to produce this listing.

```
/
├── index.html            # Home: hero, food categories, story teaser, locations, gallery teaser
├── menu.html             # Full menu by section, includes #order anchor
├── locations.html        # All three locations: address, phone, hours
├── story.html            # Restaurant history/timeline
├── gallery.html          # Photo gallery
├── 404.html              # Custom not-found page
├── robots.txt
├── sitemap.xml
├── netlify.toml
├── README.md
├── css/
│   └── site.css          # Single shared stylesheet for all pages
├── js/
│   └── site.js           # Mobile nav toggle only
├── data/
│   └── restaurant-facts.js   # window.BAMBOO_FACTS — not currently loaded by any page
├── images/
│   ├── awards/            # Community's Choice / Best of Florida award graphics
│   ├── brand/              # Logo files
│   ├── food/               # Dish photography used on the home/menu pages
│   ├── gallery/            # Storefront, signage and dining-room photography
│   ├── menu/                # Menu board photographs (gluten-free/vegan boards, etc.)
│   └── press/              # Press clippings
└── docs/                  # This documentation set
    ├── PROJECT-STRUCTURE.md
    ├── ASSETS.md
    ├── CONTENT-GUIDE.md
    ├── DEPLOYMENT.md
    ├── SEO.md
    ├── ACCESSIBILITY.md
    └── MAINTENANCE.md
```

## Notes

- There is no `order.html` in this variant — ordering is handled via an
  `#order` anchor on `menu.html` plus per-location "Order" buttons on
  `index.html` and `locations.html` that link straight to each location's
  ordering-system URL.
- `data/restaurant-facts.js` exists but is not referenced by a `<script
  src>` in any HTML page. It is kept as-is (see `docs/MAINTENANCE.md`); this
  audit did not wire it up or remove it, since either action would be a
  functional change beyond adding infrastructure.
