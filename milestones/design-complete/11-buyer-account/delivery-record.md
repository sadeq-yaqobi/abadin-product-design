# Buyer Account «حساب خریدار» — Delivery record

Status: **Design Complete** — Owner approved 2026-10-07. No OPEN item remains. The next milestone (RFQ Create) is NOT started.

## Scope
Exactly five destinations (PRD §20, P0-4 / P0-4C / P0-4D):
1. نمای کلی (Overview)
2. محصولات ذخیره‌شده (Saved Products)
3. نظرهای من (My Reviews)
4. استعلام‌های خرید عمده (RFQ List + RFQ Detail with supplier responses)
5. اطلاعات حساب (Account Information)

«پنل فروشنده» / «ثبت فروشگاه» is only a Workspace Switch entry — never a sixth destination and never a status.

## Owner approval
- Owner approved Milestone 11 on 2026-10-07.
- Account-deletion behaviour is final per DL-044 / PRD `P0-4D` (see Product Decisions). DL-043 remains in the decision log as historical and superseded.

## Figma IDs (file Qwx3QpLbhwbouq12QLvAL5)
- Page «Buyer Account» `510:571`; doc frame `531:25718`.

### Full pages
| Page | 1440 | 375 |
|---|---|---|
| Overview | `511:2` | `512:2` (mobile = account hub) |
| Saved Products | `513:106159` | `513:106553` |
| My Reviews | `515:3894` | `515:4191` |
| RFQ List | `516:4769` | `516:5108` |
| RFQ Detail (comparison tab) | `518:5780` | `519:116143` |
| Account Information | `524:14865` | `524:15114` |

### State and interaction boards
- RFQ Detail interaction, desktop `519:112897`: response side sheet, Contact Menu (RFQ), expired response, close-RFQ dialog.
- RFQ Detail interaction, mobile `522:12941`: full response sheet, Contact Sheet, close-RFQ dialog.
- Auth flow — change mobile / re-authentication `526:15713`.
- States, desktop `528:15963`.
- States, mobile & toasts `529:16345`.
- Responsive validation 1280 / 360 / 320 `529:121862`.

## Navigation architecture
- **Desktop 1440:**
  - Header (signed in) → breadcrumb → content column + Account Nav (Buyer · Sidebar, 280, sticky, right).
  - RFQ Detail is a deep task page: full 1200 width without the sidebar.
  - The Account Menu popover from «حساب من» lists the same five destinations, plus Workspace Switch and logout.
- **Mobile 375:**
  - Overview is the account hub: Account Nav list with Workspace Switch and logout, then the RFQ module and the saved preview.
  - Sub-pages use Header Type=Back with a page H1.
  - Bottom Nav: «حساب من» is active on account pages and «ذخیره‌شده» on Saved Products. The RFQ tab appears only when RFQ is on.

## Key behaviours (from PRD)
- **Overview:** shows only real data and shortcuts to real destinations. No stat cards, scores or invented activity. Empty sections show one sentence and a link.
- **Saved Products:**
  - Saved items are private.
  - Unsaving removes the product immediately and shows a Toast with «بازگرداندن» (no dialog).
  - ProductCard is reused unchanged.
- **My Reviews:** rating, text, product/supplier context and publication status. A seller reply is shown as a distinct block.
- **RFQ List:**
  - Each row shows status, date, item count, responses and an unread marker.
  - History stays visible when RFQ is globally off; only the create entry and the RFQ tab disappear.
- **RFQ Detail:**
  - Tabs: مقایسهٔ پاسخ‌ها / فهرست اقلام / فایل‌ها (DL-005).
  - Comparison is item-centric.
  - An expired price is shown with «اعتبار قیمت تمام شده» and excluded from the valid comparison.
  - Item states: a file item shows «در حال بررسی»; an unsupported item shows «فعلاً برای این شهر و دسته قابل استعلام نیست».
  - The only RFQ action is «بستن استعلام», behind a confirm dialog.
  - «ادامه با این فروشنده» opens Contact Menu / Contact Sheet with an RFQ-code reminder.
  - The buyer may continue with multiple suppliers. Contact never closes the RFQ.
  - There is no winner, selected or purchase state.
- **Account Information:**
  - Shows an editable name and the private verified mobile.
  - Changing the number: OTP to the current number → new number → OTP to the new number, with a «number linked to another account» error.
  - The account mobile never becomes a public supplier channel.

