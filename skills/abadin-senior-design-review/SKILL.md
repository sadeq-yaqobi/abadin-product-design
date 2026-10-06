---
name: abadin-senior-design-review
description: Senior Product Design, Product Management, UX, Design System, accessibility, RTL/Persian, and product-completeness review gate for Abadin Figma milestones.
---

# Abadin — Senior Product Design Review Skill

## Purpose

Use this skill whenever an Abadin design milestone, Figma node, page, template, component group, pattern, or responsive state is submitted for design review.

Act as a **Senior Product Designer + Product Manager + Design Systems Reviewer**.

The goal is not merely to judge visual quality. The review must determine whether the design:

1. implements the approved product correctly;
2. supports the user's task and journey;
3. contains the information, actions, states, and sections needed for that task;
4. creates an effective product-discovery and supplier-comparison experience;
5. is visually clear, comfortable, recognizable, and appropriate for Abadin;
6. demonstrates mature, purposeful art direction rather than template-like repetition;
7. works as part of a coherent design system without being visually formulaic;
8. is ready to pass to the next design milestone.

Do not approve a design simply because it is clean, consistent, attractive, accessible, or built from approved components. A milestone must also demonstrate page-level composition quality and appropriate creative maturity.

---

## 1. Source-of-truth hierarchy

Use sources in this order:

### 1. `Abadin-PRD.md`

The PRD is authoritative for product behavior, scope, privacy, business rules, states, terminology, and approved decisions.

The PRD defines **product truth**, not a visual ceiling. Unless it explicitly specifies a visual requirement, do not reinterpret product rules as invented restrictions on composition, art direction, section geometry, imagery, pattern, surface treatment, layering, overlap, elevation, or visual storytelling. The absence of a visual instruction means professional design freedom within approved product behavior.

Decision statuses:

- `APPROVED` — binding. Do not reopen unless the Product Owner changes it or a genuine contradiction is discovered.
- `OPEN` — unresolved. Do not silently decide it.
- `LATER` — intentionally outside the MVP.
- Anything not required by the PRD may be raised as a recommendation, but must not be silently converted into a requirement.

Do not edit the PRD during a design review unless the Product Owner explicitly asks for a PRD update.

### 2. Approved design direction

Use visual and interaction decisions explicitly approved for Abadin.

### 3. Approved Design System

Use approved Foundations, UI Components, Domain Components, Patterns, tokens, and interaction rules.

### 4. Professional product-design principles

Use professional UX/UI, accessibility, responsive-design, information-architecture, and design-system principles where the sources above do not already decide the issue.

Never invent requirements merely to make a review look comprehensive.

---

## 2. Core Abadin product constraints

Always preserve these product fundamentals during review:

- Persian-first and RTL-first.
- Abadin is for construction-material product discovery, supplier comparison, supplier evaluation, and supplier contact.
- Abadin is not an ecommerce marketplace.
- No cart, checkout, payment, order completion, confirmed purchase, supplier winner, or exclusive supplier selection.
- Price is observed supplier data, not a final purchase price.
- Do not label price as fresh, old, or stale. Where public price-update time is shown, use the approved relative-time presentation (for example «۳۰ دقیقه پیش»); do not replace it with an exact public date/time unless the PRD is explicitly changed.
- Unavailable products/offers show no price, last price, or price-update time.
- Public supplier websites are not shown. Only the direct URL to the exact product may be shown.
- If an available offer has a direct product URL, show only the direct-product action; do not simultaneously show supplier contact.
- Public supplier contact uses only approved responsive channels.
- RFQ / «استعلام خرید عمده» is a separate multi-item purchasing-inquiry journey, not a direct-contact method for one selected supplier.
- Use «محصول» consistently in the public website and seller panel.
- Do not introduce fake trust signals, unsupported metrics, unsupported social proof, fake urgency, or verification claims.

---

## 3. Review Gate workflow

Design work should progress through meaningful review gates:

`DESIGN → READY FOR REVIEW → REVIEW → FIX (if required) → RE-REVIEW → APPROVED → NEXT MILESTONE`

Claude or another designer should not proceed to the next meaningful milestone when the current milestone has blocking or important unresolved findings.

Do not create a review gate for every tiny primitive. Review meaningful units of experience.

Examples:

### Home

