# Seller Panel — Dashboard & Store Status (Milestone 13A) — Delivery record

Status: **Design Complete** — Owner approved 2026-10-10. Milestones 13B and 13C have NOT been started.

## Scope
The foundation of the Seller Panel:
- **Shell:** desktop sidebar, mobile hub, workspace identity, «بخش خریدار» switch and logout.
- **Active-store dashboard.**
- **Seller-paused dashboard.**
- **Status-focused views:**
  - Pending Review, Needs Correction and Cannot Be Activated reuse the approved Milestone 10 screens.
  - Suspended is new in this milestone.
- **Interactions and states:** pause/reactivate interactions; navigation states; empty, loading and error states.

Dashboard modules link to 13B/13C destinations without designing them: products & prices, price sources, reviews, received RFQs.

## Owner approval
- Owner approved the delivered design and authorized closure on 2026-10-10.
- Product decisions DL-049, DL-050 and DL-051 are APPROVED and synced into PRD §22.1/§22.2.

## Figma IDs (file Qwx3QpLbhwbouq12QLvAL5)
Page «Seller Panel — Dashboard & Status» `582:25271` (after RFQ Create); documentation frame `586:8661`.

### Full pages
| View | 1440 | 375 |
|---|---|---|
| Active dashboard | `582:25272` | `582:25327` |
| Dashboard — paused by seller | `583:136783` | `583:137074` |
| Status view — Suspended | `583:138061` | `583:138073` |

### Status views reused from Milestone 10 (not redesigned)
| View | 1440 | 375 |
|---|---|---|
| Pending Review | `494:26` | `494:100822` |
| Needs Correction (approved section-level correction flow) | `494:582` | `494:100994` |
| Cannot Be Activated | `494:1177` | `494:101223` |

### Boards
| Board | ID | Contents |
|---|---|---|
| S · Store status | `583:138551` | Access matrix (6 statuses); Registration Status Card states: Pending, NeedsCorrection, CannotActivate, Suspended with reason, Suspended without reason |
| P · Pause / reactivate | `584:2990` | P1 pause confirm (desktop) · P2 processing · P3 recoverable error · P4 paused result · P5 reactivate confirm (desktop) · P6 reactivated result + reactivation error · P7 / P8 mobile bottom sheets |
| N · Navigation, empty, loading, error | `585:5240` | N1 account-menu entry · N2 desktop nav · N3 mobile nav · N4 «بخش خریدار» · E1–E5 empty states · L1 loading · X1 module error |
| R · Responsive validation | `585:5654` | 1280 / 360 / 320 checks |

## Navigation
- **Shell:** the same as Buyer Account (Milestone 11):
  - public Header (Internal) and the breadcrumb «خانه › پنل فروشنده»;
  - **Account Nav · Supplier · Sidebar** (280, sticky) beside an 880 content column.
- **Nav contents:**
  - identity: store avatar, store name, «پنل فروشنده»;
  - Workspace Switch «بخش خریدار» → Buyer Account Overview `511:2` / `512:2`;
  - destinations: داشبورد · وضعیت و اطلاعات فروشگاه · محصولات و قیمت‌ها · منابع قیمت · نظرها · استعلام‌های دریافتی (private counter only);
  - خروج از حساب.
- **Mobile 375:**
  - The dashboard is the panel hub: status → notices → pending actions → Account Nav · Supplier · Mobile → modules.
  - Sub-pages (13B/13C) use Header Back.
  - Bottom Nav is hidden in the seller panel.
- **Entry:**
  - The account menu shows only «پنل فروشنده» and never a status (FR-G-04A).
  - Active and Paused open the dashboard; every other status opens its status view.
  - No separate seller login and no role selection.

## Store-status access (DL-049, DL-050, DL-051)
| Status | Panel view | Public store & offers | New RFQs | Permitted actions |
|---|---|---|---|---|
| Active | Full dashboard | Shown | Assigned | All management; «توقف موقت فروشگاه» |
| Paused by seller | Full dashboard with restrictions | Not shown (DL-017, DL-050) | Not assigned (DL-050) | Answer earlier RFQs; manage products and prices; reply to existing reviews; «فعال‌سازی دوباره» (DL-050, DL-051) |
| Pending Review | Status view, read-only | Not created | None | View status and submitted data |
| Needs Correction | Status view | Not created | None | Edit only flagged sections; «ارسال دوباره برای بررسی» (DL-038) |
| Cannot Be Activated | Closed outcome | Not created | None | «تماس با پشتیبانی» only; no reason (DL-037) |
| Suspended | Status view | Not shown (DL-017) | None (design assumption) | Reason only when Abadin provides one; «تماس با پشتیبانی» for questions or appeal; no reactivation |

## Dashboard modules (real data only)
1. **Store status (identity):**
   - Shows avatar, name, city, the store's own product count on its public page, status badge, and a plain-language effect on public visibility.
   - Active actions: «مشاهدهٔ صفحهٔ فروشگاه», «توقف موقت فروشگاه».
   - Paused action: «فعال‌سازی دوباره».
2. **Important notices (Warning):**
   - A price-source error, with its last successful run.
   - Broken direct product URLs: the outbound action is hidden for those offers (§22.3).
   - On the paused dashboard, an Info notice explains the pause effect (DL-050).
3. **Pending actions** (Seller Pending Action rows, each with a destination):
   - received RFQs awaiting a response, with the nearest exact deadline in neutral colour;
   - unanswered reviews.
