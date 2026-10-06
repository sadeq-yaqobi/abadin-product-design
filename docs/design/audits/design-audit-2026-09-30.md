# Abadin — Design Audit (Design System + Home / Search Results / Product Page)

Date: 2026-09-30 (۸ مهر ۱۴۰۵) · Author: Claude (own audit, not an independent Codex review) · Scope: read-only; nothing in Figma was changed.

Evidence base: live renders of Home — Desktop (68:3), Search Results — Desktop/Mobile (64:3202, 64:3549), Product Page — Desktop/Mobile (65:2, 65:4071); component sets ProductCard 33:154, OfferRow 35:311, Price 30:116; colour and radius variables read directly from the file.

Measured facts used below:
- background #f6f8f8, card #ffffff, muted #edf1f1, accent #edf7f6, border #dfe5e4, primary #0b6264, muted-foreground #55625f.
- Radius scale 4 / 6 / 8 / 12 / 16. Cards use 12, controls use 8.
- Type scale: Display 36, H1 28, H2 22, H3 18, H4 16, Body 14 (Large 16), Label 14/13, Caption 12, Price 18 (Large 28).
- Price strings use the Persian thousands separator U+066C «٬» correctly.

## 1. Verdict on the hypotheses

| # | Hypothesis | Verdict |
|---|---|---|
| 1 | Too uniform / repetitive | **Confirmed, mostly on Home and the PDP lower half.** Home is a stack of «heading + row of white bordered cards» five times. |
| 2 | Document / PDF / catalog feel | **Partly.** True for PDP (info column is a datasheet, then a second spec table) and Home. **Not true for Search Results**, which already reads as a marketplace. |
| 3 | Weak marketplace character | **Confirmed for Home** (zero products, zero prices on the homepage) and **PDP first viewport** (the decision block starts below the fold). Search is acceptable. |
| 4 | No recognizable identity | **Confirmed.** Logo Removal Test fails (see §4). |
| 5 | white + border + radius causes monotony | **Confirmed, but the cause is container overuse, not the border principle.** background vs card differ by ~3% luminance, so the border does all the separation work, and almost every section is put in a container. |
| 6 | Weak hierarchy in places | **Confirmed.** Compressed type scale; and an action-hierarchy inversion on the PDP (the only solid primary button is «ثبت نظر»). |
| 7 | DS forces one grammar | **Partly.** Foundations and primitives are fine; the problem is that there is no *composition* rule, so every template defaults to «card per section». Domain components also inherit shadcn-generic styling. |
| 8 | Long-session comfort | Current design is calm (good) but **inefficient**: low density in the product grid and a tall PDP. Calm is achieved, efficient is not. |
| 9 | Depends on good product images | **Confirmed risk.** ProductCard image ≈ 40% of card height; PDP gallery dominates the first viewport; category tiles rely on images. With mundane photos these areas become large, low-information blocks. |

Where I disagree with the initial critique:
- "Flat" is not the problem. Flatness and the borders-for-structure / shadows-for-elevation principle are correct and should stay.
- Search Results is the healthiest template: filters, chips, result count and grid communicate "search and compare". Its problems are density and card design, not identity.
- The most serious issues were not in the original critique: PDP information architecture (decision block too low, duplicated specs), PDP action hierarchy, and a Home page with no marketplace content.

## 2. Root cause by level

| Level | Problem | Severity |
|---|---|---|
| Foundations | Surface tokens give only ~2 usable levels (bg ≈ card); no "band"/sunken surface with real contrast; brand teal has no role beyond buttons/links; type scale steps too small; no numeric/price typographic role. | P1 (systemic) |
| UI Components | shadcn-derived visual defaults (outline button, pill badge, 8/12 radius) are generic; fine as primitives but they currently *are* the look. | P2 (systemic) |
| Domain Components | ProductCard and OfferRow are primitive assemblies with no domain-specific treatment (price/unit, availability, supplier line look like any SaaS row). ProductCard image-heavy; repeated full-width CTA. | P1 |
| Patterns | Offers Section wraps a table in a card and the price summary in another card; no column headers; no "many sellers" behaviour. | P1 |
| Template composition | No rule for when a section is open vs contained, so everything is contained; PDP ordering puts decision data low; Home has no product/price content. | P1 |

## 3. Findings (Evidence · Why · Systemic/Template · Priority · Direction)

**F1 — Container overuse (P1, systemic: Foundations + composition).**
Evidence: Home — categories, how-it-works, sellers and seller CTA are all white/border/radius-12 cards; PDP — price summary card, offers card, dashed reviews box. bg #f6f8f8 vs card #fff.
Why: every section has equal weight; the page reads as a list of boxes; nothing tells the eye where decisions happen.
Direction: a composition rule — content sits open on the page by default; containers only for interactive or comparable units (a product, an offer set, a form). Add a real "band" surface step for grouping instead of boxing.