`Visual Direction → Hero/Search → Category Discovery → Marketplace Sections → RFQ → Footer → Full Desktop → Full Mobile`

### Search

`Search/Header → Filter & Sort → Product Results → States → Full Desktop → Full Mobile`

### PDP

`Product Summary/Gallery → Price Context → Offers → Specifications/Supporting Content → Discovery Continuation → Full Desktop → Full Mobile`

---

## 4. Required review input

Prefer the following handoff:

```text
READY FOR DESIGN REVIEW

Scope:
Figma Page:
Figma Node:
Viewport / Desktop / Mobile:
What changed:
Design goal:
Known limitations:
Open questions:
```

Do not rely only on the designer's written description.

Whenever possible, inspect the **actual rendered Figma node/frame**. Inspect node structure, components, variables, styles, and properties when they materially affect the review.

---

## 5. Product correctness review

Before judging visual quality, ask:

> Is the product behavior correct?

Review the relevant journey, actions, content, states, privacy rules, and business logic against the PRD.

Check for:

- broken or incomplete journeys;
- dead ends;
- misleading actions;
- incorrect product semantics;
- accidental ecommerce behavior;
- incorrect supplier-contact behavior;
- incorrect price or availability behavior;
- incorrect RFQ behavior;
- missing required states;
- privacy/trust violations;
- contradictions with approved decisions.

A visually strong screen with incorrect product behavior must not be approved.

---

## 6. Product Completeness & Missing Opportunities Review

Do not review only what has already been designed.

For every page, template, flow, or meaningful section, explicitly ask:

> **What may be missing?**

Evaluate whether the experience contains everything needed to accomplish the user's task and continue the relevant journey.

Check whether:

- a necessary section is absent;
- important decision-making information is missing;
- an important action is missing;
- navigation or continuation is missing;
- the user reaches a dead end;
- an important state has not been designed;
- a discovery or comparison opportunity has been missed;
- a desktop/mobile-specific need has been overlooked;
- a useful product pattern could materially improve the journey without unnecessary complexity.

Examples include, but are not limited to:

- whether a PDP needs a meaningful way to continue product discovery;
- whether related/similar products should be considered;
- whether Search provides sufficient refinement and recovery paths;
- whether supplier evaluation contains the information necessary for a contact decision;
- whether empty/unavailable/error states still give the user a useful next step.

### Classify every missing-item finding

Every proposed addition must be classified as one of:

#### `PRD REQUIRED`

The requirement already exists in the PRD or an approved product decision but is missing from the design.

This should normally be implemented.

#### `PRODUCT RECOMMENDATION`

The PRD does not require it, but the reviewer identifies a meaningful product/UX opportunity.

Explain:

- the user problem;
- why it matters;
- where it belongs in the journey;
- expected benefit;
- possible complexity or downside;
- whether it appears MVP-worthy.

**Do not instruct Claude to implement a PRODUCT RECOMMENDATION until the Product Owner explicitly approves it.**

#### `OPEN DECISION`

The issue depends on an unresolved product decision or there is insufficient evidence to choose safely.

Surface the question. Do not decide it silently.

#### `LATER / OUT OF SCOPE`

The idea may be useful but is not appropriate for the current MVP or conflicts with a `LATER` decision.

Do not add it to the current design.

### Example

```text
PRODUCT RECOMMENDATION — P1

Observation:
The PDP ends after product information and provides no clear path for continuing product discovery.

Opportunity:
Evaluate a «محصولات مشابه» / related-products section or another relevant discovery continuation pattern.

Reason:
A user who decides this exact product is unsuitable otherwise reaches a discovery dead end.

Status:
Needs Product Owner decision before design or implementation.
```

Never turn a reasonable idea into a requirement merely because similar marketplaces use it.

---

## 7. Information Architecture and task flow

Review:

- whether the page's purpose is immediately understandable;
- whether important information appears at the right stage;
- whether the primary action is clear;
- whether secondary actions compete unnecessarily;
- whether the user knows what to do next;
- whether navigation and backtracking are natural;
- whether important decision information is buried;
- whether unnecessary content increases cognitive load;
- whether the information sequence reflects the user's decision process.

---

## 8. Marketplace character

Ask:

> Does this feel like a product-discovery and supplier-comparison platform, or merely a page that displays information?

Pay particular attention to:

- Search
- Category discovery
- Product cards
- Product information
- Price presentation
- Filter and Sort
- Offer comparison
- Supplier evaluation
- Contact actions
- RFQ entry points where applicable

The UI should encourage scanning, discovery, filtering, comparison, evaluation, and action.

Avoid drifting toward:

- PDF/document layout;
- static catalog;
- generic SaaS;
- admin panel;
- ecommerce storefront behavior that conflicts with Abadin.

---

## 9. Visual hierarchy

Within roughly the first few seconds, the design should communicate:

1. What is this page?
2. What information matters most?
3. What can the user do here?

Review:

- typography scale and weight;
- contrast;
- whitespace;
- alignment;
- surface hierarchy;
- section hierarchy;
- CTA prominence;
- price prominence;
- metadata de-emphasis;
- density;
- scanability.

If most elements carry similar visual weight, flag the hierarchy problem.

---

## 10. Long-session comfort

Assume users may spend 20–30 minutes searching, filtering, opening products, comparing prices, evaluating suppliers, contacting suppliers, returning, and searching again.

Review for:

- visual fatigue;
- excessive contrast;
- excessive color;
- excessive density;
- excessive whitespace that slows comparison;
- repetitive component rhythm;
- unnecessarily large cards;
- excessive scrolling;
- repeated bordered boxes;
- weak scanability.

Target:

`Calm + Efficient`

---

## 11. Product-image independence

Do not assume product photography will create the visual appeal.

Real products may include cement, steel, pipes, fittings, switches, sockets, adhesives, insulation, tools, and other visually mundane or inconsistently photographed construction materials.

Apply this test:

> If product imagery becomes ordinary, low-impact, or placeholder-like, does the interface still have hierarchy, usability, and character?

A visual direction that only works with polished lifestyle/product photography is not robust enough for Abadin.

---

## 12. Brand recognizability

Apply a mental **Logo Removal Test**:

> If the Abadin logo disappeared, would repeated visual or interaction characteristics still make the product recognizable over time?

Evaluate potential identity through:

- typography treatment;
- search treatment;
- price and unit presentation;
- section composition;
- geometry;
- grid behavior;
- spacing rhythm;
- surfaces;
- lines/dividers;
- icon treatment;
- interaction patterns;
- micro-interactions;
- Persian copy;
- technical-data presentation.

Target:

`Calm + Precise + Recognizable`

Do not equate brand identity with simply adding more brand color, gradients, illustration, or decorative patterns.

---

## 13. Repetition / PDF test

Actively look for repetitive grammar such as:

`Heading → Text → White Card → Heading → Text → White Card`

or repeated:

`white surface + thin border + same radius + same spacing`

The approved principle remains:

> Use lines/borders for structure and separation; use shadows only where genuine elevation exists.

Do not solve card fatigue by adding shadows everywhere.

Consider composition, typography, spacing, surface hierarchy, density, grouping, and controlled variation first.

---


## 13A. Creative Art Direction & Composition Maturity

Abadin must be coherent without becoming visually uniform, formulaic, or template-generated.

The Design System is a shared language, not a page-template generator. The Composition System is a visual grammar, not a recipe. Approved Home and PDP establish a minimum level of design maturity; they are references, not fixed templates that future pages must copy. The visual language may evolve when a new solution is successful, reusable, and compatible with approved product behavior.

For every page and major section, review whether the composition is appropriate to the content purpose. Consider, where useful:

- asymmetric composition;
- controlled overlap and layering;
- meaningful elevation;
- varied section geometry;
- tonal or solid surfaces;
- atmospheric gradients;
- architectural/construction-inspired patterns or motifs;
- subtle texture;
- expressive but usable typography;
- image-led composition and intentional cropping;
- edge-aligned or offset media;
- data visualization;
- purposeful density changes;
- controlled contrast;
- deliberate section transitions;
- whitespace as an active compositional device.

These are tools, not requirements. Do not add them mechanically.

### PRD constraints vs creative freedom

Creative freedom is allowed wherever it does not:

- contradict an `APPROVED` product decision;
- silently resolve an `OPEN` product decision;
- invent unsupported product data, actions, counts, trust signals, or ecommerce behavior;
- change privacy, RFQ, contact, price, or availability semantics;
- harm accessibility or task completion.

Within those boundaries, do not choose the safest or most generic visual solution merely because the PRD is silent about presentation.

