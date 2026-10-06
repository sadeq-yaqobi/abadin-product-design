# Milestone — Product Page (PDP)

| Field | Value |
|---|---|
| Status | **Design Complete** — «Phase E Home and PDP production migration» listed as Closed/approved in Abadin-Design-Handoff.md |
| Date | 2026-09-30 |
| Figma page | Product Page `64:3201` |
| Detailed source | [`docs/design/design-system-notes.md`](../../../docs/design/design-system-notes.md) — «Round 4 — FINAL APPROVED VISUAL DIRECTION», «DS Migration — Phase D/E» |
| Visual direction | [`docs/design/abadin-visual-direction.md`](../../../docs/design/abadin-visual-direction.md) §11–§13 |

> Index compiled from the sources above; no new facts are added.

## Frames
| Width | Frame |
|---|---|
| Desktop 1440 | `247:819` |
| Desktop 1280 | `247:16251` |
| Mobile 375 | `247:18223` |

## Recorded behaviour
- Content order per Visual Direction §12: identity/gallery/key specs/price context → Supplier Offers → price history (valid data only) → product information → applications → reviews → related → footer.
- Mobile: no standard Bottom Nav; one persistent PDP Compare Bar (`233:24`) with optional price + «مقایسهٔ فروشندگان», in-page jump to Offers.
- Offers Section `230:729` / OfferRow `228:420`; actions per PRD §15, C-01.

## Known follow-ups in the sources
- OPEN: order within the available-priced offers group (see decision log).
- PRD-required PDP states not yet designed: fully unavailable / no sellers with «موجود شد خبرم کن», unpriced (design-system-notes «Remaining»; design-audit-validation §3).
- PDP reviews empty state exists only on the archive page as `151:8345` (figma-cleanup-log, C0 «Kept»).
- Side finding: PDP rating summary shows «بر اساس ۱۲ نظر», which conflicts with PRD §26 (supplier-profile notes).