## Approved Product Decisions
- **DL-044** (APPROVED, Owner 2026-10-07; PRD §20, §26, §35 `P0-4D`):
  - The MVP has no self-service account deletion, in either Buyer Account or Seller Panel.
  - Deletion is handled operationally through support, outside these interfaces.
  - The account UI does not expose or explain that process.
  - No account-deletion UI exists in this milestone, and none may be reintroduced.
- **DL-043:** historical, SUPERSEDED by DL-044.
- **DL-005:** RFQ Detail tabs (existing decision, reused).

## Design Assumptions
1. Review status labels are «منتشر شده» / «هنوز منتشر نشده», taken from the PRD field «وضعیت انتشار». Buyers cannot edit or delete their own reviews (the PRD is silent).
2. Comparison lines appear in arrival order, with expired responses last. There is no price sorting and no «best» label.
3. Opening an RFQ Detail marks its new responses as read.
4. The Saved list is ordered newest-saved first, with pagination.
5. Changing the number requires two OTP confirmations. The old number stays active until the final confirmation.

## OPEN
None. OPEN-11-1 (deleting an account that also has a store) was closed on 2026-10-07 because it no longer applies (DL-044).

## Design System
- **Created:** Toast `512:105799` (Tone Neutral / Success / Error; Message; Show action), on the Notice page.
- **Changed (systemic):**
  - RFQ Summary Row `41:1094`: added Responses / Show responses, Unread label / Show unread, and Layout=Stacked.
  - RFQ Comparison Line `40:1037`: added Layout=Stacked ×6.
  - RFQ Item Comparison `40:1038`: title wraps.
  - RFQ Supplier Response Card `41:325`: rating shown without review count; item titles, validity and trust signals wrap.
  - Contact Sheet `231:11086`: inner Sheet fills the width, so it works at 320.
- **Reused:**
  - Shell: Header/Desktop, Header/Mobile, Footer, Page Atmosphere, Breadcrumb
  - Account and navigation: Account Nav, Account Menu, Workspace Switch, Nav List Item, Bottom Nav
  - Content and feedback: ProductCard, SaveToggle, Pagination, Empty State, Notice, Skeleton, Tabs, Badge
  - RFQ: RFQ Status, RFQ Buyer Header, RFQ Item Row
  - Contact and overlays: Contact Menu, Contact Sheet, Sheet, Dialog
  - Controls: Icon Button, Button, Field/Input, Checkbox, Sign-in Card / OTP Input, Avatar
- No other component was created for milestone completion.

## Responsive validation
- Full pages designed at 1440 and 375.

### Tested (inspected)
- 1440: all approved full pages.
- 375: all mobile pages and mobile interaction states.
- 1280: Overview and RFQ Detail.
- 360 and 320: all six pages (Overview hub, Saved Products, My Reviews, RFQ List, RFQ Detail, Account Information).
- 320: supplier response sheet and Contact Sheet.

### Found and fixed
- RFQ Summary Row overflowed → Stacked variant.
- Comparison-line supplier names truncated → Stacked variant.
- Item titles truncated → titles wrap.
- Response card validity and titles clipped → wrap.
- Contact Sheet was fixed at 375 → now fills the width.
- ProductCard unit and CTA clipped in 2 columns → Price Compact and no CTA arrow, as on the PLP.
- 4 saved cards too narrow at 1280 → 3 cards.
- Mobile tabs overflowed → horizontal scroller anchored right.

### Not tested
- Saved Products, My Reviews, RFQ List and Account Information at 1280.
- Desktop interaction states at 1280.
- Account Menu popover at 1280.
- Toasts at 360 / 320.
- Change-mobile flow at 360 / 320.
- Keyboard-open OTP sheets.
- Landscape.

These untested areas did not block Owner approval and are not reported as PASS.

## Out of Scope
- RFQ Create (form, entry flow, create pages) — a separate milestone, not started.
- Seller Panel.
- Internal operator tools.
- Notification center (none in MVP).
- Availability Alert «موجود شد خبرم کن» management (PRD P0-4B: no account page).
- Price following.
- Self-service account deletion (DL-044 / P0-4D).

## Known limitations
- Wrapped chip and meta rows flow left-to-right in Figma; build them with RTL flex-wrap (start = right).
- Product images are placeholders.
- The Toast action uses Link Small (36px); in build its hit area must be at least 44×44 via padding.