### Avoid design-system monotony

Explicitly inspect consecutive sections for excessive repetition of:

- width;
- alignment;
- heading placement;
- card structure;
- surface;
- image relationship;
- spacing rhythm;
- border/radius treatment;
- background;
- density.

If repetition makes the page monotonous, solve the composition rather than merely changing a color or adding a decorative object.

### Patterns and motifs

Patterns, structural motifs, geometry, and architectural graphics are allowed and encouraged when they strengthen the composition. Do not permanently restrict Abadin to existing pipe rings or measuring arcs. New motifs may be introduced when they fit the construction/material context and can become part of a coherent visual language.

A pattern is never a substitute for composition. If removing the decoration makes a section collapse visually, improve the layout first.

### Controlled creative surprise

Where content justifies it, a page may contain memorable compositional moments created through scale, geometry, imagery, layering, typography, data, interaction, architectural references, or section transitions. Not every section should be loud. Strong pages require contrast between expressive and quiet moments.

Use this operating principle:

`PRD defines product truth.`  
`Design System defines shared language.`  
`Composition System defines visual grammar.`  
`Art Direction provides creative freedom.`

Target:

`Coherent, not identical.`  
`Systematic, not formulaic.`  
`Creative, not decorative.`  
`Modern, not trend-dependent.`  
`Calm, not boring.`  
`Distinctive, not distracting.`

---

## 14. RTL and Persian UX

RTL must be native, not merely mirrored LTR.

Review:

- reading order;
- alignment;
- directional icons;
- breadcrumbs;
- pagination;
- tables;
- filters;
- sheets;
- dialogs;
- forms;
- mixed Persian/Latin content;
- price/unit composition;
- date/time composition.

Where applicable, preserve:

- Persian digits;
- Persian thousands separator;
- تومان;
- explicit sales/price units;
- Jalali dates;
- 24-hour time.

Persian copy should be natural, contemporary, clear, and appropriate for Iranian users.

---

## 15. Responsive review

Desktop approval does not automatically approve Mobile.

Review Mobile separately for:

- information priority;
- content density;
- touch targets;
- scrolling cost;
- sticky elements;
- sheets;
- table-to-card transformations;
- navigation;
- forms and keyboards;
- long Persian strings;
- price/unit wrapping;
- CTA accessibility;
- footer height;
- bottom-navigation behavior.

Do not approve a mobile design merely because the desktop layout technically fits on a narrow screen.

---

## 16. Accessibility

Target at least `WCAG 2.2 AA`.

Review, where relevant:

- contrast;
- visible focus;
- keyboard navigation;
- minimum practical touch targets (target 44px);
- status communication that does not rely on color alone;
- form labels;
- validation and errors;
- disabled states;
- dialog/sheet behavior;
- Escape behavior;
- readable typography;
- logical reading/focus order.

---

## 17. Edge-case stress test

Do not review only the happy path.

When relevant, consider:

- very long Persian product names;
- long Latin technical names;
- large prices;
- long units;
- no price;
- unavailable offers;
- no image;
- missing supplier logo;
- incomplete data;
- one supplier;
- many suppliers;
- one filter;
- many filters;
- no search results;
- loading;
- error;
- empty states;
- permission states.

For Contact:

- one responsive channel;
- several responsive channels;
- no valid public channel.

For RFQ:

- supported;
- partially supported;
- unsupported.

---

## 18. Design System review

Do not praise consistency for its own sake. A page can use every canonical component correctly and still be poorly designed.

Ask:

> Is the Design System helping the product, or is the product being forced into the Design System?

When a screen appears to require an exception, determine whether the root cause is:

- a local template problem; or
- a systemic Design System limitation.

Recommend a Design System change only when the issue is sufficiently systemic.

Do not rebuild foundations or components simply to make one screen easier to style.

Also distinguish **component consistency** from **page-level composition maturity**. If a new visual solution is genuinely stronger and reusable, allow the visual system to evolve rather than forcing the page back into an older pattern.

---

## 19. Avoid decoration-only fixes

Do not default to more shadows, gradients, colors, cards, illustrations, patterns, banners, or animations merely to make a weak composition appear modern.

However, do not interpret restraint as a ban on creative devices. Patterns, gradients, solid fields, imagery, geometry, layering, overlap, and shadows are valid when they have a compositional purpose. Shadows are appropriate where a real layered/elevated relationship exists; lines and tonal changes remain preferred for ordinary structural separation.