4. **Received RFQs:** the latest assignments (RFQ Summary Row · Supplier). Each shows status, deadline, items for you and city/area, never buyer identity. Up to 3 on desktop and 2 on mobile.
5. **Products & prices:**
   - Private counts with a clear meaning: in your list / available / unavailable.
   - The last price update as relative time, with no «قیمت قدیمی» label.
   - «افزودن محصول».
6. **Price sources:** name, last run time, and success/error.
7. **Latest unanswered review** → «مشاهده و پاسخ» (the review page, P0-5A).

The dashboard shows no sales, revenue, views, conversion, orders or other unsupported analytics.

## Pause / reactivation (Board P)
- **Pause:**
  - Dialog on desktop, bottom Sheet on mobile, explaining the effects.
  - «توقف فروشگاه» / «انصراف» → Loading (cannot be repeated) → success Toast → paused dashboard.
  - A recoverable error keeps the dialog open, with an error Toast and «تلاش دوباره».
  - Nothing is deleted.
- **Reactivation (DL-051):**
  - Same confirm pattern: «فعال‌سازی دوباره» takes effect immediately after successful confirmation, with no new Abadin review.
  - Normal Active visibility and RFQ eligibility then apply.
  - Failure shows a recoverable error and never a success message.
  - Only for a store its seller paused. It never bypasses suspension or any other blocking restriction; the Suspended view has no reactivation action.
- **Not drawn:** a separate "reactivation in progress" frame. It follows the same Loading pattern as pause (P2).

## Approved Product Decisions
- **DL-049** — Seller Panel access architecture: dashboard for Active and seller-Paused stores; status-focused views for Pending Review, Needs Correction, Cannot Be Activated and Suspended. In PRD §22.1/§22.2.
- **DL-050** — seller-paused permissions: not public; no new RFQ assignments; earlier RFQs, product/price management and replies to existing reviews remain permitted; the seller may request reactivation. In PRD §22.2.
- **DL-051** — reactivation of a seller-paused store is immediate after successful confirmation, needs no new review, never bypasses suspension or other blocks, applies normal Active rules afterwards, and shows a recoverable error on failure without indicating success. In PRD §22.2.
- **Existing decisions applied:**
  - DL-017: only Active stores are public.
  - DL-037: Cannot Be Activated shows no reason.
  - DL-038: section-level correction.
  - P0-5A: reviews flow.
  - RFQ-O9: «استعلام‌های دریافتی».
  - FR-G-04A: no status in the account menu.

## Design Assumptions (not Product Decisions)
1. Suspended has no in-product appeal form; questions and appeals go through «تماس با پشتیبانی».
2. A suspended store receives no new RFQs.
3. The dashboard shows at most 3 received RFQs (2 on mobile) and only the single latest unanswered review.
4. Notices appear only for real operational problems: price-source error, broken direct URL.

## Design System
- **New:**
  - **Seller Pending Action** `582:136850` (page Supplier Onboarding `481:95668`):
    - Variants: Tone Default/Attention × State Default/Hover.
    - Props: Title, Meta, Show meta, Count, Show count, Icon.
  - **Slot / Seller store status confirm** `583:138760`: sheet content for the mobile pause/reactivate confirmation.
- **Changed — additive, existing uses unchanged:**
  - **Registration Status Card** `483:199`: + Status=Suspended, + «Show reason».
  - **RFQ Summary Row** `41:1094`: + Audience=Supplier, Layout=Stacked. The 5 existing supplier instances remain Default.
- **Changed — systemic:**
  - **Account Nav** `48:636`: the identity name wraps instead of overflowing (all 4 variants).
  - Buyer Account (M11) nav `511:10` / `512:545` was rechecked and is visually unchanged.
- **Reused:**
  - Shell: Header/Desktop, Header/Mobile, Footer, Page Atmosphere, Breadcrumb.
  - Account: Account Nav (Supplier), Account Menu, Workspace Switch, Avatar (Store), Badge.
  - Feedback: Notice, Button, Dialog, Sheet, Toast, Empty State, Skeleton.
  - Domain: RFQ Summary Row, Registration Status Card.

## Responsive validation
- **Designed:** full pages at 1440 and 375 (Active, Paused, Suspended).

### Tested (inspected)
- **1280:**
  - Active dashboard with a long store name (content 800 + nav 280).
  - Paused dashboard.
- **360:** Active, Paused, Suspended.
- **320:** Active (long store name), Paused, Suspended.

### Found and fixed
- A long store name was clipped in the status module → it now wraps.
- A long name overflowed the Account Nav identity → systemic wrap fix.
- Supplier RFQ rows truncated deadlines on mobile → new Supplier Stacked layout.
- Pending-action notes were too long on mobile → shorter copy.

### Not tested (Owner approval does not change this)
- Pause/reactivate dialogs at 1280.
- Mobile pause/reactivate sheets at 360 and 320.
- Board N empty, loading and error states at mobile widths.
- Toasts at 320.
- Landscape.
- Milestone 10 status views at 360/320 beyond what Milestone 10 recorded.
- At 360/320 the pending-action rows wrap their text into a narrow column. Nothing overflows, but it is the tightest layout on the page.

## Out of Scope
- Product management, the pricing editor and price-source configuration (13B).
- Review management pages (13B).
- Supplier RFQ list, detail and response (13C).
- Operator tools.
- Sales analytics.
- Checkout, payments and orders.
- Account deletion (P0-4D).
- Not redesigned: onboarding/correction forms (M10), the buyer workspace (M11) and RFQ Create (M12).

## Known limitations
- Wrapped chip and meta rows flow left-to-right in Figma; build them with RTL flex-wrap.
- Empty-state icons use the Empty State default icon.
- The Bottom Nav is absent in the seller panel by design; its active tab elsewhere is set by route.
