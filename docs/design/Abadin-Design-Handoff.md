# Abadin --- Design Workflow Handoff

## What this handoff is for

Start the next Abadin design-management chat from the current production
state without relying on the long historical conversation. The project
files and Figma are the working source of truth.

## Source-of-truth hierarchy

1.  `Abadin-PRD.md` --- authoritative for product behavior, scope,
    privacy, business rules, states and terminology.
2.  `abadin-visual-direction.md` --- approved Round 4 / «سازهٔ شناور» art
    direction.
3.  Approved Figma Design System + Composition System.
4.  `abadin-figma-design-SKILL.md` --- Claude design-execution rules.
5.  `abadin-senior-design-review-SKILL.md` --- ChatGPT review/gating
    rules.
6.  `Abadin-Design-Delivery-Tracker.md` --- operational delivery status;
    it does not override the PRD.

`APPROVED` is binding. `OPEN` must not be silently resolved. `LATER` is
outside MVP.

## Product essentials

Abadin is a Persian-first, RTL-first construction-material discovery and
supplier-comparison platform for Iran, serving B2B and B2C.

Core journey: Discover/Search → Product → Compare supplier offers →
Evaluate supplier → Contact supplier or open exact direct-product URL →
continue externally.

Abadin is not ecommerce: no cart, checkout, payment or completed-order
flow.

RFQ / «استعلام خرید عمده» is a separate multi-item inquiry capability,
not a direct-contact path to one selected supplier.

Critical rules: - Public supplier website is never shown; exact direct
product URL may be shown. - If an available offer has an exact
direct-product URL, show only that action, not supplier contact as
well. - Public supplier contact uses responsive mobile/messenger
channels only. - No supplier winner, unsupported
verification/trust/social proof, fake urgency or unsupported metrics. -
Unavailable offer/product shows no price, last price or price-update
time. - Public price update display is relative time only and must not
label data fresh/stale. - Product-card CTA remains «مقایسه فروشنده‌ها». -
Search/category/brand PLPs are grid-only. - Persian-first, Vazirmatn,
RTL, light theme, WCAG 2.2 AA target.

## Approved visual / creative direction

Round 4 «سازهٔ شناور» remains approved.

Operating model: - PRD → product truth and behavior. - Visual Direction
→ personality and art direction. - Composition System → page-level
visual grammar. - Design System → reusable implementation language. -
Review Skill → quality gate.

Principles: **Coherent, not identical.\
Creative, not decorative.\
Systematic, not formulaic.\
Modern, not trend-dependent.\
Calm, not boring.\
Distinctive, not distracting.**

The PRD is not a visual recipe. Unless it explicitly specifies a visual
constraint, visual execution is professional design territory.

Home and PDP are current minimum quality references, not templates.

Claude should independently detect monotony/template-like composition
and use appropriate composition, imagery, geometry, patterns/motifs,
layering, controlled overlap, meaningful elevation, tonal/solid
surfaces, data visualization, density changes and transitions.
Decoration must not substitute for composition. New reusable motifs may
evolve after validation.

## Working workflow

The operating loop is:

**ChatGPT defines task → Claude designs in Figma → Claude internal QA →
CLS review request → ChatGPT reviews actual Figma → revision if required
→ re-review → PASS → ChatGPT defines next task.**

Claude must not start the next dependent task while awaiting review or
after PASS. ChatGPT owns task sequencing and the review gate.

ChatGPT review order: 1. Product correctness / PRD. 2. Usability and
journey clarity. 3. RTL / responsive behavior. 4. Accessibility. 5.
Design System coherence. 6. Composition quality. 7. Creative /
art-direction maturity.

Review outcomes: - `PASS` --- scoped task becomes current production
baseline. - `CHANGES REQUIRED` --- Claude receives a concrete revision
task and resubmits.

Escalate to Product Owner only for genuine PRD OPENs, approved-source
contradictions, product-level behavior/capability changes, or
privacy/trust/contact/RFQ decisions. Routine visual execution is not an
owner escalation.

## Current delivery state

Closed/approved: - Phase A Foundations. - Phase B Base UI. - Phase C
Navigation/shared. - Phase D Domain Components. - Phase E Home and PDP
production migration. - Phase F Design System cleanup / canonical
production baseline. - PLP architecture for Search / Category / Brand. -
Category PLP Identity Header Refinement test.

