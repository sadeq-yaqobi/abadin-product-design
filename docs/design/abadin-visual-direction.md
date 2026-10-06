# Abadin — Approved Visual Direction

**Status:** APPROVED  
**Approved direction:** Round 4 — Modern Marketplace / «سازهٔ شناور»  
**Date:** 2026-09-30  
**Scope:** Public product experience and shared public-site visual language  
**Relationship to PRD:** This document governs visual and interaction direction. `Abadin-PRD.md` remains authoritative for product behaviour, scope, privacy, business rules, states and terminology.

---

## 1. Purpose

This document records the visual direction approved after the Abadin design explorations.

It exists to prevent future pages, components, reviews or AI-assisted design work from drifting back toward an older generic, document-like, overly restrained or purely minimal interface.

This is **not** a component specification. Exact tokens, variants, states and implementation details belong in the production Design System.

If this document conflicts with the PRD on product behaviour, the PRD wins. If the production Design System still contains an older visual rule that conflicts with this approved direction, the Design System should be migrated rather than using the older rule to undo the approved direction.

---

## 2. Design intent

Abadin should feel like a modern Persian marketplace for discovering products, comparing observed supplier data and deciding how to continue with a supplier.

The interface should be:

- easy to scan during repeated product-search and comparison work;
- visually distinctive without becoming noisy;
- modern and marketplace-oriented rather than document-like;
- comfortable during longer sessions without equating comfort with blandness;
- capable of using imagery, data visualization and architectural/material references as part of its identity;
- clear that Abadin compares and connects; it does not sell products itself.

The governing principle is:

> Visual richness is allowed. Visual noise that harms hierarchy, comprehension or task completion is not.

Abadin should be **coherent, not visually uniform**. Consistency comes from a shared visual language, interaction logic and product truth; it does not require identical page composition, repeated section recipes or conservative visual execution.

The PRD defines product truth and behaviour. Unless the PRD explicitly states a visual requirement, its silence on composition is **design freedom**, not an instruction to choose the simplest or safest layout.

---

## 3. Fixed foundations

- Persian-first and native RTL.
- `Vazirmatn` is the product typeface.
- Light theme for MVP.
- `WCAG 2.2 AA` target.
- Practical mobile touch targets should be at least 44px.
- Persian digits and correct Persian price/unit composition.
- Lines and borders provide structure and separation.
- Shadows are reserved for genuine elevation, floating hierarchy, hover/active elevation, menus, overlays and persistent floating surfaces rather than being applied to every card.

---

## 4. Visual language

### Brand anchor

Primary brand teal:

`#0B6264`

Supporting approved direction colors include:

- deep teal `#073F41`;
- teal mist `#E4F0EE`;
- ink `#111A19`;
- stone neutrals around `#475553` / `#62706E`;
- controlled copper accent `#C2703A`;
- darker copper for text where contrast is valid, around `#9A5526`;
- light copper `#F7D2B2`;
- mint accent on dark surfaces around `#7FD1C4`;
- sand `#FBF7F2`.

The exact production token mapping belongs in the Design System.

### Atmosphere

The default public experience is white-first.

A subtle teal/mist atmospheric gradient may appear near the top of pages and in selected compositions. Copper is an accent, not a competing primary brand field.

Do not make every section teal, tinted or card-based.

---

## 5. Geometry and composition

The approved concept is «سازهٔ شناور» — floating structure. Round 4 is an **art direction**, not a fixed recipe. It must not be reduced to repeatedly applying the same gradient, mist band, pipe ring, measuring arc, border or radius to every page.

Characteristics:

- rounded structural geometry;
- floating or elevated surfaces only where hierarchy justifies them;
- content-specific section composition instead of repeating the same white-card grammar everywhere;
- controlled architectural/material references such as joints, pipe sections, measuring arcs, structural lines or similar motifs;
- open white space combined with deliberate dense decision areas;
- large modules may use stronger radius than controls and nested elements.