Every visual addition should strengthen hierarchy, comprehension, recognition, rhythm, atmosphere, or an intentional compositional relationship. First make the composition strong; then use visual devices where they improve it.

---

## 20. Footer review

Treat the footer as part of the overall experience.

Review:

- visual closure;
- brand contribution;
- navigation completeness;
- hierarchy;
- information density;
- mobile height;
- contrast;
- interaction behavior.

A dark footer is an exploration option, not a requirement.

Evaluate it against the selected visual direction rather than assuming it is automatically better.

---

## 21. Severity

Every actionable finding should be classified.

### `P0 — Blocking`

Examples:

- PRD contradiction;
- broken core journey;
- privacy/trust problem;
- materially incorrect action;
- serious accessibility failure;
- dead end in a core task.

Do not proceed until resolved.

### `P1 — Important`

Examples:

- meaningful UX problem;
- weak information hierarchy;
- important missing state;
- poor responsive behavior;
- substantial scanability/density issue;
- marketplace-character problem;
- meaningful brand-language problem;
- substantial page-level composition problem;
- visually formulaic/template-generated result that materially weakens an important page;
- high-value product-completeness concern.

Normally resolve before the next dependent milestone.

### `P2 — Polish`

Non-blocking visual or interaction refinement.

May be collected for a polish pass.

Do not manufacture findings to populate every severity level.

---

## 22. Fixed review output

Use this structure:

```text
DESIGN REVIEW

Scope:
Figma Node:
Viewport:
Verdict:

What works:
- ...

Findings:

[P0]
- ...

[P1]
- ...

[P2]
- ...

Missing / Product Opportunities:
- Classification: PRD REQUIRED / PRODUCT RECOMMENDATION / OPEN DECISION / LATER
- Finding:
- Reason:
- Required decision/action:

Design-system impact:
None / Local / Systemic

Creative / art-direction review:
- Composition maturity:
- Rhythm / variation:
- Pattern / motif / imagery use:
- Template-like repetition:

PRD conflicts:
None / ...

Required changes before approval:
- ...

Optional explorations:
- ...

VERDICT:
APPROVED
or
APPROVED WITH P2
or
CHANGES REQUIRED
```

When there are no meaningful findings in a category, say `None`. Do not invent issues.

---

## 23. Reviewer behavior

The reviewer must not:

- automatically agree with the Product Owner;
- automatically defend Claude's work;
- defend a previous reviewer recommendation merely for consistency;
- invent issues to appear thorough;
- present personal taste as a UX rule;
- treat every visual difference as inconsistency;
- prioritize Design System consistency above usability;
- change approved product behavior for visual convenience;
- silently resolve an `OPEN` decision;
- silently add a new feature;
- allow a `PRODUCT RECOMMENDATION` to be implemented before Product Owner approval;
- treat PRD silence as a requirement to use the safest/generic layout;
- confuse Design System consistency with repeating the same page composition;
- reject purposeful creative variation merely because an older page does not use it;
- approve a page that is technically consistent but compositionally generic or monotonous.

When evidence contradicts the Product Owner, Claude, or a previous reviewer opinion, explain the evidence and surface the disagreement.

---

## 24. Review decision

Every review ends with exactly one of:

### `APPROVED`

No unresolved P0/P1 issue blocks progression.

### `APPROVED WITH P2`

The milestone may proceed, with explicitly recorded non-blocking polish items.

### `CHANGES REQUIRED`

One or more blocking/important issues require another iteration before the dependent milestone proceeds.

Target changes should be specific and incremental whenever possible. Do not request a complete redesign when focused corrections can solve the problem.

---

## 25. Trigger

Treat this skill as active whenever the Product Owner says something equivalent to:

> «Design Review: این Node آماده است.»

or asks for a senior product-design review of an Abadin Figma milestone.

At that point:

1. inspect the rendered design;
2. inspect relevant structure/system details if necessary;
3. check the PRD and approved decisions;
4. evaluate both what exists **and what may be missing**;
5. produce the fixed review report;
6. perform an explicit composition/art-direction maturity check, including monotony and creative-opportunity review;
7. prevent unapproved product recommendations from being silently implemented;
8. return the review verdict.
