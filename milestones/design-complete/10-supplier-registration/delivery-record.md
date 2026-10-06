# Supplier Registration / Onboarding — Delivery record

Status: **Design Complete** — Owner approved 2026-10-06. No OPEN item remains. The next milestone is NOT started.

Scope: راهنمای فروشندگان → «ثبت فروشگاه» → auth if needed → store information → submit → Pending Review → manual activation → entry to the active seller panel. Out of scope: Internal Operator UI and the full Supplier Panel (only status / correction / active-landing screens are designed).

## Figma IDs (file Qwx3QpLbhwbouq12QLvAL5)
- Page «Supplier Registration» `484:2`; doc frame `499:103888`.
- Full pages:
  - Seller Guide «راهنمای فروشندگان»: 1440 `484:3` · 375 `492:98636`
  - Step 1 «فروشگاه و موقعیت»: 1440 `488:645` · 375 `489:1192`
- Steps 2–4 + Review, desktop board `490:1301` (form column 816; aside as in Step 1): Step 2 `490:1302` · Step 3 `490:1471` · Step 4 `491:1678` · Review `492:2`
- Steps 2–4 + Review, mobile 375 board `492:97699`: Step 2 `492:97700` · Step 3 `492:97886` · Step 4 `492:98185` · Review `492:98311`
- Auth & entry board `493:15`: guest sign-in Dialog (desktop) · bottom sheet (375) · account menu before/after · signed-in start
- Registration status, desktop 1440 board `494:15`: Pending `494:26` · Needs Correction `494:582` · Cannot Be Activated `494:1177` · Active landing `494:1594`
- Registration status, mobile 375 board `494:100821`: Pending `494:100822` · Needs Correction `494:100994` · Cannot Be Activated `494:101223` · Active `494:101298`
- Validation & error states board `496:15` (10 cases)
- Targeted validation board 1280 / 360 / 320 `496:101428` (+ keyboard open 360 `499:103786`)

## Flow and architecture
- Four steps + review: ۱ فروشگاه و موقعیت · ۲ فعالیت و ارسال · ۳ راه‌های تماس · ۴ اطلاعات هویتی → بازبینی و ارسال.
  - Why: all PRD data is collected before submit (nothing shortened, nothing moved after submit); steps group data by meaning and by visibility, keep mobile screens short, and the review shows public vs Abadin-only data before the irreversible submit.
  - RFQ Stepper reused with label overrides. RTL wizard: forward action left, back right.
- Auth: OTP only when the user is a guest (Dialog desktop / bottom sheet mobile), then straight back to Step 1. One account per mobile; buyer and seller share it; no role picker; account data never asked again.
- Account menu: «ثبت فروشگاه» while no request exists; «پنل فروشنده» from submit onward, in every status. No status in the menu.
- Submit ≠ activation → Pending Review. No ETA.
- States:
  - **Pending Review:** read-only; submitted data shown without edit; no public profile, publishing or RFQ.
  - **Needs Correction:** section-level. Only sections flagged by Abadin are editable (with the operator note); all others locked. «ارسال دوباره برای بررسی» returns the request to Pending Review.
  - **Cannot Be Activated:** closed result, no reason shown, only «تماس با پشتیبانی».
  - **Active:** landing only — «ورود به پنل فروشنده», «مشاهدهٔ صفحهٔ فروشگاه».
  - Paused / Suspended: documented only (panel scope).

## Data (PRD)
- Public: name (required, not unique, not trademark proof), logo (optional, default avatar fallback), city (required), address (optional), map pin (optional), service area (optional, separate from location), categories (≥1), brands (optional, multi), public mobile + up to 3 responsive messengers (≥1 channel), description (optional, plain text, ≤500, no phone / link / approval claim), weekly hours (optional, no holidays).
- Account mobile is private; the public mobile is filled from it only by an explicit link action.
- Abadin-only: website (no badge), social presence (not public, not a contact channel), identity.
- Identity:
  - حقیقی: نام · نام خانوادگی · کد ملی
  - حقوقی: نام ثبتی شرکت/مجموعه · شناسهٔ ملی · نام نماینده · نام خانوادگی نماینده
  - Internal only, no badge. No representative role, representative national code or document upload.
