# Figma cleanup log & off-canvas records

File: https://www.figma.com/design/Qwx3QpLbhwbouq12QLvAL5

This doc keeps compact records for canvas material removed during cleanup, so nothing unique is lost when boards are deleted.

## PASS record — Category PLP identity header refinement (2026-10-01)

- **Verdict:** ChatGPT review PASS (2026-10-01).
- **Change:** the Category identity composition in Listing Context.
  - Desktop H1 uses Heading/Section 40/58 ExtraBold.
  - The count sits on the title baseline (Label/Default).
  - Description is Body/Large with a 640 reading measure.
  - The optional category photo is 360 wide at the end side (left in RTL). It is lifted 40px above the identity layer's top edge, with radius/card and Elevation/L1.
  - On mobile, an 88×88 media square overlaps the top edge. The identity height dropped from 348 to about 238.
  - Media=None uses the same type hierarchy.
- **Production IDs:**
  - Listing Context set `285:19199`. Changed variants: Category Desktop Image `285:50`, Desktop None `348:58`, Mobile Image `285:19160`, Mobile None `348:76185`.
  - Category templates: 1440 `287:6766`, 1280 `316:61586`, 375 `287:25245`; stress 360 `348:76292` and 320 `348:77006`; conditional-content frames `302:36730`, `302:37709`, `302:38687`, `302:39665`, `302:40643`.
- **Brand identity:** redesigned separately on 2026-10-06; see `claude/brand-identity-notes.md`.
- The before/after board `363:22957` was removed in C0.

## Round 4 image sources (moved from archived board 138:270)

- All images were chosen from Unsplash for design exploration only.
- Production licensing must be checked separately.
- None of them were placed in the Figma file; the image hosts were blocked.

| ID | Intended use | URL |
|---|---|---|
| IMG-01 | Hero, arched concrete architecture | https://unsplash.com/photos/modern-architecture-with-concrete-curves-and-glass-facade-pLM1bnJtmMU |
| IMG-02 | Small hero, cement category tile, cement product card | https://unsplash.com/photos/a-pile-of-bags-of-cement-sitting-next-to-each-other-rc5crEySTXo |
| IMG-03 | Rebar category, rebar product card | https://unsplash.com/photos/bundled-rusty-steel-rebar-for-construction-XRuBqN8o7Pg |
| IMG-04 | Brick and block category | https://unsplash.com/photos/a-bunch-of-bricks-stacked-on-top-of-each-other-KCa-xut7Wn4 |
| IMG-05 | Tile category, tile product card | https://unsplash.com/photos/white-and-gray-ceramic-tiles-q9ZiOzsMAhE |
| IMG-06 | Pipe category, small gallery image, related product | https://unsplash.com/photos/a-large-stack-of-pipes-stacked-on-top-of-each-other-F4nEetWGt0A |
| IMG-07 | Main PDP image, five-layer pipe card | https://unsplash.com/photos/a-bunch-of-black-pipes-stacked-on-top-of-each-other-D5LVMChT3PU |
| IMG-08 | Faucet category, mixer card, related product | https://unsplash.com/photos/a-close-up-of-a-bathroom-sink-with-a-faucet-wqpL0EqI9rY |
| IMG-09 | Electrical category, cable card | https://unsplash.com/photos/a-pile-of-wires-and-wires-in-a-pile-xzWlB1dqICk |
| IMG-10 | Insulation category, isogam card | https://unsplash.com/photos/building-under-construction-roof-beams-frame-and-roofing-underlayment-water-resistant-waterproof-barrier-on-walls-of-hollow-foam-insulation-blocks-masonry-roofing-and-renovation-J8YHiSMnCjY |
| IMG-11 | Magazine, large image | https://unsplash.com/photos/construction-workers-pouring-concrete-on-a-sunny-day-8eEkLj8HU_I |
| IMG-12 | Magazine, second article | https://unsplash.com/photos/modern-concrete-building-facade-with-recessed-windows-Eg1hXdCWfsM |
| IMG-13 | Magazine, third article | https://unsplash.com/photos/construction-site-worker-in-boots-and-uniform-finishing-concrete-on-ground-AdS2DtmUeXw |
| IMG-14 | Reserve (dark texture for a price module) | https://unsplash.com/photos/bundled-steel-rebar-in-a-dark-blue-hue-Dk4wr4YL-4Y |
| IMG-15 | PDP gallery, related product | https://unsplash.com/photos/a-pile-of-pipes-sitting-next-to-each-other-B0jijv2X-U8 |
| IMG-16 | Brick product card | https://unsplash.com/photos/a-stack-of-bricks-sitting-on-top-of-each-other-wASesy3WhK8 |

