# Supplier Listing / فهرست فروشندگان — Delivery record

Status: **Design Complete** (owner decisions, 2026-10-06). Supplier Registration and later milestones are NOT started.

## Figma IDs (file Qwx3QpLbhwbouq12QLvAL5)
- Page «Supplier Listing» 467:2:
  - Desktop 1440: 467:3
  - Mobile 375: 467:93947
  - Desktop states board 468:1560: A picker open · B filters applied · C no results · D no suppliers at all
  - Mobile states board 470:2028: G store-city sheet · H service-area sheet searching · I applied + expanded service area · J no results · K loading · L failure
  - Targeted validation board for 1280/360/320 (sections only): 471:2496
  - Doc: 472:2977 (marked Design Complete)
- New component: City Picker set 466:191 on page «City Picker» 466:2.
  - Variants: Layout=Popover|Sheet × State=Default|Searching|No match.
  - Properties: Show helper, Helper.
- Systemic update: SupplierCard 33:376.
  - Body + CTA layout with space-between; category tags wrap, up to 6 via `Show category 2–6`.
  - Service-area inline disclosure (`Show all-cities toggle`); `Brands text` property.
  - Only the CTA is a link.
  - Home's 6 instances are unchanged in size.

## Product decisions — CLOSED / APPROVED (2026-10-06)
1. **Store city vs service area.**
   - SupplierLocation and ServiceArea are two independent data sets and two independent filters.
   - The store city is never implicitly part of the ServiceArea. Example: a Tehran store that has not registered «تهران» appears for «شهر فروشگاه: تهران» but not for «ارسال به: تهران».
   - Service area uses only cities the supplier registered explicitly.
   - Active filters combine with AND.
2. **Default order:** alphabetical.
   - No hidden ranking by rating, reviews, product count, popularity, activity, featured status or similar.
   - No sort control.
   - Sample cards in 1440 and 375 were reordered alphabetically.
   - Implementation recommendation, not a product decision: fa collation, with names starting with a Latin letter after Persian names.
3. **City Picker options:** only cities that return at least one result.
   - «شهر فروشگاه»: cities with ≥1 public Active supplier located there.
   - «ارسال به»: cities that ≥1 public Active supplier explicitly registered in its ServiceArea.
   - Alphabetical; no counts, no popular cities, no ranking.
   - The in-picker search only narrows these options.
4. **Pagination:** yes; suppliers are not all loaded at once.
   - The page size is not fixed as a product decision.
   - The current Pagination is a design pattern only.
   - Every filter change returns to page 1.
5. **Category (CONFIRMED):** only Main Categories in the control.
   - A main category matches suppliers whose activity category is that category or any of its subcategories.
   - No subcategory selector.

## Accessibility requirement (recorded in component + doc)
- The «نمایش همهٔ شهرها» / «نمایش کمتر» toggle on SupplierCard keeps its current visual (Button Link Small, 36px).
- Its interactive hit area must be ≥ 44×44px, via padding or a pseudo-element, with no visual change.

## Remaining design assumption (not product)
Both city filters are single-select, following the site's single-select filter pattern.

## Responsive
- Viewport ≥1280 (validated at 1280 and 1440): 1200 container, 3 columns, gap 24.
- Recommended intermediate widths (no frames):
  - 1024–1279: 3 columns, fluid, gutter 32.
  - 768–1023: 2 columns.
  - 600–767: 2 columns; fields stacked; the picker opens in a sheet.
- Below 600 (validated at 375, 360 and 320): 1 column; full-width stacked fields.

## Related correction — Brand Listing
In Brand Listing Desktop `452:2`, the «برندها» Nav Link instance is now actually `State=Active`. The earlier report claimed this but the instance was still Default. Nothing else in Brand Listing was changed.
