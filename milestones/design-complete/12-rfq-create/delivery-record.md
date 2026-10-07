# RFQ Create «ثبت استعلام خرید عمده» — Delivery record

Status: **Design Complete** — Owner approved 2026-10-07, including the final visual fixes. The next milestone is NOT started; the Owner selects it separately.

## Scope
The buyer-facing creation of one multi-item RFQ:

entry → add items (catalogue / manual / file, mixed) → delivery city, optional approximate area, approximate timing → official invoice and notes → guest authentication if needed → review → submit → submitted → track in Buyer Account.

- Abadin receives, reviews/classifies and routes **per item**. The buyer never selects a supplier.
- There is no cart, checkout, order, payment or purchase confirmation.
- Post-submission list and detail belong to Milestone 11 (Buyer Account) and were not redesigned. «مشاهدهٔ استعلام» leads to RFQ Detail `518:5780` / `519:116143`.

## Owner approval
- Owner approved Milestone 12 on 2026-10-07, including the final visual fixes below.
- Form-scope decisions DL-045, DL-046 and DL-047 are final and synced into PRD §19.3 (see Product Decisions).

## Figma IDs (file Qwx3QpLbhwbouq12QLvAL5)
- Page «RFQ Create» `553:387`; documentation frame `560:7686`.

### Full pages
| Destination | 1440 | 375 |
|---|---|---|
| Step 1 «اقلام» | `553:8677` | `553:131564` |
| Step 2 «تحویل و جزئیات» | `553:129202` | `553:131787` |
| Step 3 «بازبینی و ثبت» (signed in) | `553:129915` | `553:131879` |
| Submitted | `553:130561` | `553:132241` |
| RFQ globally unavailable | `553:131114` | `553:132343` |

### Supporting boards
| Board | ID | Contents |
|---|---|---|
| A · Item entry — desktop | `555:3013` | A1–A12: empty, suggestions, no match, loading, selected item, manual tab, manual errors, inline edit, file tab, drag/invalid type, file row states, remove + undo |
| B · Item entry — mobile | `556:12032` | B1–B5: empty, catalogue full sheet with keyboard, manual bottom sheet with keyboard, after-add, file states |
| C · Validation and submission | `558:5156` | C1–C8: empty list, missing quantity, upload in progress, step 2 required fields, notes over limit, submitting, recoverable error (desktop and mobile) |
| D · Staged activation | `557:4184` | D1–D6: partial unsupported, nothing routable, city not active, review with unsupported row, submitted with unsupported item, mobile notice at 375 |
| E · Guest sign-in | `557:12625` | E1–E8: desktop dialog, code, wrong code, expired, locked, success, mobile sheet, code with keyboard |
| R · Responsive validation | `558:133327` | 1280 / 360 / 320 checks |

## Architecture — three steps
1. **«اقلام»** — the long, editable part: an add panel plus the editable list.
2. **«تحویل و جزئیات»** — the PRD's «محل و زمان تحویل» and «نیازهای خرید و توضیحات» merged. After DL-045/046/047, purchase requirements are only the invoice choice and notes, too small for their own step.
3. **«بازبینی و ثبت»** — review and submit.