## C0 cleanup (2026-10-01) — status: PASS

- **Review:** ChatGPT PASS in round 2.
  - Round 1 returned CHANGES REQUIRED because the Tracker still referenced the deleted board 363:22957.
  - The fix was to point the Tracker at this log.

### Removed

- Archive page 126:2:
  - R4 Home 126:3, 151:8360, 152:645;
  - R4 PDP 133:165, 151:9425, 156:696;
  - 138:385, 138:270, 139:270, 147:253, 167:809, 167:811, 171:877, 173:930, 174:962, 165:778;
  - label texts 139:8237–139:8240.
- Search page 64:3200: 363:22957.

### Kept

- 151:8345, the PDP reviews empty state. No production equivalent exists yet; promote it to the Product Page in a later task.
- The archive banner 265:531, with its text updated.
- The archive page 126:2 itself.

### Updated

- Production Index 265:55 now reads «Production — approved».
- Production Index 265:70, the archive note.

### Evidence

- 0 prototype reactions file-wide.
- 0 broken instances after cleanup.
- All protected production IDs are present.
- No instance was detached.

### Measured

- Pages: 75 → 75.
- Archive page top-level: 25 → 5.
- Archive page nodes: 7,065 → 20.
- Search page top-level: 46 → 45.
- Whole-file totals were not compared.

### Deferred candidates (not removed)

- Orphan rectangles 173:941, 173:1021, 173:1107.
- BEFORE snapshots 316:57652, 325:18461, 325:19554, 325:20558, 325:21396 — removed later, in C1 (2026-10-06).
- Review boards 289:26694, 248:18538, 213:11517, 236:698, 190:2.

### Contract transfers

Interaction contracts that existed only on archive boards were moved into the descriptions of these production components (each tagged `[C0 transfer …]`):

- Header / Desktop `194:9957`, from board 147:253;
- Mega Menu `197:321` and Category Nav Row / «بیشتر» `194:9664`, from board 171:877;
- Nav Drawer `197:10878`, from board 173:930;
- PDP Compare Bar `233:24`, from board 174:962.

## C1 cleanup — Search / Category / Brand page `64:3200` (2026-10-06) — status: CLOSED, approved by the owner

Scope was this page only.

### Removed
Five detached BEFORE snapshots:

- `325:18461` — Category 1440, before the Composition pass.
- `325:19554` — Brand 1440, before the Composition pass.
- `325:20558` — Search 1440, before the Composition pass.
- `325:21396` — Category 375, before the Composition pass.
- `316:57652` — filter sidebar, before its refinement.

Removed after owner confirmation:

- `444:23200` — Brand identity before/after board. It is recorded in `claude/brand-identity-notes.md`.

Why removing them was safe:

- No components inside them.
- No prototype links.
- Nothing referenced them.
- Each one is superseded by an approved current frame.
- The decisions they illustrated are recorded in `claude/design-system-notes.md`, in `claude/brand-identity-notes.md` and on the Composition System page.

### Updated
- **Row label 7:** `316:61585` now reads «1280 validation + sticky filter».
- **Row label 8:** `325:18460` now reads «identity QA (Category 360/320 · Brand QA)».
- **Page doc `69:4697` / `69:4698`:**
  - Deliverables are 1440 + 375; 1280 / 360 / 320 are validation only.
  - Removed the stale note that the PRD still had the old FAQ / Long Description order.
  - FAQ bullet corrected to the split 1200 composition.
  - Added Category and Brand identity notes.
  - Added a page map.

### Page counts
- Top-level items: 47 → 41.
- Broken instances: 0.

### Left for a separate scope
- Review page `289:26694` — the PLP review board. The owner said to leave it untouched for now.
