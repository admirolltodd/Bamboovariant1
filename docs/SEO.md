# SEO Recommendations — Variant 1

This variant's HTML pages were **not modified** by this infrastructure
pass, per the project's non-destructive rules. Everything below is a
recommendation for a future, deliberate content change — not something
already applied.

## Current state (as of this audit)

- Every page has a unique `<title>`.
- `index.html`, `menu.html`, `locations.html` have a `<meta
  name="description">`. **`story.html` and `gallery.html` do not.**
- No page has a `<link rel="canonical">`.
- No page has Open Graph (`og:*`) or Twitter Card (`twitter:*`) meta tags.
- No page has JSON-LD structured data.
- `index.html` and `menu.html` set `<link rel="icon">`. **`locations.html`,
  `story.html` and `gallery.html` do not** — on those three pages the
  browser/OS falls back to its own default favicon behavior.
- `robots.txt` and `sitemap.xml` were added by this pass and are crawlable
  (new standalone infrastructure files, not existing page edits).

## Recommended (not applied) meta description additions

- `story.html`: something in the voice of the existing "Local since 2007"
  copy, e.g. *"The story of Bamboo Sushi Bar & Hibachi Express, from a
  45-seat Crestview restaurant in 2007 to three Emerald Coast locations
  today."*
- `gallery.html`: e.g. *"Photos from Bamboo Sushi Bar & Hibachi Express —
  food, storefronts and the dining room across all three Emerald Coast
  locations."*

## Recommended (not applied) favicon link

Add the same `<link rel="icon" type="image/png"
href="images/brand/bamboo-sushi-hibachi-logo-full.png">` tag already used
on `index.html`/`menu.html` to `locations.html`, `story.html` and
`gallery.html` so the favicon is consistent across the whole site.

## Recommended (not applied) canonical tags

Add `<link rel="canonical" href="https://REPLACE-WITH-PRODUCTION-DOMAIN/PAGE">`
to every page once a production domain is confirmed. Do not guess the
domain in the meantime — leave it as a documented placeholder here rather
than writing a canonical tag with an unconfirmed URL into the HTML.

## Recommended (not applied) Open Graph / Twitter Card tags

For `index.html` (and ideally every page), using only facts already present
in this repository:

```html
<meta property="og:type" content="restaurant">
<meta property="og:title" content="Bamboo Sushi Bar & Hibachi Express | Emerald Coast, FL">
<meta property="og:description" content="Family-owned sushi and hibachi on Florida's Emerald Coast since 2007. Browse the menu and order from Bamboo in Crestview, Fort Walton Beach or Niceville.">
<meta property="og:url" content="https://REPLACE-WITH-PRODUCTION-DOMAIN/">
<meta property="og:image" content="https://REPLACE-WITH-PRODUCTION-DOMAIN/images/food/seared-ahi-tuna-sashimi-emerald-coast.webp">
<meta name="twitter:card" content="summary_large_image">
```

No dedicated 1200×630 social-share crop exists in this repo today (see
`docs/ASSETS.md`); the hero image above is a placeholder choice, not a
confirmed social-share asset.

## Recommended (not applied) structured data

A `Restaurant` JSON-LD block using only the facts already present in
`locations.html` / `data/restaurant-facts.js`:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Restaurant",
  "name": "Bamboo Sushi Bar & Hibachi Express",
  "servesCuisine": "Japanese",
  "location": [
    {
      "@type": "Place",
      "name": "Bamboo Sushi Bar & Hibachi Express - Crestview",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "2505 S Ferdon Blvd",
        "addressLocality": "Crestview",
        "addressRegion": "FL",
        "postalCode": "32536",
        "addressCountry": "US"
      },
      "telephone": "+1-850-689-1391"
    },
    {
      "@type": "Place",
      "name": "Bamboo Sushi Bar & Hibachi Express - Fort Walton Beach",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "9 Eglin Pkwy NE",
        "addressLocality": "Fort Walton Beach",
        "addressRegion": "FL",
        "postalCode": "32548",
        "addressCountry": "US"
      },
      "telephone": "+1-850-200-4250"
    },
    {
      "@type": "Place",
      "name": "Bamboo Sushi Bar & Hibachi Express - Niceville",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "117 W John Sims Pkwy",
        "addressLocality": "Niceville",
        "addressRegion": "FL",
        "postalCode": "32578",
        "addressCountry": "US"
      },
      "telephone": "+1-850-678-0771"
    }
  ]
}
</script>
```

This uses only addresses, phone numbers and location names already present
in this repository. Do not add a rating/review claim or a founding-date
`foundingDate` field unless a specific, verifiable date is confirmed beyond
the general "since 2007" copy already on the site.

## Sitemap / robots

Both were added as new standalone files in this pass (not existing-page
edits) and list only the five pages that exist in this repository. Update
`REPLACE-WITH-PRODUCTION-DOMAIN` in both `robots.txt` and `sitemap.xml`
together once a production domain is confirmed.