The interface must avoid returning to:

- repetitive `Heading → text → white card` layouts;
- generic SaaS dashboards;
- static catalogue/PDF composition;
- excessive bordered boxes with identical radius and spacing;
- ecommerce semantics such as cart/buy/checkout.

Different content should use composition appropriate to its purpose. Product grids should remain highly scannable even when surrounding sections are more expressive.

Visual treatment should follow what a section is doing: discovery, identity, comparison, technical reference, education, evidence, navigation or a decision moment. This may justify different widths, alignments, density, surfaces, image relationships, geometry and transitions within the same coherent page.

Purposeful creative tools include, where appropriate:

- asymmetric composition;
- controlled overlap and layering;
- meaningful elevation;
- tonal or solid surfaces;
- atmospheric gradients;
- architectural or construction-inspired patterns and motifs;
- subtle texture and structural graphics;
- image-led composition and intentional cropping;
- typography used compositionally;
- data visualization;
- density changes and deliberate section transitions;
- whitespace used as an active compositional device.

These are tools, not a checklist. A strong composition comes first; decoration must never be used to disguise a weak layout.

---

## 6. Imagery

Real photography is part of the intended marketplace quality and should be used where it improves product recognition, category discovery, editorial value or atmosphere.

The system must also tolerate:

- ordinary construction-material photography;
- inconsistent crops;
- missing imagery;
- placeholders.

Weak imagery must not break hierarchy or core actions, but Abadin does not need to be visually independent from photography.

Round 4's final image/color balance remains pending validation with real placed product photography. This is a visual-validation task, not a blocker to the approved direction.

---


## 6A. Composition system and creative art direction

The production Design System is a shared language, not a page-template generator. A page can use every approved component and token and still be visually weak if its composition is generic, repetitive or assembled without art direction.

The **Composition System** is the layer between this Visual Direction and individual components. It translates Abadin's personality into page-level decisions about:

- hierarchy and rhythm;
- surface choice;
- density;
- image relationships;
- depth and elevation;
- section transitions;
- contrast between quiet and expressive areas.

Future page design should choose these decisions according to content purpose rather than mechanically reproducing an existing page. Home and PDP establish the current **minimum level of design maturity**; they are reference points, not templates to copy. PLP, Supplier Profile, landing pages and later public templates may introduce new compositions while remaining recognizably Abadin.

### Controlled variation

Long pages should avoid repeated sequences with the same width, alignment, surface, heading position, image ratio, spacing and density. Visual rhythm may move between quiet, dense, open and focused moments as the user journey changes. Variation must be purposeful rather than random.

Simplicity must not collapse into flatness, monotony or a generic marketplace aesthetic. Conversely, creativity must not become visual noise. Quiet areas are necessary so expressive moments retain meaning.

### Patterns, motifs and structural graphics

Patterns and motifs are allowed and encouraged when they strengthen the composition. Abadin is **not** permanently limited to the existing pipe-section rings or measuring arcs. New motifs may evolve from the world of construction, materials, measurement, structure, plans, grids, fabrication, surfaces, architecture or technical notation, including abstract interpretations.

A pattern is a supporting device, not proof of modernity. Adding a small pattern to an otherwise generic section does not make the section distinctive. If a section collapses visually when its decoration is removed, improve the composition first.

### Surfaces and elevation

Hierarchy does not require turning every section into a card. Use open atmosphere, tonal surfaces, solid fields, structural lines, image-led surfaces and bordered containment according to purpose.

Shadows remain reserved for meaningful elevation, but meaningful elevation may include a deliberately overlapping media object, sticky surface separating from scrolling content, floating control, menu, popover, sheet or overlay. The rule is not “avoid shadows”; it is “do not use shadows without a real depth relationship.”

### Evolution of the visual language

The visual system is allowed to mature. A successful new composition, motif, image relationship, transition or reusable pattern may become part of the Design System after validation. Future pages should not be forced back into older compositions merely because those compositions existed first.