Layout and navigation:
- **Guest authentication** sits between step 2 and review, following the PRD §9.3 order.
- **Stepper:** RFQ Stepper with «Show step 4» = false.
- **Desktop:** a form column of 816 and a sticky 360 aside. The aside holds the deep-teal «مسیر استعلام» route module (the page's contrast moment) and a privacy note.
- **Mobile:**
  - Header Back, H1, stepper, and a collapsed «استعلام چطور کار می‌کند؟».
  - A sticky action bar with a 34 safe area.
  - Bottom Nav hidden on the form steps.
- **RTL wizard:** the forward action is on the left, back on the right.

## Item entry
- **Catalogue:**
  - Typeahead (RFQ Catalog Suggestions / RFQ Catalog Match). Selecting keeps the Product ID and structured data.
  - The row is labelled «از کاتالوگ آبادین» and takes quantity + unit (unit prefilled, changeable).
  - A product already in the list shows «در فهرست» and is not added twice.
  - No prices, offers or filters — this is not a PLP.
  - No match → «افزودن دستی همین عبارت».
- **Manual:** description, quantity, unit and an optional note. The buyer is not asked for a category (RFQ-O1).
- **File:**
  - Excel/spreadsheet, PDF or image.
  - While uploading, only the transfer progress is shown; afterwards the file shows «در حال بررسی».
  - Replace or remove before submit. A retry is available on upload error, and an invalid type is rejected at the dropzone.
  - No extraction, OCR or parsing is shown or promised.
- **Mixed:** catalogue, manual and file items coexist in one RFQ. There is no separation by category and no cart semantics.
- **Remove:** immediate, with a Toast offering «بازگرداندن» (no confirmation dialog).
- **Mobile:** catalogue search in a full Sheet; manual entry in a bottom Sheet with a fixed footer (FR-G-05); files through the system picker.

## Delivery information
- **City:** «شهر تحویل», required (City Picker trigger).
- **Area:** «محله یا محدودهٔ تقریبی», optional plain text. The helper asks for a neighbourhood or area only — no exact address, street, plaque or map pin. A caption explains that the area is shown only to suppliers assigned items.
- **Timing:** «زمان نیاز», a required single choice (options in Design Assumptions).
- **Invoice:** «فاکتور رسمی نیاز دارم», one checkbox (DL-046).
- **Notes:** «توضیحات تکمیلی», optional. The helper asks the buyer not to write contact details or an exact address.
- **Not collected:** buyer or purchase type (DL-045), shipping cost or requirement (DL-047), payment terms, discount, tax, budget, contact preference, company profile, exact address.

## Staged activation and unsupported items
- **Evaluation:** only catalogue items can be evaluated, once the city is chosen in step 2. Manual items and files get no eligibility claim before Abadin classifies them.
- **Some catalogue items unsupported:**
  - A Warning names them. Each stays in the RFQ, is labelled «فعلاً برای این شهر و دسته قابل استعلام نیست» and is never sent to suppliers.
  - The rest proceed, and the RFQ stays one RFQ.
- **Nothing routable** (catalogue-only list with every item unsupported, or the city has no active scope):
  - The RFQ cannot be submitted with that city, and «ادامه» is disabled.
  - The buyer can change the city or edit the items. The list is kept.
- **Internal rules:** no lists of active cities or categories are shown.
- **Submitted page:** if an item is unsupported, it says so explicitly and never claims that every item was sent.

## Global OFF
- No creation invitations appear.
- Direct access shows «ثبت استعلام خرید عمده فعلاً در دسترس نیست», with «جست‌وجوی محصولات» and «استعلام‌های من».
- The header RFQ entry and the Bottom Nav RFQ tab are hidden.
- Existing history remains in Buyer Account.

## Authentication
- **Signed in:** no account questions. The review shows «ثبت با حساب شما» with the private verified mobile.
- **Guest:**
  - Fills everything first. «ادامه» at step 2 opens the shared Sign-in Card: a Dialog on desktop, a bottom Sheet on mobile.
  - States covered: Phone, Code, CodeError, Expired, Locked and Success.
  - On success the guest goes to the review with all data kept. Closing sign-in keeps them on step 2 with their data.
- No role selection; one verified mobile = one account.

## Review and submission
- **Review sections:** items (display rows), delivery and details with «ویرایش», «ثبت با حساب شما», and «بعد از ثبت چه می‌شود؟» (an RFQ is not an order or purchase).
- **Submitting:** the button shows Loading, back and edit are disabled, and the request is idempotent (§30).
- **Recoverable error:** a Destructive notice with «تلاش دوباره»; all data kept (FR-G-06).
- **Success page:**
  - «استعلام شما ثبت شد», the RFQ code in LTR, and a summary.
  - «آبادین اقلام را بررسی می‌کند…»; an SMS for the first response only if one arrives (RFQ-O7).
  - «این استعلام سفارش یا خرید نیست».
  - No promised response time and no guaranteed response.

## Privacy
- **Aside:** suppliers see only their assigned items, quantity and unit, city and approximate area, timing, invoice need and notes. They never see the buyer's name, mobile, email or exact address, and there is no unlock.
- **Review:** repeats «فروشندگان چه می‌بینند؟» once.

## Product Decisions
- **DL-045** — no Buyer/Purchase Type field in MVP.
- **DL-046** — «فاکتور رسمی نیاز دارم» remains one simple control; no tax or company fields.
- **DL-047** — the buyer does not enter shipping cost; shipping cost and conditions come from the Supplier response (§19.6).

All three are APPROVED by the Owner on 2026-10-07. They were recorded in commit `4adbad3` and synced into PRD §19.3 in the completion commit; §19.6 is unchanged.

## Design Assumptions (not Product Decisions)
1. Approximate timing options: «تا ۳ روز» · «تا یک هفته» · «تا یک ماه» · «زمان مشخصی ندارم».
2. The catalogue product unit is prefilled from product data and may be changed.
3. Notes have a maximum of 1000 characters.
4. Catalogue suggestions start after two characters.
5. A file that is still uploading blocks «ادامه» until it finishes or is removed.
6. RFQ Create does not separately ask for the buyer's name; it uses the authenticated account and verified-mobile context. PRD §19.3 lists «نام و شمارهٔ تأییدشده برای حساب خریدار» as account data. This is not treated as a contradiction because the name belongs to the account (Buyer Account › Account Information), but it is recorded here for development.
7. The manual-item unit list is a technical/product list.
8. Multiple files are allowed; file size and type limits are technical settings.
9. On mobile, tapping a catalogue result adds it and closes the sheet.
10. "No routable item" at submit is evaluated only from known data: catalogue categories, or a city with no active scope.

## Design System
### New (page «RFQ Item» `37:3`)
- **RFQ Draft Item** `552:128506` — the editable item row. Layouts Wide/Stacked × types Catalog, Catalog Error, Manual, File Uploading, File Ready, File Error.
- **RFQ Catalog Match** `552:128557` — one typeahead match: Default, Highlighted, Added.
- **RFQ Catalog Suggestions** `553:386` — the suggestions panel: Surface Popover/Plain × Results, No match, Loading.
- **Slot / RFQ Catalogue search** `556:11912` — content for the mobile full Sheet.
- **Slot / RFQ Manual item form** `556:11974` — content for the mobile bottom Sheet.

### Changed
- **RFQ Stepper** `61:124` — added the optional boolean «Show step 4». The default is true, so existing behaviour is unchanged.
- **RFQ Item Row** `39:115` — added Layout=Inline/Stacked, a stacked narrow-screen layout. Inline is the default, and all 68 existing instances kept the original layout.
- **OTP Input** `58:2885` (shared):
  - Cells now flex between 36 and 48 px, and the input fills the Sign-in Card `59:294`. This prevents overflow at 320; it looks the same at 375 and above.
  - Every authentication surface uses it, including Supplier Registration and Buyer Account.
  - Validation done: RFQ Create code entry at 320, and the default-width sign-in dialog rechecked.
  - Not exhaustively revalidated: every historical authentication screen. The change does not reopen completed milestones unless a real regression is found.
- **RFQ Draft Item alignment correction** (after Owner review): Wide rows are top-aligned and the actions column has a fixed width, so delete/edit icons line up with the row structure and the quantity groups align across rows.

### Owner-requested final visual fixes (preserved)
- The Step 2 action bar sits below the form content.
- Edit/Delete actions in RFQ Draft Item align with the row structure.
- Icons on green primary buttons are white, matching the button text: 22 button instances on page `553:387` now have icon strokes bound to `primary-foreground`. The Button component itself was not changed.

### Reused
- **Page shell:** Header/Desktop, Header/Mobile, Footer, Page Atmosphere, Breadcrumb, Bottom Nav.
- **Form controls:** Tabs/Tab, Input, Field, Select, Textarea, Radio, Checkbox.
- **Actions and feedback:** Button, Icon Button, Notice, Toast, Empty State, Skeleton.
- **Overlays and sign-in:** Sheet, Sign-in Card, Accordion.
- **Lists and labels:** Nav List Item, Badge.
- **RFQ:** RFQ Status, RFQ Upload `39:168`, RFQ Manual Item `39:169`.

## Responsive validation
- **Full pages designed:** 1440 and 375 (five each).

### Tested (inspected)
- **1280:** Steps 1–3; catalogue suggestions at the 736 form width.
- **360:** Steps 1–3; Submitted.
- **320:** Steps 1–3; Submitted; catalogue sheet; manual-item sheet; code entry.
- **Keyboard-open states drawn:** catalogue sheet (B2), manual sheet (B3), OTP code (E8).

### Found and fixed during QA
- **OTP overflow at 320** → OTP Input flexible cells.
- **Cramped review rows at 320** → RFQ Item Row Layout=Stacked on the mobile review.
- **Mobile timing options broke reading order when wrapping** → vertical list.
- **Mobile review section title clipped** → wraps; shorter mobile title.

### Not tested
- Unavailable page at 360 and 320.
- Boards A, C and D at 1280 and at mobile widths, except the specifically tested D6 cell at 375.
- Desktop sign-in dialog at 1280.
- Toasts at 320.
- Landscape.

## Out of Scope
- Buyer Account RFQ list/detail (Milestone 11).
- Seller RFQ response flow.
- Operator routing and classification tools.
- Activation-rule management.
- Supplier selection by the buyer.
- Checkout, order or payment.
- Post-contact tracking.
- Notification center.
- Automatic file extraction UI.
- Supplier winner.
- Purchase confirmation.

## Known limitations
- Wrapped chip/meta rows flow left-to-right in Figma; build them with RTL flex-wrap (start = right).
- File names with Latin extensions need bidi isolation in build.
- Product images are placeholders.
- The catalogue popover is drawn inline in Board A; in build it overlays content (Elevation/L2).
- Button Large has no drawn Disabled or Loading state; Board C/D use Medium for those states.
- The Bottom Nav active tab on the submitted page is set by route in build.

## Non-blocking follow-up (OPEN)
**DL-048 (OPEN):** if an RFQ contains only manual items and/or uploaded files and, after Abadin classifies them, none is eligible for routing, how is that already-submitted RFQ represented and closed for the buyer?

This is not decided and no UI state was designed. It belongs to the post-submission RFQ lifecycle and is not a blocker for this milestone.
