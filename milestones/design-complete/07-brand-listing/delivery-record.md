# Brand Listing / فهرست برندها — Delivery record

Status: **Design Complete** (owner decision, 2026-10-06). Next milestone NOT started.

## Figma IDs (file Qwx3QpLbhwbouq12QLvAL5)
- Page «Brand Tile» 450:2:
  - Brand Tile set 450:49 (Logo=Image|None × State=Default|Hover|Focus; TEXT `Name#450:0`)
  - Brand Logo Placeholder set 454:92315 (Standard/Wide/Square/Tall/Low quality; a design-only stand-in for real logos)
- Page «Brand Listing» 450:3:
  - Desktop 1440: 452:2 (category filter row 459:1630)
  - Mobile 375: 453:91537 (category filter row 459:1683)
  - States board (empty · loading · failure · stress): 454:1278
  - Category filter states board (1440 + 375: selected; category with no brand): 460:1678
  - Targeted validation board for 1280/360/320 (grid + category filter; sections only): 455:1504
  - Doc: 456:1630

## Product decisions (APPROVED by Product Owner)
1. **Default order:** alphabetical.
   - No alphabetical index or jump navigation for now.
   - No ranking by popularity, product count, supplier count, or manual order.
2. **Pagination:** yes; brands are not all loaded on one page.
   - The exact page size is NOT fixed as a product decision.
   - The existing Pagination is a design pattern only.
3. **Category browsing/filter (new decision):** the user can narrow brands by one Category.
   - Default is «همهٔ دسته‌ها»; the control is single-select.
   - Selecting a category limits the grid to related brands.
   - Clear works through «همهٔ دسته‌ها», or through the Empty State action «نمایش همهٔ دسته‌ها».
   - If no brand relates to the category, show an Empty State.
   - Changing the category resets Pagination to page 1.
   - Not allowed: in-page search, sort control, PLP filter sidebar or sheet, and counts next to categories.

## Category filter — design
- Reuses Chip 26:115 (Toggle) as a single-select chip row, with radiogroup / aria-checked semantics.
- Desktop: one row, which scrolls horizontally if it overflows.
- Mobile: horizontal scroll that bleeds to the screen edge, with an edge fade; the selected chip is scrolled into view.
- Filter state is in the URL (suggested `?category=`).
- Assumption: the chips are the site's main categories, the same as the global nav. Sub-category level is not designed.

## Rules
- The tile shows only the logo and the name. The whole tile links to the Brand PLP.
- No counts, rating, popularity, or Official/Verified/Featured badges.
- The logo zone is a fixed 88px. The logo is contain-fit in a box of 70% width × 48, centred, never cropped or upscaled.
- No logo: surface-tint fill with a neutral glyph, no initials.
- Names wrap in full and are never truncated.
- Tiles in a row have equal height. An incomplete last row keeps the column width.
- Breadcrumb: خانه › برندها. On desktop the «برندها» nav item is Active. On mobile no Bottom Nav item is active.

## Responsive
- Viewport ≥1280 (validated at 1280 and 1440): 1200 container, 6 columns, gap 20.
- Recommended intermediate widths (no frames):
  - 1024–1279: 5 columns
  - 768–1023: 4 columns
  - 600–767: 3 columns
- Below 600 (validated at 375, 360 and 320): 2 columns, gap 12, gutter 16.
- Doc fix: the earlier «≥1024 = 5 columns» contradicted the validated 6 columns at 1280. It is now 1024–1279.
- At ≤360 a wide logo relies on contain-scaling; the placeholder is not scaled.

## States
- populated
- mixed logo / no logo
- long-name stress
- empty: «مشاهدهٔ دسته‌بندی‌ها»
- loading: skeleton
- failure: «تلاش دوباره»
- category selected
- category with no related brand: «نمایش همهٔ دسته‌ها»

## Correction log
2026-10-06: In Desktop `452:2`, the «برندها» Nav Link instance was still `State=Default`, although the delivery report said Active. It is now set to `State=Active`. This was the only change; nothing else in Brand Listing was touched.

## Technical note
Plugin API resizes on instance sublayers do not apply in this file. Logo shapes therefore use a nested variant instance that HUGs its content.
