# Abadin — Product & Design documentation

**Abadin / آبادین** is a Persian-first, RTL-first platform in Iran for discovering construction-material products, comparing observed supplier prices, evaluating suppliers and contacting them. It serves B2B and B2C buyers. Abadin is not an ecommerce marketplace: there is no cart, checkout or payment. «استعلام خرید عمده» (RFQ) is a separate multi-item inquiry capability.

This repository keeps the **source-controlled documentation and history** of Abadin's product and design work. It does not replace Figma.

## Sources of truth

| Area | Source of truth | In this repo |
|---|---|---|
| Product behaviour, scope, rules | [`Abadin-PRD.md`](docs/product/Abadin-PRD.md) | Copy, synced with the Claude Project PRD (Owner-approved update 2026-10-07: `P0-4D`) |
| Visual direction | [`abadin-visual-direction.md`](docs/design/abadin-visual-direction.md) | Copy, unchanged |
| Design output | **Figma** — [Abadin — Design System](https://www.figma.com/design/Qwx3QpLbhwbouq12QLvAL5) | Node references only ([index](docs/figma/figma-node-index.md)) |
| Decision history | [Decision log](docs/decisions/decision-log.md) | History only — not a second PRD |

`APPROVED` is binding · `OPEN` is never decided silently · `LATER` is outside MVP.

## Milestone status

| Milestone | Status |
|---|---|
| [Design System foundation (Phases A–F)](milestones/design-complete/01-design-system-foundation/delivery-record.md) | ✅ Design Complete |
| [Home](milestones/design-complete/02-home/delivery-record.md) | ✅ Design Complete |
| [Product Page](milestones/design-complete/03-product-page/delivery-record.md) | ✅ Design Complete |
| [Search Results](milestones/design-complete/04-search/delivery-record.md) | ✅ Design Complete |
| [Category PLP](milestones/design-complete/05-category-plp/delivery-record.md) | ✅ Design Complete |
| [Brand PLP](milestones/design-complete/06-brand-plp/delivery-record.md) | ✅ Design Complete (architecture) |
| [Brand Listing](milestones/design-complete/07-brand-listing/delivery-record.md) | ✅ Design Complete |
| [Supplier Listing](milestones/design-complete/08-supplier-listing/delivery-record.md) | ✅ Design Complete |
| [Public Supplier Profile](milestones/design-complete/09-supplier-profile/delivery-record.md) | ✅ Design Complete |
| [Supplier Registration / Onboarding](milestones/design-complete/10-supplier-registration/delivery-record.md) | ✅ Design Complete |
| [Brand PLP identity consistency](milestones/delivered/brand-plp-identity-consistency/delivery-record.md) | 📦 Delivered — Owner approval not recorded |
| [Planned items](milestones/planned/README.md) (buyer account, RFQ, seller panel…) | 🗓 Planned |

Details: [Design Delivery Tracker](docs/delivery/design-delivery-tracker.md).

## Repository map

```
README.md
CONTRIBUTING.md                     milestone & commit workflow
docs/
  product/Abadin-PRD.md             product source of truth
  decisions/
    decision-log.md                 history of important decisions
    prd-sync-queue.md               approved decisions not yet in the PRD
  delivery/design-delivery-tracker.md
  design/
    abadin-visual-direction.md
    Abadin-Design-Handoff.md
    composition-system.md
    design-system-notes.md
    working-rules.md
    audits/                         design audits & DS migration audit
  figma/
    figma-node-index.md
    figma-cleanup-log.md
    figma-cover-script.md
skills/
  abadin-figma-design/SKILL.md
  abadin-senior-design-review/SKILL.md
milestones/
  design-complete/                  approved milestones
  delivered/                        delivered, awaiting approval
  planned/
```

## Notes on the copied documents
- All files in `docs/product`, `docs/design`, `docs/figma`, `skills/` and the four original milestone notes are **verbatim copies** of the Claude Project files as of 2026-10-06. Exceptions: `Abadin-PRD.md` was updated on 2026-10-07 by Owner instruction (`P0-4D`, no self-service account deletion; same change made in the Claude Project); the «Design widths» section of [`working-rules.md`](docs/design/working-rules.md) was later aligned with the final responsive policy.
- `Abadin-Design-Handoff.md` describes an older ChatGPT task/review workflow. It was later replaced by [`working-rules.md`](docs/design/working-rules.md) (tasks come directly from the Owner; no ChatGPT review). The file is kept unchanged as history.
- [`abadin-senior-design-review/SKILL.md`](skills/abadin-senior-design-review/SKILL.md) was written for that earlier review gate.
