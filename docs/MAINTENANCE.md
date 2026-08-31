# Maintenance Guide — Variant 1

Practical instructions for common future edits. No build tools, package
managers, or frameworks are involved anywhere in this workflow.

## Updating menu descriptions

1. Edit the relevant section directly in `menu.html` (sections are marked
   with `id` attributes: `#starters`, `#sushi`, `#specialty`, `#sashimi`,
   `#hibachi`, `#noodles`, `#more`).
2. Do not add prices — pricing lives only on the ordering system.
3. If you add a brand-new section, add a matching link in the `.menu-jump`
   bar at the top of `menu.html` pointing at the new anchor.

## Updating location information

1. Update `locations.html` first (the canonical page for hours/address).
2. Update the matching location card on `index.html`.
3. Update `data/restaurant-facts.js` (`window.BAMBOO_FACTS`) to match, even
   though no page currently loads it — keep it accurate in case it's wired
   up later.
4. If you later add structured data or OG tags per `docs/SEO.md`, update
   those too so every source agrees.

## Replacing hero photos

Replace the file referenced by `.hero img` in `index.html` with a new file
in `images/food/` or `images/gallery/` (see `docs/ASSETS.md` for naming
convention). Give the new file a new, descriptive filename rather than
overwriting the old one in place — `netlify.toml` caches everything under
`/images/*` for a year, so reusing a filename means returning visitors keep
seeing the old photo until their cache expires.

## Adding gallery images

Add the new file to `images/gallery/` or `images/food/` and reference it
from `gallery.html`. Do not caption it with a specific dish name unless
that name is already confirmed elsewhere on the site (see
`docs/CONTENT-GUIDE.md`).

## Updating ordering links

Each location's "Order" button links directly to that location's own URL
on the ordering platform (`menu-6161.orderexperience.net/...`). If a
location's ordering URL changes, update it everywhere that location's
button appears (`index.html`, `locations.html`, `menu.html`) — do not
consolidate multiple locations onto one shared ordering URL.

## Testing mobile layouts

Resize the browser below 820px (the breakpoint in `css/site.css`) and
confirm:

- The `.menu-toggle` button appears and opens/closes `.nav-links`.
- Grids (`.cards`, `.food-grid`, `.story-grid`, `.location`,
  `.footer-grid`, `.menu-items`) collapse to a single column.
- The Menu page's sticky jump bar (`.menu-jump`) doesn't overlap content.

## Validating sitemap changes

After adding or removing a page:

1. Add/remove the corresponding `<url>` entry in `sitemap.xml`.
2. Validate the file is well-formed XML (e.g. `python3 -c "import
   xml.dom.minidom as m; m.parse('sitemap.xml')"`).
3. Confirm every URL in the sitemap actually resolves to a real page.

## Testing 404 routing

Visit an unknown path (e.g. `/does-not-exist`) on the deployed site and
confirm `404.html` renders and the response status is 404 (check with
`curl -I` or browser dev tools — visually identical content served with a
200 status is not correct 404 behavior).

## Deployment checks

See `docs/DEPLOYMENT.md` for the full pre-deploy checklist.
