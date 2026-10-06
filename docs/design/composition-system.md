# Abadin Composition System

**Status:** Design System layer (2026-10-01).
**Figma page:** «Composition System» `326:2` (root frame `326:3`).

This layer sits above tokens and components and below individual pages.

- The **Component System** answers: "What does a Button, ProductCard, Filter or Accordion look like?"
- The **Composition System** answers: "How do these parts form a convincing page?"

A page can pass the first and fail the second. Every review evaluates both.

## Key rule

**Visual treatment follows the purpose of the information.** For each section, decide first what it does: discovery, comparison, education, identity, evidence, decision, technical reference or navigation. Then choose the composition. Never change a surface, width or image just to add variety.

## Diagnosis (why this layer exists)

Round 4 set the visual identity, but later work reduced it to a recipe:

- white → mist → white → deep teal;
- pipe ring, arc, border, large radius, Section Heading.

Components became consistent while page composition became uniform:

- every section was "heading + centred block on a surface";
- consecutive sections repeated the same width, alignment and density;
- decorative devices stood in for compositional decisions.

## Reference lessons (Flooring Surgeons — principle, not style)

1. **Each section is composed for its job:**
   - layered split hero;
   - plain white category grid for scanning;
   - dense deals row;
   - values section with no imagery and larger type;
   - full-bleed dense gallery;
   - location on a dark surface;
   - structured pricing table;
   - calm contained form.
2. **A pattern background marks only the "evidence" section.** Surface changes have a reason.
3. **Split sections alternate direction** to build rhythm.
4. **Only genuinely floating things are elevated:** the sticky header and the chat widget.
5. **Density rises and falls deliberately.**

Not adopted: its colours, type, mascot, discounts, ratings and social-proof numbers. They conflict with the PRD.

## Families

- **A · Open Atmosphere.** Page intros and Search context. Content sits directly on the shared atmosphere, with no surface.
- **B · Identity Layer.** Category, brand and supplier identity.
  - A translucent white surface (72%) with a border-subtle line and radius 28, no shadow.
  - Media and text form one unit. With no media, the layer shrinks to fit the text.
- **C · Media Composition.** Asymmetry, crop, offset, one overlapping media element (L1), edge bleed. Alternate the direction between consecutive sections.
- **D · Dense Workspace.** PLP, filters, offers, tables. Richness comes from structure; do not dilute density.
- **E · Feature / Story.** An edge-bleed image with a text panel riding on it (L1) and strong type. At most one or two per page.
- **F · Data & Technical.** Charts with a left-to-right time axis, numbers with units, tables with horizontal rules, LTR codes. Only valid data.
- **G · Contrast Band.** Mist, sand or deep teal, only when the content's purpose changes. At most one dark band besides the footer. Never two tinted bands in a row.
- **H · Decision Moment.** Limited width (640–800), one message, one primary action. Not a generic banner. Never for actions the PRD disables.
- **I · Discovery Mosaic.** Tiles of mixed size only when there is real hierarchy. Real images with a dark scrim. Never used for the product grid.

## Surfaces (when to use / when not to use)

| Surface | Use | Avoid |
|---|---|---|
| 1. Open / atmosphere | Intros, reading columns | Grouping dense controls |
| 2. Atmosphere-integrated translucent | Identity layers | On plain white; over images |
| 3. White contained (border, r20) | Panels, cards, tables | Wrapping whole sections or articles |
| 4. Mist | Decision and reference sections (offers, FAQ) | Consecutive bands |
| 5. Sand | Voices, guides, decision moment | Data |
| 6. Deep teal | Market data, footer | Long text, forms |
| 7. Line only | Grouping inside a surface | As the default for every block |
| 8. Elevated (L1) | Only when layered over something | Static cards |
| 9. Media as surface (scrim) | Category tiles, story | Without real images |
| 10. Structural / pattern | Page edges, contrast bands | Behind text; as the only idea in a section |

## Depth model

