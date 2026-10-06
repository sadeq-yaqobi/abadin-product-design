# Milestone — Search Results

| Field | Value |
|---|---|
| Status | **Design Complete** — «PLP architecture for Search / Category / Brand» listed as Closed/approved in Abadin-Design-Handoff.md |
| Date | 2026-09-30 (later refinements 2026-09-30 / 2026-10-01) |
| Figma page | Search / Category / Brand `64:3200` |
| Detailed source | [`docs/design/design-system-notes.md`](../../../docs/design/design-system-notes.md) — «Milestone — Search / Category / Brand PLP», «PLP Content & Filter Closeout», «PLP Visual Coherence Refinement», «Shared Page Atmosphere + Filter Refinement Surface» |

> Index compiled from the sources above; no new facts are added.

## Frames
| Purpose | Frame |
|---|---|
| Desktop 1440 (filters active) | `285:23156` |
| Desktop 1280 (no filters, mixed card states) | `286:2927` |
| Mobile 375 (filters active) | `286:21992` |
| Mobile filter panel open | `286:22922` |
| Mobile sort sheet open | `286:23101` |
| No results for query 1440 / 375 | `286:23743` / `286:25482` |
| No results after filters 1440 / 375 | `286:24622` / `286:26128` |
| Stress 360 / 320 | `287:28917` / `287:29834` |
| 1280 template with Active Filters popover | `310:49488` |
| Filter QA sheet | `310:50436` |

Review board: «Review — Search / Category / Brand PLP» `289:26694` (left untouched per owner, C1).

## Shared architecture
Listing Context `285:19199` → Results Toolbar `58:278` → Product Grid rows → Pagination. Desktop filter panel 280 column; mobile full-screen filter panel + separate sort sheet (P1-15).

## Recorded closeout points
- Multi-category Search shows only general filters.
- Price filter is unit-aware; hidden in mixed-unit sets. Further mixed-unit behaviour is OPEN.
- Default sort: Search «مرتبط‌ترین».
- Products per page configurable; card counts in frames are illustrative.