- Every section carries «نمایش عمومی» or «فقط برای آبادین».

## Resolved from PRD (no new product decision)
1. Service Area: optional, not an activation condition. Store City stays independent and required.
2. Draft persistence: not designed in MVP — no auto-save, resume draft or draft status.
3. Cannot Be Activated: no reason; only «تماس با پشتیبانی». The reason requirement belongs to Suspended only.
4. Needs Correction: section-level; only flagged sections editable; others locked; resubmit → Pending Review.
5. Terms acceptance: no checkbox or blocking acceptance before submit (not in the PRD).

## Final Owner changes (round 2, 2026-10-06)
- **Category selector:** search + removable chips (like brands). Abadin categories only, no free text, no subcategories, ≥1 required. An already selected category is checked in the suggestions and is not added twice. Applied to Step 2 (1440, 375, 360, 320), review / status summaries and validation case 7.
- **Image Upload** `502:225` replaces Logo Upload `482:144` in Registration (Logo Upload kept, marked deprecated).

## Design System
- New (page «Supplier Onboarding» `481:95668`): Form Section Header `481:95693` · Checklist Item `481:95706` · Contact Channel Input `482:52` · Weekly Hours Row `482:77` · Image Upload `502:225` · Registration Status Card `483:199` · Icon/lock `481:5` · Icon/eye `481:11`.
- Deprecated: Logo Upload `482:144`.
- Systemic changes:
  - Field `23:245`: helper text wraps (all Fields; no visual change at desktop widths).
  - Textarea `23:265`: min-height 112.
  - City Picker `466:191`: + Multi-select (Popover / Sheet).
  - Weekly Hours Row: + Layout=Stacked (mobile).
  - Contact Channel Input: + Layout=Stacked (mobile); type select 150 → 120.
  - Registration Status Card: actions wrap, right-aligned.
- Reused: Field, Input, Select, Textarea, Checkbox, Chip, Notice, Button, Icon Button, Menu, Segmented Control, Sign-in Card, Account Menu, Workspace Switch, RFQ Stepper, SupplierCard, Header, Footer, Bottom Nav.
- Recommendation (not done): rename RFQ Stepper to a generic Stepper.

## Responsive validation
- Full pages designed: 1440 and 375.
- Tested (inspected):
  - 1280: Step 1 page (form + aside), Needs Correction.
  - 360 and 320: Steps 1–4, Review, Needs Correction, Active landing.
  - 320: Seller Guide.
  - 360: keyboard open (focused field, sticky bar above keyboard, safe area 34).
  - Image Upload Uploaded state at 288px content width (320 viewport).
- Issues found and fixed: contact value too narrow (Stacked variant); hours row overflow (Stacked variant); review header squeezing titles (stacked header on mobile); status-card buttons overflowing (wrap); guide sample card and bottom nav overflowing at 320; Steps 2–4 steppers showing RFQ labels; vertical clipping; Image Upload info collapsing at 320 (actions moved under the file name).
- Known Figma limitation: wrapped chip lists flow left-to-right in Figma; build with RTL flex-wrap (start = right).
- **Not tested:** Seller Guide at 360 and 1280; Pending and Cannot Be Activated at 360 / 320; OTP sheet at 320; validation cases at mobile widths (components only); landscape.

## Assumptions
- One entry per messenger type (duplicates blocked).
- Identity validation is format-only (digit count / check digit); matching is Abadin's review.
- Logo / image format and size limits are a technical setting.
- Status screens live at the seller-panel entry; the full panel shell is out of scope.
- On Pending, the applicant sees their own submitted data in full.