| Level | Treatment | Use |
|---|---|---|
| 0 · Flat | None | Page, open sections |
| 1 · Structure | 1px border-subtle | Cards, panels, tables, identity layer |
| 2 · Lift | Elevation/L1 | Sticky header over scrolling content, overlapping media, story panel, card hover |
| 3 · Float | Elevation/L2 | Menus, popovers, dropdowns, tooltips |
| 4 · Overlay | Elevation/L3 + scrim | Dialogs, sheets |

- At most two lifted or floating elements per composition region.
- Never use a shadow to make something "visible".

## Image art direction

Eight relationships: contained, offset, bold crop, overlapping, edge-aligned, background-integrated, gallery, small supporting media.

- **Aspect ratios:**
  - 1:1 product or tile;
  - 4:3 application;
  - 16:9 editorial;
  - 3:4 vertical story.
- **Real photography only.** Placeholders are for design files only.
- **Missing or weak image:** switch the composition. Never leave a large empty slot.
- No essential text inside images; always give descriptive alt text.

## Section transitions

Eight mechanisms: whitespace (64/96/128), tonal change, structural line, geometry on the boundary, image overlap across the boundary, controlled depth (a module straddling the boundary), density change, typographic opener.

Don't default every transition to a new background colour or to large whitespace.

## Rhythm

- A page moves through quiet → dense → open → focused → quiet.
- Change only one or two variables per transition: width, density, alignment, image scale or crop, surface, depth, type scale.
- Avoid both monotony and chaos (see the examples on the page).
- **Remove-the-pattern test:** if a section collapses without its decoration, redesign it.

## Workflow for a new page

1. List the sections from the PRD.
2. State each section's purpose.
3. Choose a family.
4. Map the rhythm.
5. Choose a transition for each boundary.
6. Choose surfaces and depth.
7. Choose image relationships and design the no-image state.
8. Add patterns last, then run the remove-the-pattern test.
9. Compose mobile separately.
10. Run the checklist and the component review.

## Composition quality checklist (14)

1. Is the page visually flat?
2. Are too many consecutive sections using the same width, alignment or surface?
3. Does every section look like a card?
4. Are background changes meaningful?
5. Is the information hierarchy clear?
6. Is there at least one strong compositional moment where appropriate?
7. Are dense areas allowed to stay dense?
8. Are quiet areas really quiet?
9. Does imagery take part in the composition?
10. Is decoration compensating for weak layout?
11. Does the page still feel like Abadin without the logo?
12. Does it look designed rather than assembled from components?
13. Does mobile keep the hierarchy rather than just stack desktop blocks?
14. Does visual variation support the user journey?

## Disclosure (Base UI, page «Disclosure», set `301:36169`)

This generic Read more / Read less component replaces the PLP-specific «Long Content».

**Properties:**
- State: Collapsed / Expanded.
- Layout: Desktop / Mobile.
- Content: instance swap.
- Show fade.
- Toggle: exposed Button, so the label can be edited.

**Collapsed:**
- Visual max-height of 360 (desktop) / 420 (mobile).
- A fade covering about a third of the region, in the colour of the surface behind it.
- A centred action row: rule · Outline pill with chevron · rule.

**Expanded:**
- Full content, then the same centred row.
- The action's horizontal position stays the same in both states.

**Rules:**
- If content is no taller than max-height + 120px, show it fully with no action.
- Never cut an image or table in half.

**SEO:**
- Full content is in the server-rendered HTML.
- Collapsing is CSS only.
- No truncation, no fetch on expand, no injection.

**Accessibility:**
- `<button aria-expanded aria-controls>`, operable with Enter/Space.
- Visible focus; target of at least 44px.
- No focus trap; hidden links are inert.
- Motion ≤200ms and off under reduced motion.

**Use for:**
- long category or brand descriptions;
- the supplier «درباره» (about) section;
- long guides.

**Do not use for:**
- short text;
- legal text;
- specifications;
- offers or prices;
- FAQ answers (use Accordion);
- task-critical content.