The operating principles are:

> **Coherent, not identical.**  
> **Creative, not decorative.**  
> **Systematic, not formulaic.**  
> **Modern, not trend-dependent.**  
> **Calm, not boring.**  
> **Distinctive, not distracting.**

## 7. Data visualization and diagrams

Data visualization may be a signature device when the underlying data is valid and the visualization helps a decision.

Examples include price history and compact market-data modules.

Technical diagrams, application diagrams or enhanced product visuals are optional and data/content-dependent. They are not mandatory for every product category.

Do not invent technical content merely to fill a visual pattern.

---

## 8. Desktop header and navigation

The desktop header is one coherent two-level assembly.

### Level 1

Contains the brand, limited dedicated navigation, Search where applicable, RFQ entry when active, and authentication/account action.

### Level 2

Contains:

- «همهٔ دسته‌ها»;
- selected major categories;
- «بیشتر» when required by available width;
- برندها;
- فروشندگان.

The two levels are visually connected inside one rounded header assembly with a divider and subtle surface distinction. They should not read as two unrelated floating bars.

On Home at the top, Hero Search is primary and the header search slot is not duplicated. After the Hero leaves the relevant scroll area, Search may appear in the first header level. Internal discovery pages expose Search directly.

The category system must be data-driven and must not depend on exactly seven categories.

---

## 9. Desktop category menus

«همهٔ دسته‌ها» opens a scalable RTL mega menu with parent categories and the selected parent's relevant groups/children.

The menu must not contain:

- promotional banners;
- supplier promotion;
- unsupported counts;
- advertising placements.

«بیشتر» is a compact overflow menu containing only major categories that did not fit in the visible row. It is not a second mega menu.

Keyboard navigation, focus return and `Esc` closing are part of the interaction contract.

---

## 10. Mobile header and Search Row

The mobile header uses one stable brand position across page types.

- Abadin logo: fixed at the left edge and links Home.
- Right edge: menu on normal pages, Back on PDP/deep contexts where appropriate.
- Middle: intentionally quiet.
- Do not replace the logo with a page title or product title.
- Do not place Account in the mobile header.

Page titles belong in page content.

Search is a separate full-width Search Row below the header.

### Search Row ON by default

Use on discovery/browsing contexts such as:

- Search Results;
- Category;
- Brand;
- supplier product listings;
- similar product-discovery pages.

When ON, Search is immediately visible. It is not hidden behind a search icon.

### Search Row OFF

Current approved exceptions:

- Home, because Hero Search is primary;
- PDP;
- focused Landing Pages where persistent Search would waste vertical space or distract from the focused task.

---

## 11. Mobile persistent navigation

Normal mobile pages may use the standard Bottom Navigation according to the approved product/navigation rules.

The PDP is an exception.

### Mobile PDP

The PDP does **not** show the standard Bottom Navigation.

It uses one persistent bottom supplier-comparison bar containing:

- the displayable observed starting price when one exists;
- «مقایسهٔ فروشندگان».

The bar is stable while scrolling. It does not alternate with another bottom bar based on scroll direction.

The action is an in-page jump to the Supplier Offers section. It is not a Buy action and does not open a supplier directly.

If no price is displayable, omit the amount and retain «مقایسهٔ فروشندگان».

Hide the bar while the keyboard or a contact sheet is open.

---

## 12. Product page hierarchy

Supplier Offers are the primary decision/action area of the PDP.

Price history and other market context support that decision but must not visually overpower supplier comparison.

The current content order is:

1. product identity, gallery, compact key specifications and price context;
2. Supplier Offers;
3. compact price history when valid data exists;
4. product information and grouped specifications;
5. applications where data exists;
6. reviews;
7. related products;
8. footer.

Optional enhanced technical content must remain optional and data-dependent.

