---
name: "abadin-figma-design"
---

# Abadin Figma Design

Use this skill for Abadin product-design work in Figma.

The outcome must be a usable, coherent Persian RTL product experience that implements the approved product behavior and belongs unmistakably to Abadin's approved visual direction.

Visual novelty is not a goal by itself, but visual richness, composition, imagery, data visualization, architectural references, and distinctive geometry are valid design tools when they improve the experience or strengthen the approved direction.

## Source-of-truth hierarchy

Use sources in this order:

1. `Abadin-PRD.md`
2. `abadin-visual-direction.md`
3. Approved Abadin Design System (including the Composition System layer — Figma page «Composition System» and `claude/composition-system.md`)
4. Professional UX/UI, accessibility, responsive-design, and design-system principles

### PRD

Read the current Abadin PRD before starting meaningful design work.

Treat `APPROVED` decisions as binding.

Do not silently decide items marked `OPEN`.

Do not reintroduce items marked `LATER` into MVP.

Do not add product features, metrics, states, claims, trust signals, or CTAs that the PRD does not support.

The PRD governs product behavior, scope, privacy, business rules, terminology, and required states.

It is not a visual-style specification. Unless it explicitly states a visual requirement, the absence of visual instruction is design freedom. Do not invent visual restrictions from product rules or choose the safest/generic composition merely because the PRD is silent about presentation.

### Approved Visual Direction

Read `abadin-visual-direction.md` before creating or materially changing screens, templates, patterns, or visual foundations.

It governs the approved visual language, atmosphere, composition, geometry, imagery approach, motion philosophy, responsive visual behavior, and recognizable Abadin characteristics.

Do not reinterpret the PRD as a requirement for a minimal, quiet, low-expression, or generic interface.

If an older Figma component or Design System rule conflicts with the approved Visual Direction, treat it as a migration issue. Do not force new work back to the superseded visual treatment.

### Approved Design System

Use approved Foundations, UI Components, Domain Components, Patterns, tokens, and interaction rules whenever they remain compatible with the PRD and approved Visual Direction.

Preserve an existing component or pattern when its product behavior, structure, and visual treatment remain valid.

Change or migrate it when necessary to resolve a real product, usability, accessibility, responsive, systemic-consistency, or approved-direction problem.

## Composition System (mandatory for every page or section)

The Component System answers "what does a Button / ProductCard / Filter look like"; the Composition System answers "how do these parts form a convincing page". A page can use every correct component and still be badly designed. Evaluate both, separately, before calling any page complete.

Key rule: visual treatment follows information purpose. For every major section first state what it does (discovery, comparison, education, identity, evidence, decision, technical reference, navigation), then choose a composition family:

- A Open Atmosphere — intros, Search context; content directly on the shared atmosphere, no surface.
- B Identity Layer — category / brand / supplier identity; establish a distinct but integrated identity composition. Translucent/tonal containment, border, radius, media integration and no-media adaptation are approved reference techniques, not mandatory recipes.
- C Media Composition — use media as part of the composition through techniques such as asymmetry, crop, offset, overlap or edge alignment where they strengthen the content. These are options, not required ingredients; do not mechanically alternate layouts.
- D Dense Workspace — PLP, filters, offers, tables; richness from structure, never diluted density.
- E Feature / Story — a more expressive composition for explanation/editorial storytelling. Edge-bleed media, layered text surfaces, stronger typography or other approved techniques may be used when appropriate; do not force a fixed layout or quota.
- F Data & Technical — valid data only; time axis left-to-right; LTR codes.
- G Contrast Band — use an approved tonal/solid shift when content purpose genuinely changes. Mist, sand and deep teal are established options, but the composition should determine treatment; avoid mechanical alternation or arbitrary quotas.
- H Decision Moment — focus attention on a genuine next decision/action using an appropriately concentrated composition; never introduce a PRD-disabled action. The exact width and layout are design decisions.
- I Discovery Mosaic — mixed tile sizes only for real hierarchy; never the product grid.

Workflow for any new page: sections from the PRD → purpose per section → family → rhythm map (quiet / dense / open / focused) → one transition mechanism per boundary (whitespace, tonal change, structural line, geometry, image overlap, controlled depth, density change, typographic opener) → surfaces and depth → image relationship and no-image state → structural patterns last (remove-the-pattern test) → compose mobile separately → run the checklist.