**F2 — Compressed type hierarchy (P1, systemic: Foundations).**
Evidence: H2 22 / H3 18 / H4 16 / Body 14; section titles barely above content; hierarchy relies on weight and muted colour.
Why: first-glance comprehension and scanning suffer; everything feels mid-weight.
Direction: widen the scale at the top (page/section titles) and add a dedicated numeric role for prices/quantities (tabular figures, distinct size/weight), rather than more colour.

**F3 — PDP decision block below the fold (P1, template).**
Evidence (desktop 65:2): first viewport = gallery 420 px + 5-row spec table; price summary starts at ≈ y 750, offers at ≈ y 780; mobile: first price after ≈ 2 screens.
Why: the PDP's job is "compare sellers"; the user must scroll past a datasheet to reach it.
Direction: bring product identity + price summary together in the top zone; keep only 3–4 key specs up top; full spec table once, lower. Reduce the image share of the first viewport.

**F4 — Action hierarchy inversion on PDP (P1, template + pattern rule).**
Evidence: the only solid primary button on the PDP is «ثبت نظر» in the reviews empty state; all offer actions are outline; header RFQ is a filled secondary.
Why: the most visually urgent action is the least important one for the journey.
Direction: action-hierarchy rule per page. Offer actions stay equal to each other (PRD: no seller highlighted) but should be the strongest class on the PDP; the review CTA becomes secondary.

**F5 — Home has no marketplace content (P1, template).**
Evidence: 68:3 contains no product and no price; only category counts.
Why: a price-comparison product whose homepage shows no prices reads as a landing/about page.
Direction: design the data-backed states PRD §11 already allows ("محصولات پرجست‌وجو / کمترین قیمت‌های مشاهده‌شده / تغییرات قیمت — فقط با دادهٔ پشتیبان"), plus the empty fallback. This is PRD-supported, not a new feature.

**F6 — Identity fails the Logo Removal Test (P1, systemic).** See §4.

**F7 — ProductCard: image-dependent, CTA repetition, low density (P1, domain component).**
Evidence: card 264×400, image area ≈ 150 px; each card has a full-width outline «مقایسه فروشنده‌ها»; at 1280 ≈ 1.7 rows visible.
Why: mundane images waste the most visible area; six identical outline buttons create visual noise; low density slows 20–30-minute browsing.
Direction: shorter, fixed-ratio image well; stronger name/price block; whole card clickable with a lighter, consistent CTA treatment (the CTA text stays per PRD P1-8).

**F8 — Offer comparison is a list, not a comparison (P1, pattern).**
Evidence: Offers Section has no column headers; the price is not on a strong vertical rail; availability badge floats mid-row; no behaviour for 15+ sellers.
Why: comparison is the core task; scanning prices across rows should be effortless.
Direction: explicit columns and a price rail with tabular numerals; unavailable rows visually quieter by structure (not by time/age); a many-sellers behaviour (see recommendations).

**F9 — Footer closure is weak (P2, template/foundation).**
Evidence: footer muted #edf1f1 on page #f6f8f8 — nearly invisible boundary.
Direction: a dark footer is a reasonable exploration (see §6).

**F10 — Home hero is generic and search is duplicated (P2, template).**
Evidence: centered headline + subline + search; header search also visible.
Direction: hero can do more work (search + category entry + a live price example once data exists); hide header search on Home is an option.

**F11 — Mobile cost (P1, template).**
Evidence: PDP mobile — image 343 + specs before any price; offer cards ≈ 190 px tall each; four offers ≈ 900 px.
Direction: price summary right after identity; denser offer cards; a sticky decision affordance is worth exploring (recommendation).

**F12 — Category tiles rely on images (P2, domain).**
Direction: typographic/icon-led tiles that still work with no or poor imagery.

## 4. Logo Removal Test

Remove «آبادین» from Home, Search and PDP. What remains: Vazirmatn, a pale grey-green background, white bordered cards with 12 px radius, outline buttons, a teal primary button. This is the default look of a shadcn-based Persian dashboard. **Result: nearly nothing recognizable.**

Candidates that could become recognizable without heavy branding:
- a signature **price/unit lockup** (the «از ۲۴۵٬۰۰۰ تومان / کیسه» pattern set with a distinctive numeric style);
- a **measurement/ledger line language** (hairline rules, a start-edge rail, precise tick-like markers) — construction translated into "measure, structure, module", not concrete textures;
- **search as a signature object** (a recognizable search bar treatment);
- **technical-data presentation** (spec rows as a consistent, precise "ledger");
- **deliberate surface bands** (page rhythm by surfaces, not boxes);
- a **tone of voice** that is plain, exact and honest (already partly present: «قیمت مشاهده‌شده، نه قیمت قطعی خرید»).