No seller should be visually presented as the winner, recommended supplier or preferred cheapest supplier unless a future approved product decision explicitly introduces such behaviour.

---

## 13. Product cards

Product cards prioritize scanning.

For public discovery contexts, preserve the approved product behaviour, including the comparison action «مقایسه فروشنده‌ها».

Do not add a direct shortcut that rewards or promotes the cheapest supplier.

Do not add seller counts where the PRD does not allow them.

Visual experimentation should happen around the grid and section composition before making every product card more complex.

---

## 14. Footer

The footer is part of Abadin's visual identity, not an afterthought.

The approved footer uses the architectural/structural skyline as an integrated background layer rather than a separate image strip.

A deep-teal tonal fade blends the skyline into the footer surface:

- the skyline remains recognizable in the upper/low-text area;
- the fade becomes stronger behind navigation and legal content;
- functional text must maintain measured accessible contrast;
- do not add opaque cards behind every footer column merely to solve contrast.

The footer retains its functional information architecture: product/category navigation, market links, guide/content, Abadin/support, official Abadin social channels when they exist, legal links and legitimate trust/regulatory marks when actually held.

On mobile, use an appropriate crop of the same visual without making the footer excessively tall.

The previously estimated contrast values from exploration are not acceptance measurements; production must measure contrast against the actual final background.

---

## 15. Motion

Motion is limited and purposeful.

Approved motion categories:

- subtle ambient/parallax edge elements where appropriate;
- functional micro-motion such as hover/focus/elevation transitions, menu/sheet transitions, search transition and chart tooltip behaviour.

Respect reduced-motion preferences.

Do not add decorative motion simply to make a page feel more dynamic.

---

## 16. Responsive direction

Desktop and mobile are separately designed experiences, not scaled copies.

Reference validation widths used during approval:

- Desktop: 1440;
- narrower desktop: 1280;
- Mobile: 375.

Future templates must stress-test long Persian labels, long product names, price/unit wrapping, keyboard states, sheets, fixed UI, safe areas and content density.

---

## 17. Sidebars

Do not introduce a general navigation/content sidebar on Home or PDP.

A sidebar remains appropriate where the task structurally requires it, such as desktop Search/PLP filtering.

---

## 18. Review guardrails

Visual review must consider not only component consistency and accessibility but also **creative/art-direction maturity**. A page may satisfy the PRD and use canonical components yet still require refinement if it feels generic, excessively uniform, template-generated or compositionally weaker than the approved quality baseline.

A reviewer should not reject a design merely because it is:

- visually rich;
- rounded;
- atmospheric;
- image-led;
- diagram-led;
- gradient-based;
- compositionally varied.

A reviewer should intervene when those choices:

- weaken hierarchy;
- slow comparison;
- obscure primary actions;
- reduce accessibility;
- introduce unsupported product claims;
- create ecommerce semantics;
- create excessive repeated motion;
- cause responsive or RTL failures;
- conflict with the PRD.

Likewise, consistency with an older Design System is not a reason to undo this approved direction. Systemic mismatches should be migrated into the production Design System.

The PRD must not be used to invent visual restrictions it does not contain. Creative freedom ends where a visual decision changes approved product behaviour, invents unsupported data or trust signals, harms privacy/accessibility, introduces unsupported actions or ecommerce semantics, or silently resolves an `OPEN` product decision. Within those boundaries, professional creative judgment is expected.

---

## 19. What is not fixed here

This document does not freeze every component, token or page composition.

The following belong elsewhere:

- exact component variants and state matrices → Design System;
- product behaviour and business rules → PRD;
- unresolved product decisions → PRD `OPEN` decisions;
- implementation details → engineering handoff;
- final logo/wordmark → separate brand/design decision.

The goal is coherent family resemblance, not identical composition on every page. The Visual Direction defines personality and quality; the Composition System defines page-level visual grammar; the Design System defines reusable implementation language; and the PRD remains authoritative for product truth and behaviour.
