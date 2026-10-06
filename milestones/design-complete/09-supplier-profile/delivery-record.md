# Public Supplier Profile — design record (updated 2026-10-06)

Figma file: https://www.figma.com/design/Qwx3QpLbhwbouq12QLvAL5.

Responsive policy:
- Full-page designs at 1440 and 375.
- 1280, 360 and 320 are targeted validation only.
- External review is not used.

## Pages and frames

- **Component:** page «Supplier Identity» `373:2`, set `375:133`.
  - Variants: Layout=Desktop `374:2`, Layout=Mobile `375:42`.
  - Properties: Show rating, Show contact, Show facts, Show address, Show service area, Show hours.
- **Template page:** «Supplier Profile» `373:3`.
  - Full pages: 1440 `375:134` and 375 `375:91298`.
  - Earlier validation frames, kept: 1280 `375:1722`, 360 `375:92511`, 320 `375:93108`.
- **States** (each shows 1440 and 375):
  - No Logo + Long Name `376:3191`
  - No Contact Channel `376:3344`
  - Minimal Profile `376:3492`
  - Contact Menu + Sheet `376:93057`
  - Mobile Only + No Messengers `376:93656`
  - Empty Products `377:4868`
  - Unavailable + Mixed `377:4931`
  - No Reviews `431:5041`
  - Owner View `431:5298`
  - Showcase Loading + Failure `432:5576`
- **Removed:** the Paused + Inactive board (`432:5349`), because only Active suppliers have a public profile.
- **Boards:**
  - Components Used `433:5510`
  - Decisions board `433:5523`, renamed «OPEN Decisions (all closed)»
  - Doc `433:5533`

## Decisions closed by the owner (2026-10-06)

### Showcase
- Available and unavailable products are both shown.
- Order is newest to oldest only. Availability never affects order.
- An unavailable product shows no price, no last price and no update time.
- No other sorting, ranking, search or filter. The showcase does not replace Search or PLP.

### Rating
- One valid, published review is enough to show the rating.
- With no valid review, the rating is hidden.
- The review count is never shown publicly.

### Visibility
- Only Active suppliers have a public profile.
- These statuses have no public profile and no public status page or message: Pending Review, Needs Correction, Cannot Be Activated, Paused, Suspended.
- These statuses are handled only in the supplier's own panel flows.

## Page structure

1. **Identity Layer:**
   - logo, or the default avatar if missing;
   - name, city, date of presence on Abadin;
   - rating, shown when at least one valid review exists;
   - categories;
   - contact dock «تماس با فروشنده»;
   - facts (address, service area, hours), each only when registered.
2. **«دربارهٔ فروشگاه»:**
   - seller-written text, labelled as seller-written;
   - neutrality note;
   - map only when a pin is registered.
   - On mobile this section comes after the showcase.
3. **Showcase:**
   - grid of ProductCard Context=Supplier, available and unavailable mixed by date;
   - product count;
   - pagination.
4. **Buyer reviews:**
   - sand band;
   - rating summary without a count;
   - seller reply shown as distinct.
   - The owner sees «فروشنده نمی‌تواند برای فروشگاه خودش نظر ثبت کند».
5. **Footer.**
   - Mobile Bottom Nav shows no active item.

## PRD rules applied

### Contact (§15, C-02)
- «تماس با فروشنده» always opens the menu (desktop) or sheet (mobile), even with one channel.
- Mobile number first, then up to three messengers.
- With no channel, there is no contact action at all.

### Never shown
- Supplier website or social channels.
- RFQ button (RFQ-O8).
- Verification badge (RFQ-O10).

## Implementation notes (not blocking)

- **Product count:** the count shows the products listed in the showcase, available and unavailable. This is the «محصولات فعال» of §16.2; confirm in build.
- **Loading and error:** identity is server-rendered. Loading and error states are designed for the showcase only.
- **Owner view:** no seller-panel link. No new feature was added.
- **Side finding:** the PDP rating summary shows «بر اساس ۱۲ نظر», which conflicts with §26.