## 5. Keep / Refine / Introduce / Avoid

**KEEP**
- Token architecture, semantic colour naming, light-only with dark-ready semantics.
- Brand teal #0b6264; Vazirmatn; Persian digits and «٬» separator (verified); RTL decisions (breadcrumb chevrons, wizard direction).
- Borders for structure, shadows only for real elevation.
- 44 px controls, focus rings, component property model.
- All PRD logic encoded in domain components: OfferRow §15 matrix, relative price time, availability without price, no counts, no «بهترین», RFQ privacy.
- Filter panel vs sort sheet split; Search Results overall structure.

**REFINE**
- Type scale (top steps) + a numeric/price role.
- Surface tokens: add one real band/sunken level; clarify when card vs band vs open.
- ProductCard (image ratio, density, CTA treatment).
- Offers Section (columns, price rail, many-sellers behaviour).
- PDP top composition and action hierarchy; single spec table.
- Home composition (data-backed product/price sections; less boxed how-it-works).
- Footer contrast/closure.
- Radius usage: fewer radii in play, slightly tighter on data surfaces for precision.

**INTRODUCE**
- Composition rules: "open by default, contain only interactive/comparable units"; "one dominant decision block per page"; action-hierarchy rule per template.
- Numeric typography role (tabular figures) and a price/unit lockup.
- A line/rail motif as the identity carrier (structure, measurement, module).
- Density guidance for browse/compare surfaces.
- Section bands for page rhythm.

**AVOID**
- Shadows on cards, gradients, coloured cards everywhere, decorative banners, carousels as default content.
- Construction clichés (concrete/brick textures, hazard stripes, cranes, helmets).
- Image-led layouts that only work with glossy photography.
- Using more teal as "identity"; any «بهترین/پیشنهاد ما/برنده» styling of a seller.
- Dense spreadsheet tables on mobile.

## 6. Dark footer
Useful as a closure anchor if (a) it is the *only* dark surface or one of very few, (b) it uses a deep teal-ink derived from the brand scale rather than pure black or grey, (c) link contrast meets AA. Risk: on long mobile pages it adds a heavy block; mobile footer should stay collapsed. Recommendation: include it in exploration, not decide now.

## 7. Product completeness
- PRD REQUIRED (not yet designed): PDP unavailable / no-sellers state with «موجود شد خبرم کن» (§14.5, P0-4B); unpriced-only state.
- PRD-supported conditional sections not designed: Home popular / lowest observed prices / price changes (§11); PDP related products, rating summary, guide content, price trend (§14.4) — "only with valid data" means the with-data design is still needed.
- PRODUCT RECOMMENDATION (needs owner approval): many-sellers behaviour on PDP (e.g. show N then expand); a sticky mobile decision bar / "jump to seller prices"; offer-list filter by delivery city (PRD has no such filter).
- OPEN DECISION (already recorded): order within available-priced offers.

## 8. Visual Directions

**A — Ledger («دفتر مقایسه»): data-first precision.**
Idea: the interface as a precise comparison ledger. Few containers; content open on the page; hairline rules and a start-edge rail; strong type scale; prices in a signature numeric lockup on a vertical rail.
Different: removes most cards; hierarchy from typography and rules, not boxes.
Why it fits: comparison is the core job; works with mundane images; calm and efficient for long sessions.
Risk: can feel austere or spreadsheet-like; needs careful spacing to stay friendly; weaker "delight".
Keep: tokens, components' logic, borders principle. Refine: type scale, OfferRow, ProductCard, PDP composition.

**B — Module («ماژول»): structure through surfaces and grid.**
Idea: pages built from visible modules on a strict grid; rhythm from surface bands (page / band / card) instead of borders on everything; tighter radii for precision; teal as a thin structural marker (active edges, section markers), not fills.
Different: introduces a real surface scale and band composition; geometry becomes the identity.
Why it fits: abstract reference to construction (module, layer, grid) without clichés; strong page rhythm; good for Home.
Risk: bands can become heavy or "blocky"; needs strict rules to avoid a new uniformity.
Keep: tokens architecture, components. Refine: surface tokens, radius usage, Home/PDP composition.

**C — Quiet Contrast («تضاد آرام»): light system with ink anchors.**
Idea: mostly light and calm, anchored by a few deep teal-ink surfaces at key moments (dark footer, header search band or PDP price summary) and large confident typography/numerals.
Different: adds a deliberate dark counterpoint; identity from ink surfaces + big numbers.
Why it fits: strongest immediate recognizability; clear visual closure.
Risk: dark blocks can tire the eye in long sessions and compete with content; needs a hard limit (e.g. max 2 per page) and AA checks.
Keep: most of the system. Refine: footer, header/search, price summary.

Author's lean (for the owner to decide): A as the base language, with B's surface-band rule for page rhythm, and C's dark footer as a single anchor to test.
