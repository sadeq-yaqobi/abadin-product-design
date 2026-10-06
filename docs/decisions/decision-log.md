# Abadin — Product & Design Decision Log

This log is a **history** of important Product and Design decisions. It is **not** a second PRD.

- [`docs/product/Abadin-PRD.md`](../product/Abadin-PRD.md) remains the Product source of truth.
- Figma remains the source of truth for design output.
- If an entry changes product behaviour and is not yet in the PRD, its **PRD sync** column says `Required`. The PRD is only changed when the Owner explicitly asks. Open sync items are collected in [`prd-sync-queue.md`](prd-sync-queue.md).
- Entries are only added from recorded sources. Each row names its source.

**Status values:** `APPROVED` (Owner decision) · `CONFIRMED` (Owner confirmed an existing interpretation) · `RECORDED` (recorded design decision; explicit Owner approval not found in sources) · `OPEN` (unresolved — do not decide silently).

**PRD sync values:** `In PRD` · `Required` · `Recommended` (detail level; Owner to decide) · `N/A` (visual / process / design-system only).

| ID | Date | Decision | Status | Milestone | Figma nodes | PRD sync | Source |
|---|---|---|---|---|---|---|---|
| DL-001 | 2026-09-29 | One default avatar for users and stores; never first-letter initials | APPROVED | Design System | Avatar `30:56` | In PRD (FR-G-07, P1-23) | design-system-notes «Direction» |
| DL-002 | 2026-09-29 | RFQ response general terms (delivery time, shipping, formal invoice, notes) are all optional; only price validity is required (default «۲۴ ساعت») | APPROVED | Design System (RFQ) | RFQ Response Terms `40:156` | In PRD (§19.6, RFQ-O4/O5) | design-system-notes «Direction» |
| DL-003 | 2026-09-29 | Sort options: «مرتبط‌ترین» (default), «کمترین قیمت», «بیشترین قیمت»; never a «بهترین قیمت» claim | APPROVED | Search | Sort Sheet `58:151` | Recommended (PRD §12 allows sorting; options not listed) | design-system-notes «Pattern decisions» |
| DL-004 | 2026-09-29 | OTP length is not fixed in the design system (4–6 cells); final value from SMS provider | APPROVED | Design System | OTP Input `58:2885` | N/A | design-system-notes |
| DL-005 | 2026-09-29 | Buyer inquiry tabs «مقایسهٔ پاسخ‌ها / فهرست اقلام / فایل‌ها» approved for now | APPROVED | RFQ (planned) | `62:3318` | N/A | design-system-notes |
| DL-006 | 2026-09-29 | No purchase/buyer-type field in RFQ until a routing use is defined | APPROVED | RFQ (planned) | RFQ Create Step `62:485` | In PRD (§19.3 conditional) | design-system-notes |
| DL-007 | 2026-09-29 | Available priced offers may come first; order **within** that group | **OPEN** | Product Page | Offers Section `230:729` | Required when decided | design-system-notes; Handoff «Known unresolved» |
| DL-008 | 2026-09-30 | Round 4 «سازهٔ شناور» approved as Abadin's visual direction | APPROVED | Visual Direction | Archive `126:2` | N/A (PRD D-02) | abadin-visual-direction.md |
| DL-009 | 2026-09-30 | Header search after scroll on Home; mobile PDP persistent «مقایسهٔ فروشندگان» bar (no Bottom Nav on PDP) | APPROVED | Home / Product Page | Header `194:9957`, Compare Bar `233:24` | N/A (Visual Direction §8, §11) | design-system-notes «Convergence pass» |
| DL-010 | 2026-09-30 | DS migration D1 add + remap primitives; D2 warning stays amber; D3 ink Button variant; D4 Search/PLP visual migration deferred | APPROVED | Design System | Foundations `184:8949` | N/A | design-system-notes «Phase A» |
| DL-011 | 2026-10-01 | Category/Brand PLP order: grid → pagination → FAQ → long description → footer | APPROVED | Category / Brand PLP | `64:3200` | In PRD (P1-17, owner record ۹ مهر ۱۴۰۵) | Handoff «workflow override 2026-10-01»; PRD |
| DL-012 | 2026-10-01 | Public price-update time is relative only | APPROVED | All | Price `30:116` | In PRD (P1-12) | PRD owner record |
| DL-013 | 2026-10-05 | Responsive delivery: full pages at 1440 and 375; 1280/360/320 only as targeted validation; existing frames kept | APPROVED | Process | — | N/A | Handoff «Responsive delivery policy»; working-rules |
| DL-014 | 2026-10-05 | Tasks come directly from the Owner; no ChatGPT/CLS review step | APPROVED | Process | — | N/A | working-rules (supersedes Handoff «Working workflow») |
| DL-015 | 2026-10-06 | Supplier showcase shows available and unavailable products, newest → oldest only; availability never affects order | APPROVED | Supplier Profile | `375:134`, `375:91298` | **Required** | supplier-profile delivery record |
| DL-016 | 2026-10-06 | Supplier rating shown with ≥1 valid published review; hidden otherwise; review count never public | APPROVED | Supplier Profile | Supplier Identity `375:133` | **Required** (threshold); count rule In PRD (§26) | supplier-profile delivery record |
| DL-017 | 2026-10-06 | Only `Active` suppliers have a public profile; no public page or message for Pending Review, Needs Correction, Cannot Be Activated, Paused, Suspended | APPROVED | Supplier Profile | removed board `432:5349` | **Required** (PRD §16.2 still lists «توقف موقت و وضعیت‌های غیرفعال» states) | supplier-profile delivery record |
| DL-018 | 2026-10-06 | C1 cleanup of page `64:3200` closed; review page `289:26694` left untouched | APPROVED | Figma cleanup | see cleanup log | N/A | figma-cleanup-log |
| DL-019 | 2026-10-06 | Brand Listing default order alphabetical; no alphabetical index; no ranking by popularity, product count, supplier count or manual order | APPROVED | Brand Listing | `452:2`, `453:91537` | **Required** | brand-listing delivery record |
| DL-020 | 2026-10-06 | Brand Listing is paginated; page size not fixed as a product decision | APPROVED | Brand Listing | Pagination `45:267` | **Required** | brand-listing delivery record |
| DL-021 | 2026-10-06 | Brand Listing gets a single-select Category filter (default «همهٔ دسته‌ها», no counts, clear, empty state, resets to page 1); no search, sort or PLP filter panel | APPROVED (new) | Brand Listing | `459:1630`, `459:1683`, `460:1678` | **Required** (PRD §13 / P1-18 describe browse-only) | brand-listing delivery record |
| DL-022 | 2026-10-06 | Supplier Listing: SupplierLocation and ServiceArea are independent filters; store city is never implicitly part of the service area; only explicitly registered cities count; filters combine with AND | APPROVED | Supplier Listing | `467:3`, `467:93947` | **Required** (clarifies §16.1, P0-3A/P0-3D) | supplier-listing delivery record |
| DL-023 | 2026-10-06 | Supplier Listing default order alphabetical; no hidden ranking (rating, reviews, product count, popularity, activity, featured); no sort control | APPROVED | Supplier Listing | `467:93195` | **Required** | supplier-listing delivery record |
| DL-024 | 2026-10-06 | City Picker lists only cities with ≥1 result (store city: located Active suppliers; «ارسال به»: explicitly registered ServiceArea); alphabetical; no counts, popular cities or ranking | APPROVED | Supplier Listing | City Picker `466:191` | **Required** | supplier-listing delivery record |
| DL-025 | 2026-10-06 | Supplier Listing is paginated; page size not fixed; any filter change returns to page 1 | APPROVED | Supplier Listing | Pagination `45:267` | **Required** | supplier-listing delivery record |
| DL-026 | 2026-10-06 | Supplier Listing category control shows Main Categories only; a selection matches suppliers in that category or its subcategories; no subcategory selector | CONFIRMED | Supplier Listing | `467:571` | **Required** | supplier-listing delivery record |
| DL-027 | 2026-10-06 | SupplierCard «نمایش همهٔ شهرها» keeps its visual size; hit area ≥ 44×44px | APPROVED | Supplier Listing | SupplierCard `33:376` | In PRD (§27 general) | supplier-listing delivery record |
| DL-028 | 2026-10-06 | Nav Link Active state uses a single indicator line (duplicate full-width underline removed) | APPROVED | Design System | Nav Link Active `47:50` | N/A | Owner request in session 2026-10-06 |
| DL-029 | 2026-09-30 | Search/PLP closeout: multi-category Search shows general filters only; unit-aware price filter hidden in mixed-unit sets; Category/Brand default sort label «پیش‌فرض»; products per page configurable | RECORDED | Search / PLP | `64:3200` | Recommended | design-system-notes «Closeout pass» |
| DL-030 | 2026-09-30 | Future mixed-unit price-filter behaviour | **OPEN** | Search / PLP | — | Required when decided | design-system-notes; Handoff |
| DL-031 | 2026-09-30 | Product review rating display threshold / moderation (Round 4 note) | **OPEN** | Product Page | — | Required when decided | design-system-notes «Convergence pass» |
| DL-032 | 2026-09-30 | Optional enhanced product content ownership / conditions | **OPEN** | Product Page | — | Required when decided | design-system-notes «Convergence pass» |
| DL-033 | — | Mobile active-filter «clear» interpretation — validation point | **OPEN** | Search / PLP | — | — | Handoff «Known unresolved» |

## How to add an entry
1. Add a row with the next `DL-` number, the decision date, and the source.
2. If it changes product behaviour and is not in the PRD, set PRD sync to `Required` and add it to [`prd-sync-queue.md`](prd-sync-queue.md).
3. Never edit an old row's meaning. If a decision is replaced, add a new row and mark the old one «superseded by DL-xxx» in its Decision cell.
