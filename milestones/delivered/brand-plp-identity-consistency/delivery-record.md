# Brand PLP — Identity Consistency (2026-10-06)

Figma: https://www.figma.com/design/Qwx3QpLbhwbouq12QLvAL5

## Component

Listing Context set `285:19199`. Only the Brand variants changed:

- Desktop Image `285:75`
- Desktop None `348:80`
- Mobile Image `285:19177`
- Mobile None `348:76202`

## Changes

### Desktop
- **Brand plate:** a white plate at the RTL start, 232×136, with border-subtle, radius/card and no shadow. The logo sits inside a 184×88 box, contained and centred, never cropped or upscaled.
- **Eyebrow:** «برند», in teal with a copper bar.
- **Title:** H1 at Heading/Section 40/58. It wraps and is never truncated.
- **Count:** shown as a meta line under the title.
- **Description:** Body/Large, at most 640 wide.
- **Layer:** full-width at 1200.

### Mobile
- **Plate row:** an 88×52 plate on top.
- **Title:** full width, H1 28 ExtraBold, so long names are never squeezed by the plate.
- **Count and description:** follow below the title.
- **Eyebrow:** none. The breadcrumb already says «برندها».

### No logo (Media=None)
- The plate is removed.
- The layer hugs a 720 text column.

### Fixes
- Show description was bound in the None variants. Before, it was not linked.
- Brand 375 fixture corrected: the breadcrumb was «سیمان و بتن» and is now «برندها». The title and description now match the brand.

## Count

- The count is the dynamic total after filters (§13).
- No other counts, ratings, «official» or «verified» labels, or supplier counts are shown.

## Validation

QA board: `445:95982` on page «Search / Category / Brand».

| Width | Container | Result |
|---|---|---|
| 1440 | 1200 | PASS |
| 1280 | 1200 with a 40 gutter; same layout as 1440 | PASS |
| 375 | 343 | PASS |
| 360 | 328 | PASS |
| 320 | 288 | PASS (a long name wraps to 4 lines; the plate does not squeeze it) |

### Heights
- Desktop: 282 with a short name, 400 with a long name and long description.
- Mobile: 280 at 375, up to 440 with a long name and long description.
- Before the change: desktop 198, mobile 204.

### Edge cases
- Wide, square, tall and low-quality logos.
- No logo.
- Short and long names.
- Short and long descriptions.
- No description.

## Untouched

- The Category and Search variants.
- Grid, filters, toolbar, pagination, FAQ, Long Description and footer.

## Before / After board

- `444:23200`