### Latest workflow test --- PASS

Task: Category PLP identity/header refinement only.

Result: - Claude completed only the scoped Category identity area. -
Claude submitted exact Figma IDs. - Review returned `PASS`. - Claude
stopped and did not start another task. - Review rounds: `1`. - Owner
decision required: `No`.

Figma: - comparison board `363:22957` - Category 1440 `287:6766` -
Category 1280 `316:61586` - Category mobile `287:25245` - 360 test
`348:76292` - 320 test `348:77006` - changed Category variants `285:50`,
`348:58`, `285:19160`, `348:76185`

Follow-up: - Brand still has the older identity treatment. Handle only
when Brand is explicitly scoped. - Fixture QA: desktop Category count
says `۳۸ محصول`, mobile says `۲۱۴ محصول`; do not treat this as an owner
decision by default.

## Important canonical Figma references

Shared/domain: - ProductCard `33:154` - SupplierCard `33:376` - OfferRow
`228:420` - Offers Section `230:729` - Header/Desktop `194:9957` -
Header/Mobile `197:9862` - Footer/Desktop `212:10911` - Footer/Mobile
`213:1062` - Price `30:116` - Price Context `232:136` - Category Tile
`66:28`

Production references: - Home 1440 `243:488`; 1280 `243:16569`; mobile
`245:2075` - PDP 1440 `247:819`; 1280 `247:16251`; mobile `247:18223` -
Brand PLP `287:26416`; `316:62540`; `287:27394` - Composition System
page `326:2`

## Known unresolved / decision items

Do not silently resolve: - PLP FAQ vs Long Description ordering
conflict: current design direction uses FAQ before Long Description,
while recorded PRD text has Long Description before FAQ. - Offer
ordering within priced supplier group remains OPEN. - Future mixed-unit
price-filter behavior remains OPEN. - Mobile active-filter "clear"
interpretation remains an unresolved validation point.

QA, not automatically Product Owner decisions: - production contrast
remeasurement; - real category-image / brand-logo validation; - sample
fixture count consistency.

## Tracker

Use `Abadin-Design-Delivery-Tracker.md` as the operational dashboard.

Update it whenever: - a task is defined; - Claude starts; - a review
request arrives; - a review round completes; - a task becomes
Approved; - a blocker or owner decision appears; - the next task
changes.

Never use the tracker to override an APPROVED PRD decision.

## Next step

The next planned milestone is **Public Supplier Profile**. It has **not
started**.

Before Claude does any Supplier Profile work, ChatGPT should define the
first bounded task. The task must preserve: - no fake
rating/verification/social proof; - no public supplier website; - exact
direct-product URL/contact-action rules; - supplier product count is
allowed on its own page; - public mobile/responsive messenger contact
only; - supplier product listing integration; - no ecommerce
assumptions.

Apply the Composition System and creative-art-direction rules, but do
not clone Home or PDP.

## Current workflow override — 2026-10-01

Owner approved FAQ before Long Description on Category/Brand PLP; prior ordering conflict is resolved. Relative public price-update time is reconfirmed in PRD. Next milestone is Figma cleanup audit and bounded Claude cleanup BEFORE Public Supplier Profile. No cleanup PASS or Supplier Profile start yet.


## Responsive delivery policy — owner update 2026-10-05

This policy overrides any earlier instruction requiring a full-page design at every test width for future tasks.

- Required full-page deliverables: Desktop 1440 and Mobile 375 only.
- Widths 1280, 360 and 320 are responsive QA widths, not mandatory independent full-page deliverables.
- Test affected sections and relevant shared components at these widths. Record tested widths, findings and fixes; do not claim an unperformed test passed.
- Create an additional frame only when a real layout/interaction difference or a failure needs visual evidence. Prefer a section-level frame; use a full-page frame only when page-level composition requires it.
- Document intermediate-width rules: container sizing, gutters, columns, text wrapping and navigation/filter transitions. Do not infer that static frames prove behavior between widths.
- Do not duplicate every state at every width. Show unique states at component/section level unless the page composition or journey changes.
- Reuse approved shared components. Review changed areas and affected dependencies; avoid rereading entire historical review boards for a bounded revision.
- Existing approved production and stress frames remain historical/current evidence. This policy does not authorize deleting them, reopen their PASS, or change C0's In Review status.
- Apply this policy in future Claude task briefs and in both design-execution and review skills.