Change only one or two variables per transition (width, density, alignment, image scale/crop, surface, depth, type scale). Avoid both monotony and chaos. Decorative devices (pipe rings, measuring arcs, textures) are secondary: if a section collapses when they are removed, redesign the composition.

Depth model: 0 flat · 1 structure (1px border-subtle) · 2 lift (Elevation/L1: sticky over scrolling content, overlapping media, story panel, hover) · 3 float (L2: menus, popovers) · 4 overlay (L3 + scrim). Shadows only for real layering, never to make a panel "visible"; at most two lifted/floating elements per region.

Shared page top: every public desktop page with the standard header uses the instance «Page Atmosphere / Top (shared)» at (0,0) (mobile −500,−200; PDP −300). Never fork, hide a layer, lower opacity or resize it; fix contrast locally.

Composition quality checklist (run before completion): 1 flat? 2 too many consecutive sections with the same width/alignment/surface? 3 everything a card? 4 background changes meaningful? 5 clear hierarchy? 6 at least one strong compositional moment where appropriate? 7 dense areas allowed to stay dense? 8 quiet areas really quiet? 9 imagery participates? 10 decoration compensating for layout? 11 still Abadin without the logo? 12 designed rather than assembled? 13 mobile keeps hierarchy rather than stacking? 14 variation supports the journey?

Long content: use the shared Disclosure component (Base UI) only for genuinely long content; full content stays in server-rendered HTML, collapse is presentation only, the action is centred.

## Creative art-direction responsibility

The designer is responsible for art direction, not merely component assembly. Do not wait for the Product Owner to request more depth, a pattern, an overlap, a different section treatment, stronger imagery, a new motif, or less repetition when those needs are visible from the composition itself.

Before requesting review, perform an internal creative pass and iterate on obvious weaknesses. Explicitly ask:

1. Is the composition strong without decoration?
2. Are several consecutive sections repeating the same width, alignment, surface, heading placement, image relationship, spacing rhythm or density?
3. Does anything feel template-generated or like a safe default rather than a designed Abadin page?
4. Is imagery participating in the composition rather than being dropped beside text?
5. Is hierarchy being created through more than cards, borders and background changes?
6. Is there an appropriate balance between quiet and expressive moments?
7. Could geometry, layering, meaningful elevation, typography, data, imagery, pattern, texture or a section transition materially improve the experience?
8. Does the result meet or exceed the design maturity of the approved Home and PDP without copying them?

If obvious improvements exist, iterate before handing the milestone to review.

Creative tools are available when they serve the page: asymmetric composition, architectural geometry, construction/material-inspired patterns, abstract technical motifs, subtle texture, controlled overlap, layered surfaces, meaningful elevation, solid or tonal fields, atmospheric gradients, expressive typography, image-led composition, intentional cropping, edge-aligned media, data visualization, density changes and purposeful transitions. They are possibilities, not requirements.

Patterns and motifs are not limited to the existing pipe rings and measuring arcs. New motifs may be developed from construction, materials, measurement, plans, grids, structure, fabrication, surfaces, architecture or technical notation, including abstract interpretations. When a new motif or composition proves successful and reusable, propose/document it as an evolution of the Design System after validation.

A pattern, gradient, shadow or decorative object must never be used as a substitute for weak composition. A section should remain compositionally convincing when secondary decoration is removed.

Home and PDP are the current quality baseline, not page templates. Future pages may introduce new compositions and extend Abadin's visual language while remaining recognizably part of the same product family.

Operating principles:

- **Coherent, not identical.**
- **Creative, not decorative.**
- **Systematic, not formulaic.**
- **Modern, not trend-dependent.**
- **Calm, not boring.**
- **Distinctive, not distracting.**

## Design-system foundation

Use `shadcn/ui` primarily as an architectural reference for component taxonomy, composition, states, accessibility behavior, and predictable APIs.

Do not treat the default visual appearance of `shadcn/ui` as Abadin's visual direction.

Abadin must not become "shadcn with a teal brand color."

Abadin's visual language comes from `abadin-visual-direction.md`.

MVP is light theme only.

Do not create dark-theme screens, dark component variants, or a second token mode.

Keep semantic tokens structured so a future theme can be added without redesigning component semantics.

Build and migrate foundations and reusable primitives before duplicating local patterns.

Add Abadin-specific domain components progressively as genuine reusable needs emerge from product journeys.

## Design-system health

Before creating a component:

1. inspect the existing system for an equivalent or adaptable component;
2. determine whether the need is local or systemic;
3. extend an existing component when its structure and behavior are genuinely the same;
4. create a new component only for a reusable structural or domain-specific need.

Do not create overlapping variants of buttons, cards, fields, filters, menus, sheets, or other established patterns.

For every new reusable component, make its purpose, states, responsive behavior, content rules, and relationship to existing components clear.

Do not force a product screen into an unsuitable component merely to preserve Design System consistency.

The Design System serves the product; the product is not forced into the Design System.

## Figma workspace and plugin

Create and edit Abadin Figma work only in `Sadeq's team`.

Before implementing or changing a design, read the `Design Skill` supplied by the installed design plugin and follow its operational guidance where it does not conflict with Abadin's source-of-truth hierarchy.

Use Figma data, components, variables, styles, and assets only when they are present and valid.

Do not invent brand assets, unsupported data, technical integrations, certifications, supplier claims, or product behavior.

## Approved design direction

Design Persian first and RTL first.

Use natural contemporary Persian copy, native RTL layout and reading order, and deliberate handling of mixed Persian, numerals, URLs, technical codes, and English product data.

Use `Vazirmatn` as the product typeface.

Use `#0B6264` as the primary brand anchor.

The public experience is primarily white-first, with restrained teal/mist atmosphere and controlled copper accents according to the approved Visual Direction.

Use rounded structural geometry, purposeful floating/elevated surfaces, content-specific compositions, real imagery, diagrams, data visualization, and architectural/material references where they improve the experience.

Do not require every page or section to use every visual device.

The goal is family resemblance, not identical composition.

Avoid returning to:

- repetitive `Heading → Text → White Card` layouts;
- generic SaaS styling;
- static catalogue or PDF-like composition;
- excessive identical bordered cards;
- generic AI styling;
- decorative elements that compete with product tasks;
- ecommerce semantics that conflict with Abadin.

Visual richness is allowed.

Visual noise that harms hierarchy, comprehension, comparison, accessibility, or task completion is not.

## Marketplace character

Abadin should feel like a modern product-discovery and supplier-comparison marketplace.

Design should support:

- scanning;
- discovery;
- filtering;
- product evaluation;
- observed-price understanding;
- supplier comparison;
- supplier evaluation;
- contact or exact-product continuation;
- RFQ where applicable.

Do not visually imply that Abadin sells products itself.

Do not introduce cart, checkout, payment, Buy actions, supplier winners, cheapest-supplier promotion, unsupported verification, fake urgency, or unsupported social proof.

Product Cards retain the approved supplier-comparison behavior unless the PRD explicitly changes it.

## Long-session comfort

Assume users may spend 20–30 minutes searching, filtering, opening products, comparing offers, evaluating suppliers, contacting suppliers, returning, and searching again.

Optimize for:

- scanability;
- readable typography;
- useful hierarchy;
- manageable density;
- predictable interaction patterns;
- purposeful progressive disclosure;
- clear decision areas;
- responsive performance of the interface structure;
- low cognitive friction.

Do not equate long-session comfort with blandness or minimalism.

Rich composition, strong typography, imagery, atmospheric surfaces, diagrams, data visualization, and distinctive geometry are acceptable when they preserve usability.

## Imagery

Real photography is part of the intended marketplace quality.

Use it where it improves product recognition, category discovery, editorial value, or atmosphere.

The interface must remain usable when imagery is weak, missing, inconsistently cropped, or replaced by a placeholder.

Do not design the entire product under the assumption that imagery will always be polished.

Do not suppress imagery merely because construction-material photography may sometimes be ordinary.

Use the Composition System image relationships (contained, offset, crop, overlap, edge-aligned, background-integrated, gallery, small supporting media) instead of defaulting to "rectangle image + text beside it"; when an image is missing, change the composition rather than leaving an empty slot.

## Responsive design and delivery

Desktop and Mobile are separately designed experiences, not scaled copies.

The standard responsive delivery model is:

- `1440`: full-page Desktop design.
- `375`: full-page Mobile design.
- `1280`: targeted narrower-desktop validation width.
- `360`: targeted mobile validation width.
- `320`: targeted narrow-mobile stress-test width.

Do not create independent full-page designs at `1280`, `360`, or `320` by default.

These widths exist to validate responsive behavior, expose problems, and document meaningful adaptations—not to duplicate the complete approved page.

Create an additional frame at `1280`, `360`, `320`, or another intermediate width only when:

- a real layout or interaction difference needs to be demonstrated;
- a responsive problem cannot be understood clearly without a visual example;
- a section requires explicit responsive treatment;
- or review/implementation needs a concrete reference.

When an additional frame is needed, prefer a focused section-level or pattern-level frame over duplicating the entire page.

Document responsive behavior between the primary `1440` and `375` designs where material. This includes, as applicable:

- column-count changes;
- container and page margins;
- grid behavior;
- wrapping;
- typography behavior;
- navigation adaptation;
- filter and sort behavior;
- sticky/fixed behavior;
- media resizing/cropping;
- content reordering;
- sheet/overlay behavior;
- dense comparison layouts;
- intermediate breakpoint behavior.

Do not duplicate every state at every width.

Design a state at the width where it is most useful to communicate the behavior, then document or demonstrate additional responsive differences only where those differences are material.

Do not rebuild or locally duplicate an approved shared component merely to demonstrate responsive behavior. Use the approved component and its responsive rules unless a real systemic problem requires a Design System change.

Stress-test where relevant:

- long Persian labels;
- long product names;
- mixed Persian/Latin content;
- large prices;
- price/unit wrapping;
- empty and unavailable states;
- keyboard states;
- sheets and overlays;
- fixed/sticky UI;
- safe areas;
- dense supplier lists;
- navigation overflow.

Do not consider a desktop frame complete without defining the mobile behavior that materially affects the journey.

A responsive width or state that has not actually been inspected or tested must not be reported as validated, complete, approved, or `PASS`.

Untested behavior remains an explicit validation dependency.

## Accessibility

Target at least `WCAG 2.2 AA`.

Where relevant, design for:

- visible focus;
- logical keyboard navigation;
- practical 44px touch targets;
- sufficient measured contrast;
- non-color-only status communication;
- clear labels and validation;
- predictable dialogs and sheets;
- `Esc` behavior;
- logical reading/focus order;
- reduced-motion preferences.

Do not rely on visual estimates where measured contrast is required.

## Interaction and motion

Use motion purposefully.

Appropriate uses include functional transitions, hover/focus feedback, menus, sheets, search transitions, chart interaction, and restrained ambient/parallax behavior where approved.

Do not add decorative motion merely to make a screen feel dynamic.

Respect reduced-motion preferences.

## Delivery discipline

Design the responsive and interaction states required by the approved journey.

Do not treat desktop artboards as the whole deliverable.

Use the responsive delivery model defined above: full-page production designs at `1440` and `375`, with `1280`, `360`, and `320` used for targeted validation rather than automatic full-page duplication.

Before calling a milestone complete, verify:

- destination and CTA behavior;
- available data;
- empty/unavailable/error states;
- responsive behavior;
- RTL behavior;
- accessibility;
- PRD compliance;
- Visual Direction compliance;
- Composition System checklist (all 14 questions);
- Design System impact.

Only claim validation for widths, states, components, and journeys that were actually inspected or tested.

Never report an untested width, state, interaction, or dependency as `PASS`, approved, complete, or validated.

When responding to review feedback, update and re-review the changed areas and any components, sections, states, or responsive behaviors materially dependent on those changes.

Do not automatically redesign or re-review unaffected approved areas.

Do not reopen previously approved design decisions unless:

- the Product Owner explicitly changes them;
- the current task explicitly includes them;
- or a real contradiction, dependency, accessibility issue, product error, or systemic problem makes reconsideration necessary.

Do not automatically delete, replace, archive, or restructure old Figma frames as part of unrelated design work.

Deletion or cleanup requires explicit task scope.

Do not rebuild approved shared components as local page-specific copies.

If an approved shared component requires a real change, treat the impact as systemic, identify its dependencies, and update the Design System intentionally.

Report:

- what changed;
- which PRD decisions governed it;
- which Visual Direction principles governed it;
- which composition families and transitions were chosen, and why;
- whether Design System changes were Local or Systemic;
- which primary responsive frames were designed;
- which targeted responsive widths were actually tested;
- what intermediate responsive behavior was documented;
- which states or widths remain untested;
- any affected dependencies that were re-reviewed;
- any unresolved product question;
- any remaining validation dependency.

Do not claim an unresolved decision is complete.

Do not claim untested work is complete.

When a meaningful milestone is ready, hand it to the `abadin-senior-design-review` gate before proceeding to the next dependent milestone.