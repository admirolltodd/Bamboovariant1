# Asset Guide — Variant 1

Documents where image assets live and how they're used. This does not
rename or move any existing file.

## Directories

| Directory | Contents |
|---|---|
| `images/brand/` | `bamboo-sushi-hibachi-logo-full.png` (used in header/footer and as the favicon reference) and `bamboo-sushi-hibachi-logo-full-outlined.png` (currently unused by any page) |
| `images/food/` | Dish photography used in the home page food-category tiles and gallery |
| `images/gallery/` | Storefront, signage and dining-room photography |
| `images/menu/` | Photographs of physical menu boards (gluten-free, vegan, sushi boat, weekly drink specials) |
| `images/awards/` | Community's Choice and Best of Florida award graphics |
| `images/press/` | Press clipping images (Northwest Florida Daily News) |

## Naming conventions already in use

Filenames are descriptive kebab-case (e.g.
`bamboo-sushi-hibachi-storefront-evening-800w.webp`), with a `-800w` suffix
marking a pre-sized responsive variant of a full-resolution image. This
variant does not currently use `srcset`/`sizes` to serve the `-800w` files
automatically — they exist on disk but each `<img>` tag references one
specific file directly. Do not rename these files; anything that reuses the
existing naming pattern will fit in without further changes.

## Assets that should not be renamed

Every file currently referenced by an `<img src="...">`, `<link
rel="icon">`, or CSS `background` in this repository. Renaming any of them
requires updating every page that references that filename.

## Content safety

Do not caption or rename an image with a specific dish name (e.g. "Volcano
Roll", "Spicy Tuna") unless the existing alt text or page copy in this repo
already names it. Several filenames in `images/food/` (e.g. `sunset.jpg`,
`volcano.jpg`) look like they may reference specific dishes, but the site's
current alt text for the images actually in use is generic ("Prepared
seafood dish", "Hibachi meal") — treat the literal filenames as internal
labels only, not as confirmed dish names to publish.

## Where future optimized images should go

Add new photography into the existing category folder that matches its
subject (`images/food/`, `images/gallery/`, etc.) rather than creating new
top-level image directories. If a new photo needs a smaller responsive
variant, follow the existing `-800w` suffix convention used elsewhere in
the same folder.
