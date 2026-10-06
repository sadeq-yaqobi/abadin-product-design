# Abadin — Design Audit validation pass (2026-09-30)

Companion to `claude/design-audit-2026-09-30.md`. Read-only; nothing in Figma changed. Author: Claude.

## Status labels used
EVIDENCE = measured problem in the current renders · PRD = requirement with exact citation · APPROVED = explicit owner decision (dated) · REC = design recommendation · HYP = exploration hypothesis (not approved) · OPEN = unresolved decision.

## 1. Approval status of current foundations (conflict to resolve)
- On 2026-09-29 the owner wrote that token architecture, semantic colours, spacing, radius, sizing, typography, RTL-first and the border/shadow logic are approved, and chose brand colour #0b6264 (recorded in `claude/design-system-notes.md`).
- On 2026-09-30 the owner asked not to assume #0b6264, surfaces, radius or component styling are approved.
- Treatment in this pass: colour, surface treatment, radius, type scale and component styling are **reopenable pending owner confirmation**. Not PRD decisions (the PRD prescribes no visual system).
- Still approved / required: RTL-first (PRD §7.1), Vazirmatn (PRD §27), WCAG AA contrast, status not by colour alone, visible focus, Esc (PRD §27, FR-G-06), 44 px mobile targets (PRD §27), light theme only (PRD P1-25, §5.3), border/shadow principle (owner, reaffirmed 2026-09-30).

## 2. Refine / Introduce — classified
| Item | Class | Basis |
|---|---|---|
| Container overuse (bg #f6f8f8 ≈ card #fff; Home 4 of 6 sections boxed) | EVIDENCE | render + variables |
| Open-by-default composition rule | HYP | — |
| Type scale compressed (H2 22 / H3 18 / H4 16 / body 14) | EVIDENCE (observation) | text styles |
| Wider top scale + numeric/price type role | HYP | — |
| Extra surface level ("band") | HYP | — |
| PDP decision block below first viewport (summary ≈ y 750 of 2269; mobile ≈ 2 screens) | EVIDENCE | render |
| Move price summary to top zone / single spec table | REC | purpose from PRD §9.1, §14; order not specified by PRD |
| Duplicate spec rows (info column + technical specs) | EVIDENCE | render |
| PDP action inversion (only solid primary = «ثبت نظر») | EVIDENCE | render |
| Offer actions equal, no seller emphasised | APPROVED | owner 2026-09-29 (offer order); project principle "no supplier winner"; PRD RFQ-C2 applies to RFQ only |
| Offer actions as strongest class, review CTA secondary | REC | — |
| Home has no products/prices | EVIDENCE | render |
| Home popular / lowest observed / price-change sections | PRD (conditional permission) | §11 bullet 4: «فقط با دادهٔ پشتیبان نمایش داده شود» |
| Designing those sections now | REC | PRD permits, does not require |
| ProductCard image ≈ 150/400 px, repeated full-width CTA, ≈1.7 rows visible | EVIDENCE | render |
| Keep «مقایسه فروشنده‌ها» on every card | PRD | §12, P1-8 |
| Whole-card click, lighter CTA, shorter image well | REC | — |
| Offers table lacks column headers; weak price alignment | EVIDENCE (observation) | render |
| Column headers + price rail | REC / HYP | — |
| Wide tables become readable cards on mobile | PRD | §27 |
| Footer barely separates (#edf1f1 on #f6f8f8) | EVIDENCE | variables |
| Dark footer | HYP | — |
| Header + hero search both on Home | EVIDENCE | render |
| Hide header search on Home | REC | FR-G-01 only requires search to be available |
| Category tiles depend on images | EVIDENCE (risk) | render |
| Tighter radius on data surfaces, rail motif, ink surfaces | HYP | — |
| Persian separator «٬» | PRD, verified correct | FR-G-03 |

## 3. PRD claim validation
| Claim | Result | Citation |
|---|---|---|
| PDP fully-unavailable / no-seller state with «موجود شد خبرم کن» and related alternatives | PRD REQUIRED ✓ | §14.5 bullet 1; §18 P0-4B |
| Unpriced state without fabricated data or misleading action | PRD REQUIRED ✓ | §14.5 bullet 3; §14.2 offer states |
| No-review invitation | PRD REQUIRED ✓ (already designed) | §14.5 bullet 2 |
| Home data sections | Allowed, conditional ✓ | §11 |
| Magazine route on Home | Allowed (optional) ✓ | §11 «می‌تواند» |
| PDP related products, rating summary, guide content | Allowed, conditional ✓ | §14.4 bullet 3 |
| Price trend chart | Allowed, conditional ✓ (LTR time axis, text summary) | §14.4 bullets 1–2; §27 |
| "With-data design still needed" | **Downgraded → REC** | PRD permits, does not require |
| Order within available priced offers | OPEN ✓ — owner decision, not PRD | owner 2026-09-29; PRD §14.2/§25 only forbid time-based ordering |
| Many-sellers behaviour | PRODUCT RECOMMENDATION ✓ | PRD silent |
| Sticky mobile decision bar / jump to prices | PRODUCT RECOMMENDATION ✓ | PRD silent |
| Offer filter by delivery city | PRODUCT RECOMMENDATION ✓ | PRD silent (§5.1 goal 2 names location as comparison criterion, not a filter) |

## 4. Directions re-assessed (no winner)
See the chat reply of 2026-09-30 for the full A/B/C matrix (problems solved/unsolved, DS changes, comfort, SaaS/document risk, imagery, Home/Search/PDP effect, recognizability).

## 5. Smallest systemic experiment (3–5 changes)
1. Composition rule: open by default; containers only for interactive/comparable units (template/pattern; no token change).
2. Type scale: larger top steps + numeric/price role with tabular figures (foundation).
3. One additional contrasting surface level, tested with vs without (foundation).
4. Action-hierarchy rule per template (pattern/composition).
5. Comparison presentation: offer column headers + price alignment; compact ProductCard image ratio (domain).

## 6. Next milestone (proposed)
Slice: PDP Desktop decision zone (header → identity → price summary → offers table, ≈ first 1.5 viewports), plus a one-row Search Results slice (toolbar + 3 cards).
Fixed: PRD behaviour, content and copy, same product and same four §15 offer cases, 1280 viewport, Vazirmatn, RTL, border/shadow principle, brand colour (held constant to isolate structure), identical deliberately mediocre product image.
Varies: composition (boxed vs open), type scale, surface levels, action hierarchy, price/numeric treatment; ink/dark anchor only in C.
Set: current baseline + A + B + C side by side on a separate exploration page; templates untouched.
