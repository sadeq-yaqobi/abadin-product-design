# Abadin Design System — decisions & status

Updated: 2026-09-30 (۸ مهر ۱۴۰۵)

> **STATUS (2026-09-30): Round 4 — Modern Marketplace is APPROVED as Abadin’s visual direction** after convergence, navigation completion, final header/PDP correction and footer integration. Rounds 1–3 remain historical exploration only. The production Design System has NOT yet been migrated to Round 4; existing production components/templates may therefore reflect the older direction. Next step: document the approved visual direction, then migrate the production Design System without changing PRD product behaviour.

## Direction (owner decisions)
- The Figma design system is built on **shadcn/ui** structure and naming.
  - No other shadcn kit is imported.
  - Visuals and tokens are Abadin's own.
- From the earlier Claude Design artifact, only the approved brand colour carries over. Everything else in that artifact is superseded.
- **Foundations:** Round 4 is now the approved visual direction. Production tokens/components still need migration. Fixed across the approved direction: RTL, Vazirmatn, accessibility requirements, 44px targets, light theme, `#0b6264` as the brand anchor, and the updated border/elevation principle. Exact production token mapping is a Design System migration task. The original foundation list:
  - token architecture;
  - semantic colours, spacing, radius, sizing and typography;
  - RTL-first approach;
  - the border/elevation rule: borders and dividers provide structure; shadows are used for genuine elevation or floating hierarchy (for example scrolled/floating header, menus, popovers, dialogs, sheets, drawers, persistent floating bars, hover elevation), not as a default treatment for every card.
- **Light theme only.** The PRD confirms this (P1-25). Semantic tokens keep a later dark mode possible.
- **Icons:** Lucide is the base set, managed through the `Icon/<lucide-name>` contract.
  - The owner installed the Lucide Figma plugin.
  - Claude cannot run Figma plugins through the MCP, so Claude draws new icons from Lucide path data and normalises them to the contract: 24px, stroke 2, stroke bound to `foreground`, named `Icon/<name>`.
- **Default avatar (owner decision, 2026-09-29):**
  - A single default avatar for users and stores (FR-G-07, P1-23), never first-letter initials.
  - It is the `Avatar` component: User is a circle, Store is a rounded square. `Content=Default` is a Lucide user or store glyph on the `accent` fill.
- **RFQ response terms (owner decision, 2026-09-29):**
  - Delivery time, shipping, formal invoice and general notes are ALL optional. None of them blocks sending a response.
  - Only price validity is required: today / 24h (default) / 3d / 7d.
- **One account, two workspaces (PRD: FR-G-04, FR-G-04A, P0-7, §8.3, §20, §21; revised PRD 2026-09-29):**
  - One verified mobile number gives one account, and that account can be both buyer and supplier.
  - There is no role picker at sign-in.
  - The account menu and buyer account show exactly one of two entries:
    - a neutral «پنل فروشنده» for any account with a store request or store;
    - «ثبت فروشگاه» for accounts with none.
  - The menu never shows any request or store status: in review, needs fixes, active, inactive, or closed. Status and the right action appear only inside the seller panel.
  - A store request closed with «امکان فعال‌سازی وجود ندارد» is covered by the same rule: that account sees the neutral «پنل فروشنده», and the panel shows the status and the support action.
  - The seller panel shows «بخش خریدار».
  - The switch is not a sixth buyer destination. It does not log the user out, and data is not merged.
- **Pattern decisions (owner, 2026-09-29):**
  - **Offer order:** available offers with a price may come first. The order *within* that group is an **OPEN decision**. No ranking or priority rule for sellers is defined, and no seller is highlighted as better, winner or recommended.
  - **Sort options:** «مرتبط‌ترین» (default), «کمترین قیمت», «بیشترین قیمت». They are only sorting and must never become a «بهترین قیمت» claim or an Abadin recommendation.
  - **OTP length:** mockups may show 6 digits, but the length is not a fixed design-system rule. OTP Input supports 4, 5 or 6 digits ("Show cell 5/6"). The final value comes from the SMS provider.
  - **Buyer inquiry tabs:** «مقایسهٔ پاسخ‌ها / فهرست اقلام / فایل‌ها» is approved for now. If «فایل‌ها» lacks enough content for its own tab when designing the template, review it again.
  - **Purchase/buyer type:** no field. It stays out of the RFQ flow until a routing use is defined.
- **RTL wizard convention (design decision):** in step-by-step flows, the forward action («ادامه») sits on the left and «بازگشت» on the right. Non-directional action bars (dialogs, response actions) keep the primary action at the start (right).
- **Hierarchy:** Foundations → UI Components → Abadin Domain → Patterns → Templates.
- **Build order:** reviewable stages. Product behaviour always comes from the current PRD; no new requirements are invented for undefined cases.
- Design work happens in Figma. See `claude/working-rules.md`.

## Brand colour
- Firouzeh-teal `#0b6264`. APPROVED as the primary brand anchor for the Round 4 visual direction.

## Figma file
- **Abadin — Design System**, sadeq's team (plan: Pro): https://www.figma.com/design/Qwx3QpLbhwbouq12QLvAL5
- **Page order:**
  1. Cover
  2. Foundations
  3. —— UI Components ——
  4. Icons, Button, Input & Field, Textarea, Select, Checkbox, Radio, Switch, Avatar, Badge, Chip, Tabs, Tooltip, Notice, Skeleton, Empty State, Dialog, Sheet, Separator, Breadcrumb, Pagination
  5. —— Abadin Domain ——
  6. SearchField, Price, AvailabilityBadge, SaveToggle, ProductCard, SupplierCard, OfferRow, ContactMenu, Category Tile, RFQ Status, RFQ Item, RFQ Supplier Response, RFQ Buyer Response, Site Header, Mobile Nav, Account Nav, Site Footer
  7. —— Patterns ——
  8. Offers Section, Product Grid, Filter & Sort, OTP Sign-in, RFQ Create Flow, RFQ Response Flow
  9. —— Templates ——
  10. Home, Search Results, Product Page
- Every page has a Persian doc header. Bullet lines are RLM-prefixed.
- **Technical notes for future builds:**
  - When binding colour variables, also pass the resolved colour as the paint's fallback colour. Otherwise overrides inside nested instances render black.
  - A TEXT component property on a variant set shares one value across all variants. Do not bind variant-specific copy (titles, quantities) to a set-level text property.
  - When wiring component properties, look up the target by direct child, not `findOne`. Otherwise it can match a layer inside a nested instance, which throws an error.
  - Set `isExposedInstance` only after the instance has been appended inside the component.
  - Space-separated digit groups (a phone number such as «۰۹۱۲ ۳۴۵ ۶۷۸۹») reorder inside RTL text. Write phone numbers without spaces, or isolate them as LTR.
  - Button Size=Large has only a Default state. Use Medium for Loading and Disabled.
  - Always read property keys (e.g. `Count#66:4`) from the set before calling `setProperties`; do not guess the suffix.
- The IDs below are the durable record.

### Foundations (approved)
- **89 variables:** Primitives 35, Color 28 (Light), Spacing 13, Radius 7, Size 6.
- **Text styles:** 14, Vazirmatn.
- **Shadows:** 4.
- **Docs page.**
- **Cover:** `23:99`. The thumbnail must be set manually.

### Stage 1 — UI components (done)
| Component | ID | Notes |
|---|---|---|
| Icons | page Icons | 47 icons, Lucide contract. Stage 3 added clock, paperclip, trash-2, pencil, send and calendar. Stage 4 added house, layout-grid, layout-dashboard, message-square, log-out, package, link and factory (factory is used for brands). |
| Button | 5:291 | 6 variants × Default / Hover / Focus / Disabled / **Loading**, plus Small and Large |
| Icon Button | 26:337 | 44×44 |
| Input | 23:210 | |
| Field | 23:245 | |
| Textarea | 23:265 | |
| Select | 23:307 | Includes Menu Item `23:286` and Select Menu `23:308` |
| Checkbox | 23:373 | |
| Radio | 23:401 | |
| Switch | 23:432 | |
| Avatar | 30:56 | Type User / Store × Content Default / Image × Size 32 / 40 / 64 |
| Badge | 26:40 | |
| Chip | 26:115 | |
| Tab | 26:142 | Tabs list `26:143` |
| Tooltip | 26:178 | |
| Notice | 26:230 | |
| Skeleton | 26:238 | |
| Empty State | 26:248 | |
| Dialog | 26:338 | |
| Sheet | 26:477 | |

### Stage 2 — Abadin domain, discovery journey (done 2026-09-29)
| Component | ID | PRD rules applied |
|---|---|---|
| SearchField | 31:74 | Header 44 / Hero 52 × Default, Focus, Filled. Search Suggestions popover `31:75` (product, brand, category). |
| Price | 30:116 | From (P1-8); Seller with relative «به‌روزرسانی قیمت: ۳۰ دقیقه پیش» (P1-12), updated line switchable; Summary with lowest price and range; Unpriced; Unavailable with no price (P1-21). |
| AvailabilityBadge | 30:85 | Only Available / Unavailable (P1-22); built on Badge. |
| SaveToggle | 30:141 | Heart on the image, Saved × Default / Hover / Focus (P1-11A). |
| ProductCard | 33:154 | Context Search / Supplier × Price Priced / Unpriced / Unavailable. No seller count. Supplier context shows the seller's own price and no compare CTA (P1-20). |
| SupplierCard | 33:376 | Store avatar, name, city, categories, delivery, optional brands, CTA «مشاهده محصولات و قیمت‌ها». No rating, counts or contact (P1-19). |
| OfferRow | 35:311 | Case Site / Contact / Unpriced / Unavailable / NoAction × Layout Desktop / Mobile. Seller shows name and delivery only (P1-24). Actions follow the §15 matrix and C-01. |
| ContactMenu | 34:91 | Context Offer / RFQ (with RFQ-code reminder). Contact Item `34:52`: Channel Mobile / WhatsApp / Telegram / Eitaa / Bale × State; mobile first, at most 3 messengers. |
| Category Tile | 66:28 | Default / Hover / Focus. Image, name, real product count (Show count off when there is no real data). P1-13. Added with the Home template. |

### Stage 3 — Abadin domain, RFQ (done 2026-09-29)
| Component | ID | PRD rules applied |
|---|---|---|
| RFQ Status | 38:270 | Built on Badge. Scope Buyer (در حال بررسی / ارسال‌شده برای فروشندگان / N پاسخ رسیده / بسته شد), Supplier (جدید / پیش‌نویس / پاسخ ارسال شد / بسته شد), Item (قیمت داده شد / ناموجود / تأمین نمی‌کند / امکان تأمین ندارم / بدون پاسخ / اعتبار قیمت تمام شده / خارج از محدودهٔ استعلام). §19.5, RFQ-O5, RFQ-O12. |
| RFQ Summary Row | 41:1094 | Audience Buyer / Supplier. Public code RFQ-1405-000123 (P0-6). The supplier row shows no buyer identity (RFQ-O2). |
| RFQ Item Row | 39:115 | Type Catalog («از کاتالوگ آبادین») / Manual / File («در حال بررسی», no auto-extraction promise) / OutOfScope (never routed). Removable boolean. RFQ-O1, RFQ-O12. |
| RFQ Upload | 39:168 | Default / DragOver / Error. Excel, PDF or image. |
| RFQ Manual Item | 39:169 | Description, quantity, unit (Select), optional note. Category is not required. |
| RFQ Item Response | 40:155 | Response Unset / Priced / Unavailable / CannotSupply. Unit price only in the buyer's unit (RFQ-O6). Partial quantity only if lower than requested. Optional item note. |
| RFQ Response Terms | 40:156 | All general terms optional (owner decision above): delivery time, shipping, formal invoice, general notes (payment, discount and tax go here). Only price validity is required, default «۲۴ ساعت». RFQ-O4, RFQ-O5. |
| RFQ Deadline | 40:225 | Open / Passed. Exact date plus time remaining, neutral colour, no urgency. |
| RFQ Response Actions | 40:272 | «ارسال پاسخ» plus «ذخیرهٔ پیش‌نویس»; Disabled after the deadline. |
| RFQ Comparison Line | 40:1037 | Result Priced / Partial / Expired / Unavailable / NotSupplied / NoResponse. Expired price is muted, not struck through, so it cannot read as a discount. No "best" label. |
| RFQ Item Comparison | 40:1038 | Item-centric comparison (RFQ-O3): item header plus lines. |
| RFQ Supplier Response Card | 41:325 | Validity Valid / Expired. Trust signals: name, city, service area, optional rating, time on Abadin (RFQ-O10). No profile link, no verified badge. CTA «ادامه با این فروشنده» → ContactMenu RFQ. |

- The buyer's only management action, «بستن استعلام», uses Button Outline plus a Dialog confirmation. It needs no new component.
- Catalogue add uses SearchField plus Search Suggestions. It needs no new component.

### Stage 4 — Navigation and structure (done 2026-09-29)
| Component | ID | Notes |
|---|---|---|
| Separator | 44:138 | Horizontal / Vertical × Default (border) / Strong (border-strong). 1px. |
| Breadcrumb Item | 45:159 | Link / Current / Ellipsis × states. |
| Breadcrumb | 45:193 | Desktop / Mobile (collapsed middle, truncated current). Chevron-left separator (RTL). SEO BreadcrumbList (§28). |
| Pagination Item | 45:215 | Page / Current / Ellipsis, 44×44. |
| Pagination | 45:267 | Desktop («قبلی» / pages / … / «بعدی», reusing Button Ghost) / Mobile (Icon Buttons plus «صفحهٔ N از M»). |
| Logo | 47:40 | **Placeholder** wordmark «آبادین» in primary. The final logo is still not designed. |
| Nav Link | 47:60 | Default / Hover / Active / Focus; Show chevron. |
| Account Trigger | 47:92 | Guest «ورود / ثبت‌نام» / SignedIn «حساب من» / SignedInOpen. |
| Site Header | 47:181 | **PRE-R4 production component;** behavior rules remain relevant, but visual structure is superseded by the approved Round 4 header and must be migrated. Show RFQ entry only when RFQ is on (§19.9). |
| Bottom Nav Item | 47:198 | Default / Active / Focus. |
| Bottom Nav | 47:270 | RFQ On (5 tabs: خانه، دسته‌بندی‌ها، استعلام عمده، ذخیره‌شده‌ها، حساب من) / Off (4 tabs). Hidden on form pages and in the seller panel. |
| Mobile Menu | 49:463 | Right-side drawer, Guest / SignedIn; all main and organisational destinations; Show RFQ entry. |
| Nav List Item | 47:450 | Shared row for menus: Default / Hover / Active / Focus / Destructive; Icon, Show badge (private RFQ counters only), Show chevron. |
| Workspace Switch | 54:437 | FR-G-04A (revised). Target SellerPanel (neutral «پنل فروشنده», no caption, no status; also Hover / Focus) / RegisterStore («ثبت فروشگاه») / BuyerArea («بخش خریدار», inside the seller panel). The status variants were removed. A bordered card with an arrow, visually distinct from nav rows so it reads as "change workspace". |
| Account Nav | 48:636 | Buyer (exactly the five P0-4 destinations, plus a Workspace Switch on top, exposed) / Supplier panel (§8.3, «استعلام‌های دریافتی», plus a Workspace Switch «بخش خریدار») × Sidebar / Mobile. |
| Account Menu | 48:637 | Popover from the desktop header (Shadow/md). A Workspace Switch (exposed) sits on top, then the five buyer destinations, then «خروج از حساب». |
| Footer Link Group | 50:23 | Column / Collapsed / Expanded (mobile accordion). |
| Site Footer | 50:83 | **PRE-R4 production component;** content/IA rules remain relevant, but the visual treatment is superseded by the approved Round 4 integrated architectural footer and must be migrated. The intro says Abadin is not a shop. Support phone and email are explicit [ ] placeholders (BIZ-01). No legal badges until launch (BIZ-02). «ثبت فروشگاه» appears without any plan or fee (BIZ-03). |

- Request and store status (in review, needs fixes, inactive, closed) belongs in the seller panel's own status screens. Those screens are designed with the seller-panel templates.

### Stage 5 — Patterns (done 2026-09-29; owner decisions applied)
| Pattern / component | ID | Notes |
|---|---|---|
| Offers Section | 57:432 | Desktop (table with dividers) / Mobile (stacked cards). Price Summary with «قیمت مشاهده‌شده، نه قیمت قطعی خرید», no seller count; OfferRows per §15. Available offers with a price first; in-group order OPEN; no highlighting. |
| Filter Group | 57:486 | Options (checkboxes, no counts, «نمایش همه») / Price (از–تا, comparable unit) / Collapsed. |
| Filter Panel | 57:656 | Desktop sidebar (instant apply, «پاک‌کردن همه») / Mobile full-screen with fixed footer «اعمال فیلتر» + «پاک‌کردن» (P1-15, P1-16). |
| Sort Sheet | 58:151 | Mobile short sheet, single-select Radio, applies immediately, no footer. Options approved: مرتبط‌ترین (default) / کمترین قیمت / بیشترین قیمت. |
| Results Toolbar | 58:278 | Query title, dynamic result count, removable active-filter chips, «پاک‌کردن همه»; Desktop sort Select; Mobile «فیلتر» (active dot, no count) + sort button. |
| Product Grid | 58:981 | Results Desktop (3 columns next to the filter panel) / Mobile (2 columns) + Pagination; NoResults with «پاک‌کردن فیلترها» and the RFQ entry only when RFQ is on. |
| OTP Input | 58:2885 | Variable length 4–6 via "Show cell 5" / "Show cell 6" (mockups show 6). LTR digit order, Persian digits; Empty / Typing / Filled / Error / Disabled. |
| Sign-in Card | 59:294 | Steps: Phone / Sending / Code / CodeError / Expired / Locked / Success. Dialog on desktop, Sheet on mobile. |
| RFQ Stepper | 61:124 | Desktop 4 steps / Mobile «مرحلهٔ N از ۴» + progress bar. |
| RFQ Create Step | 62:485 | Items / Delivery / Details / Review / Submitted / Unavailable (global off) / NotRoutable (nothing routable). No purchase-type field. |
| RFQ Assignment Header | 62:3061 | Supplier: Open / Draft / Sent / Closed; deadline plus request info only (no buyer identity). |
| RFQ Buyer Header | 62:3140 | Buyer: InReview / Responses / Closed; only action «بستن استعلام». |
| Example frames | 62:3141, 62:3318 | Supplier responds (desktop), buyer compares (desktop, tabs «مقایسهٔ پاسخ‌ها / فهرست اقلام / فایل‌ها»); compositions, not components. |

### Stage 6a — Templates: discovery (done 2026-09-29, awaiting review)
| Template | Frame IDs | Notes |
|---|---|---|
| Home | Desktop 68:3, Mobile 69:333 (page 68:2) | Hero message + Hero search, category tiles with real counts, «آبادین چطور کار می‌کند», RFQ entry block (only when RFQ is on, approved 4-step model), sellers + trust note, seller CTA. Data-dependent sections (popular, lowest prices, price changes) omitted until real data. |
| Search Results | Desktop 64:3202, Mobile 64:3549 (page 64:3200) | Toolbar + filter sidebar + grid + pagination; mobile filter/sort split. Same template serves category/brand PLP with short intro, long text and FAQ (P1-17). |
| Product Page | Desktop 65:2, Mobile 65:4071 (page 64:3201) | Breadcrumb, gallery with heart on the main image, names, key specs, sale unit, Offers Section, technical specs, reviews empty state. |

- **Open items noticed in templates:**
  - Home shows both the header search and the hero search on desktop. Hiding the header search on Home is an optional design choice.
  - The Bottom Nav example highlights «خانه» on non-home pages. Implementation sets the active tab by route.

### Remaining (paused — resume only when the owner asks)
- Product page states: unavailable / no sellers with «موجود شد خبرم کن» (P0-4B), unpriced.
- Category / brand PLP, supplier list and public supplier profile.
- Buyer account: overview, saved products, my reviews, RFQ list and RFQ detail (tabs as approved), account info.
- RFQ create (desktop and mobile pages).
- Seller panel: dashboard, store status screens (pending, needs fixes, cannot be activated, inactive/suspended), products and prices, received RFQs and response page.

## Round 1 exploration (owner decision 2026-09-30)
- **Page:** «Exploration — Round 1» `82:2` (after Product Page). Header doc `82:3`. Labels and 800px fold guides `Labels & fold guides (not design)` (not design).
- **Variables:** type scale, surface hierarchy, radius (only with a structural reason). **Fixed:** IA, Persian copy, product/category data, ordinary imagery, 1280 viewport, PRD behaviour, RTL, Vazirmatn, accessibility, 44px, border/shadow principle, `#0b6264`.
- **Shared ordinary imagery** (local components on the page, holder `82:11`): Photo/Cement sack `82:12`, Rebar bundle `82:19`, PE pipe `82:28`, Wall switch `82:33`, Brick block `82:38`, Tile `82:44`, Faucet `82:49`. Used in every version, baseline included.
- **Shared data:** 6 categories with the template's counts; section «کمترین قیمت‌های مشاهده‌شده» (PRD §11, only with valid data) with 4 products (cement ۲۴۵٬۰۰۰ / کیسه, rebar ۳۲٬۴۰۰ / کیلوگرم, PE pipe ۱۸۶٬۰۰۰ / متر, switch ۸۵٬۰۰۰ / عدد). PDP: cement product, 3 offers (Site priced, Contact priced, Unavailable with no price), range ۲۴۵٬۰۰۰ تا ۲۵۲٬۰۰۰.
- **Home Desktop:** Current `83:2`, A Ledger `85:185`, B Module `86:308`, C Quiet Contrast `87:431`.
- **PDP Desktop slice:** Current `87:5269`, A Ledger `89:1022`, B Module `89:1230`, C Quiet Contrast `89:1440`.
- **A — Ledger:** single white surface, hairlines, teal start-edge rail (hero, section heads, price summary); Display 44 / H2 24 / name 32; categories as a ruled row; data section as a ledger table with column headers and a neutral/50 price rail; radius 6 on images, 0 on sections.
- **B — Module:** alternating bands (neutral/100 and white); everything in bordered modules, radius 4 (structural: modules on a strict grid); 3px teal marker on the hero/price modules and short teal section markers; H1 40 / name 30; card CTA as a module footer link.
- **C — Quiet Contrast:** light page with teal/950 ink anchors (Home: header + hero; PDP: header + price summary = 2); big numerals (card price 28, summary 40); open categories and cards without borders; radius 8.
- **Exploration-only shortcuts:** type sizes are hardcoded (not tokens); colours are bound to existing Primitives. Muted text on neutral/50 uses neutral/600 (neutral/500 is 4.31:1 there). Baseline slices are clones of production templates with the same data and imagery.
- **Noted for review:** the production PDP template's price range text («۲٬۴۵۰٬۰۰۰ تا ۲٬۶۸۰٬۰۰۰») does not match its ۲۴۵٬۰۰۰ price (fixed only in the exploration copy). C on a full page would add a dark footer as a third ink surface, which breaks its own max-2 rule; it needs a decision.
- **Codex review gate:** blocked (no Figma/image access, 60s limit). Review handoff = file key, the node IDs above, scope Home + PDP desktop, 1280×800 viewport, fixed vs varied list.

## Round 2 exploration (owner decision 2026-09-30)
- **Owner feedback on Round 1:** A/B/C read as variations of the same interface. Hypothesis added: "Abadin may need content-specific composition diversity, not merely surface diversity."
- **Reference:** older Sanj Product page (PDF/HTML supplied by owner) used ONLY for visual richness, composition, section rhythm and density. Its behaviour was deliberately not carried over (seller rating in table, «کمترین» badge, stale-price warning, seller counts, buy-from-cheapest CTA).
- **Page:** «Exploration — Round 2» `94:2`. Header doc `94:3`; extra stand-in Photo/Insulation roll `94:10`; labels + 900px fold guides `111:732`. Round 1 untouched.
- **Canvas:** 1440 desktop, content 1232; bands full width where the direction needs it.
- **Shared content:** 8 categories with counts; 6 products in «کمترین قیمت‌های مشاهده‌شده»; RFQ 4-step model; «آبادین چطور کار می‌کند» (3 steps); 3 magazine items; PDP cement with 4 key specs, price summary + range, 4 offers (site priced, contact priced, unpriced, unavailable), 8 specs, about (intro, uses, compatibility note), reviews empty state, 4 related products.
- **D1 Datasheet (برگهٔ فنی):** Home `95:2`, PDP `105:397`, rationale `111:675`. White, no cards, dimension-line motif, numbered sections, sharp geometry, big type; side-index layout for supporting content.
- **D2 Market Hall (بازارچه):** Home `98:5837`, PDP `107:490`, rationale `111:694`. Mint band, floating two-tier header with category row, bento hero with RFQ panel, large-radius stalls/cards, decision price card.
- **D3 Workbench (میز کار):** Home `101:269`, PDP `109:590`, rationale `111:713`. Ink header, two-pane layout with persistent category directory (Home) and sticky decision rail (PDP), dense panels, ink price summary.
- **Needs owner approval if chosen (new UI behaviour):** D2 category row in header, amber RFQ entry; D3 «در این صفحه» anchor navigation, category rail replacing the category grid. D1 adds no behaviour.
- **Exploration shortcuts:** buttons/search/cards hand-built (not DS instances) so geometry could vary; sizes hardcoded; colours bound to existing Primitives.

## Round 3 exploration — Creative Freedom (owner brief 2026-09-30)
- **Page:** «Exploration — Round 3 — Creative Freedom» `112:2`. One direction only; isolated; DS, templates, Round 1 and Round 2 untouched.
- **Concept «نمونه‌خانه» (material library):** categories are material samples, products carry "sample tags", the PDP is a sourcing board. Kufam display type (banna'i/geometric Kufi reference) + Estedad text; palette plaster #EFEAE0, paper #FBF8F2, graphite #1B1A17, lapis #1F3FA8, deep lapis #152C7A, saffron #F2B533, stone #5F5A50 (all used text pairs ≥5.2:1).
- **Frames:** Home `115:2`, PDP `119:1010`, rationale & visual system `123:1592`.
- **Local R3 library (not DS):** swatch frame `113:2` (R3/Swatch/* 113:3, 113:145, 113:191, 113:207, 113:213, 113:238, 113:280, 113:290); product imagery frame `114:2` (R3/Product/* 114:3, 114:13, 114:24, 114:30, 114:35, 114:42, 114:47, 114:54); logo mark `114:61`.
- **PRD behaviour preserved:** not-a-shop; card price «از … / واحد» only; price summary without seller count + observed-price note; offers without ratings/highlighting, relative update time without judgement; §15 actions (direct link only vs contact menu with responsive channels, mobile first); unavailable without price; RFQ item-based routing and unsupported items not sent.
- **Open:** sample data (brands, sellers, prices, phone) is illustrative; Kufam small-size numeral legibility untested; mobile and interaction states not designed.

## Round 4 exploration — Modern Marketplace (owner brief 2026-09-30)
- **Page:** «Exploration — Round 4 — Modern Marketplace» `126:2`. One direction; evolved from Round 2-B; DS, templates and Rounds 1–3 untouched.
- **Fixed by owner:** RTL, Vazirmatn only, brand #0b6264 as anchor, white page with top atmospheric gradient, no general sidebars on Home/PDP, 1440 desktop.
- **Frames:** Home `126:3`, PDP `133:165`, concept & system board `139:270`, Image Sources `138:270`, image drop zone `138:385`.
- **Concept «سازهٔ شناور»:** rounded floating modules over a white page; ambient "joints" (pipe sections, bolt heads, measuring arcs) as parallax edge elements; content-specific compositions (image bento, product cards, deep-teal data modules, blueprint RFQ routing, cross-section anatomy, application diagrams, editorial with floating card, structural-skyline footer).
- **Palette:** teal #0B6264, deep #073F41, mist #E4F0EE, ink #111A19, stone #475553/#62706E, copper #C2703A (shapes) / #9A5526 (text), light copper #F7D2B2 and mint #7FD1C4 on dark, sand #FBF7F2.
- **Imagery:** 16 Unsplash photos chosen (IMG-01…IMG-16, URLs on the Image Sources board). Workspace network policy blocked image hosts and Figma upload, so frames are named slots; owner drops images, then they get placed by name.
- **Needs owner decision:** in-page "مقایسهٔ قیمت فروشندگان" jump; category filter chips on Home product section; per-offer price-position marker; search scope selector.

## Round 4 — Refinement pass (owner brief 2026-09-30)
- **Scope:** refinement of Round 4 only on page `126:2`; no Round 5, no DS migration; DS, templates and Rounds 1–3 untouched.
- **Updated frames:** Home 1440 `126:3`; PDP 1440 `133:165`; search states board `147:253`; reviews empty-state `151:8345`; Home 1280 `151:8360`; PDP 1280 `151:9425`; Mobile Home 375 `152:645`; Mobile PDP 375 `156:696`; concept board `139:270` (updated).
- **Removed:** Home category chips; per-offer price-range markers; search category/scope selector; PDP dark price module, cross-section Anatomy as core section, application diagrams; bolt ambient elements; haze fade, footer window lights, chart draw-in motion.
- **PDP order:** identity + gallery + price context (with jump «مقایسهٔ قیمت فروشندگان ↓») → Supplier offers `149:295` (decision area, equal teal actions, no ranking) → compact price history `149:8530` → Product information `150:303` (description, highlights, note, optional enhanced content, grouped specs) → Applications `151:314` (icon-based) → Reviews `151:350` (sample data; empty state `151:8345`) → related → footer.
- **Home:** hero search primary (no scope); search moves into header after scroll (states board); Products = title column + 3×2 grid; RFQ = value + benefits + CTA first, diagram supporting.
- **Motion (max 2):** ambient edge parallax (4 elements, reduced-motion static); functional micro-motion (header-search transition 200ms, hover elevation, chart tooltip).
- **Radius:** controls 14 · cards/offer rows/menus/header 20 · nested image 14 · media/category tiles 24 · large modules 40 · pills. **Elevation:** L0 flat · L1 card (border) · L2 hover/active · L3 floating (scrolled header, menus, suggestions, mobile bottom nav, sticky price bar).
- **Imagery:** still NOT placed — image hosts and Figma upload blocked; drop zone `138:385` empty. Image/colour balance unvalidated.
- **Needs owner decision:** header-search-on-scroll; mobile sticky price bar; optional enhanced content ownership/conditions; review rating display threshold/moderation.

## Round 4 — Convergence pass (owner decision 2026-09-30)
- **Status:** Round 4 approved as the direction to converge on. No new direction, no DS migration.
- **Header (two-level):** primary floating capsule (radius 20) = logo · wide search (FILL, 52h, surf field + teal 44 button) · «مجله» · «استعلام خرید عمده» (only when RFQ is on) · «ورود / ثبت‌نام». «تماس با ما» stays in the footer to protect search width. Secondary row (not floating, 40h) = «همهٔ دسته‌ها» menu (mist pill) · 7 major categories · برندها · فروشندگان. Home top: search slot empty (hero search primary); after scroll search enters capsule (200ms) and the secondary row hides on scroll-down / returns on scroll-up. Internal pages: search in header from the start.
- **Atmosphere:** warm copper glow on the account side replaced with teal mist (#CDE5E1 @60%) on all R4 frames; copper kept for accents only.
- **PDP top:** 2×2 feature tiles → one compact key-spec strip (4 cells, 20 radius, ~70h); gallery 560×440 (1280: 500×400), thumbs 80/72; short description moved below the price context; Product top 889→703. Jump button bottom at y≈766 (inside a 1280×800 fold).
- **Approved:** header search after scroll; mobile sticky «مقایسهٔ فروشندگان» (chevron-down, no cart semantics).
- **Still open:** optional enhanced content ownership; review threshold/moderation. Real imagery still pending (network block).
- **Frames:** Home `126:3`, PDP `133:165`, Home 1280 `151:8360`, PDP 1280 `151:9425`, states board `147:253`, Mobile Home `152:645` (atmosphere only), Mobile PDP `156:696` (atmosphere + sticky label).

## Round 4 — Header, footer & navigation pass (owner brief 2026-09-30)
- **Desktop header (all R4 desktop frames):** primary floating capsule = A+B brand + dedicated links (logo · divider · «مجله», max 2 links) · C search (FILL, never shrinks for links; empty slot on Home top) · D actions («استعلام خرید عمده» outline only when RFQ is on; guest «ورود / ثبت‌نام» dark / signed-in «حساب من» with default avatar). Secondary layer = full-bleed translucent band with top/bottom hairlines: «همهٔ دسته‌ها» · major categories (data-driven, priority+ overflow into «بیشتر»; 1440 = 7, 1280 = 5 + بیشتر) · برندها · فروشندگان; current category underlined. «تماس با ما» lives in the footer.
- **States:** desktop board `147:253` (moved to x −1640): Home top / Home scrolled (band hides on scroll-down) / internal signed-in RFQ on / internal signed-in RFQ off / focused hero search. Mobile board `167:809` + component `R4/Mobile Search Row` `167:811`.
- **Breadcrumb:** desktop quiet 13px path with chevron-left separators, current item truncates at 320px. Mobile: parent path only (category › subcategory) above the brand chip; back in header.
- **Mobile header:** account removed (lives in bottom nav). Home: menu · centred logo · page-utility slot (search icon after scroll). Discovery pages: header + Search Row. PDP: back · truncated title · Abadin mark; Save (approved P0-4B) moved onto the gallery. PDP now has bottom nav with the sticky «مقایسهٔ فروشندگان» bar stacked above it, plus the mobile footer.
- **Bottom nav:** خانه، دسته‌بندی‌ها، استعلام عمده (only when RFQ is on), ذخیره‌شده‌ها، حساب (guest label «ورود»).
- **Footer (desktop, all frames):** brand + intro + official social slots · groups دسته‌های اصلی (data-driven + همهٔ دسته‌ها) / بازار / راهنما و محتوا / آبادین و پشتیبانی · bottom bar legal (© · قوانین و مقررات · حریم خصوصی · observed-price note) + trust-mark slots. Mobile: 4 accordions, social row, legal links always visible, 2 trust slots, skyline crop 100px.
- **Social & trust marks:** dashed slots only. Official platform icons come from each platform's brand kit; only existing Abadin accounts render. Trust marks render only when genuinely held (PRD FR-G-02: legal badges only at launch).
- **Product card unchanged:** still «مقایسهٔ فروشنده‌ها»; no lowest-price supplier shortcut (separate marketplace decision).

## Round 4 — Navigation completion pass (owner brief 2026-09-30)
- **Boards (left of Home, right-aligned to x −200):** desktop menus `171:877` (mega menu 1440 stage `171:880`, 1280 stage `174:9035`, «بیشتر» 1280 + long-name stress); mobile drawer `173:930`; mobile PDP fixed-bottom-layer `174:962`.
- **Mega menu «همهٔ دسته‌ها»:** click/Enter opens (not hover); panel attached under the secondary band (radius 0/20, L3, scrim 18%). Right column = all parent categories (data-driven, no counts, scrolls inside with fade, «همهٔ دسته‌بندی‌ها» pinned); current page's category active (white row + teal marker). Left = group → leaf links of the active parent + «مشاهدهٔ همهٔ …». Hover intent 150ms; keys ↑↓ / ← into children / → back / Home End / Esc returns focus to trigger. Closes on Esc, outside click, trigger, selection, scroll >120px. Max height = viewport − header − 24. No banners, suppliers or promos.
- **«بیشتر»:** compact 248px menu of only the overflowed selected major categories (never duplicates the row); rows ≥44, 24 line height, long names wrap; right edge aligned to trigger; ↓ opens, Esc/outside closes; one menu open at a time.
- **Mobile drawer:** right edge 320px, scrim, focus trap, close ×/scrim/Esc/swipe. L1 = دسته‌بندی محصولات (→ level) · برندها · فروشندگان · مجله · راهنما group · آبادین group · fixed legal footer. No account or RFQ (bottom nav owns them). Categories = in-drawer levels (L2 parents with «همهٔ دسته‌بندی‌ها», L3 groups/leaves with «مشاهدهٔ همهٔ …»), back in header, active path highlighted.
- **Mobile PDP bottom chrome:** one fixed bottom layer at a time. Bottom nav at arrival, on scroll-up, while Offers are in view and near the footer; the compare bar replaces it only when the price card is out of view, Offers are not in view and the user scrolls down. Max chrome 114px (iPhone) / 80px (667). Jump focuses the offers heading. No fixed layer with keyboard/drawer/sheet open. Long frame `156:696` shows the page-end state (bottom nav only).

## Round 4 — Header & PDP behaviour correction (owner brief 2026-09-30, final before Visual Direction docs)
- **Desktop header = one assembly, two levels:** «Header assembly» (radius 20, white 95%, one L1 shadow, clips) = Level 1 primary row (logo · مجله · search · RFQ · account) + 1px divider + Level 2 row (tinted #F3F7F6, 48h: همهٔ دسته‌ها · categories · بیشتر · برندها · فروشندگان). Applied to all 11 header instances (Home/PDP 1440 & 1280, states board, menu stages). Scrolled Home = Level 1 only. Mega panel and «بیشتر» menu now float 8px below the assembly (radius 20); architecture unchanged.
- **Mobile header:** fixed structure — Abadin logo at the LEFT edge on every page (→ Home); right edge = ☰ (normal pages) or Back (PDP/deep pages); middle empty. No page/product/category titles, no search icon, no account in the header.
- **Mobile Search Row:** page-level config ON/OFF, always visible when ON, no reveal/hide. ON: search results, category, brand, supplier product lists. OFF: Home (hero search), PDP, focused landing pages. Board `167:809`.
- **Mobile PDP bottom:** scroll-direction state machine removed. PDP has no bottom nav; the price + «مقایسهٔ فروشندگان» bar is the single persistent bottom layer (in-page jump to Offers only). Chrome 114px iPhone / 80px 667; content padded; bar hidden only under keyboard/contact sheet. Without a displayable price the bar shows only «مقایسهٔ فروشندگان». Board `174:962`. All other mobile pages keep the standard bottom nav.

## Round 4 — Footer image integration (owner brief 2026-09-30)
- Skyline is now an absolute background layer at the top of the footer (all 4 desktop footers + 2 mobile footers), not a section above it. A vertical tonal fade (#053232, alpha 0 → .72 → .94 → 1) sits over its lower part; footer content starts inside the fade. Ground line faded at both ends. IA, links, social, trust slots and legal unchanged.
- Desktop: skyline full strength in the top ~90px, content from y≈170; footer 782 → 636px. Mobile: 150px crop at full strength top, fade 30–160px; footer 729 → 685px.
- Contrast (worst case: lit mint window behind a heading at ~79% overlay): copper heading ≈6:1, white text ≈8.7:1 — AA.

## DS Migration — Phase A: Foundations (done 2026-09-30, awaiting review)
Decisions: D1 add + remap (existing primitives untouched; Rounds 1–3 not flattened) · D2 warning stays amber, copper uses accent-copper roles · D3 ink-filled guest action becomes a reusable Button variant in Phase B (name after inspecting Button API) · D4 Search/PLP visual migration deferred.
- **Primitives added (22):** teal/850 #073F41, teal/925 #06302F, teal/975 #041E1D; mist/25 #F3F7F6, /50 #EEF6F4, /100 #E4F0EE, /200 #CDE5E1, /300 #C8E0DC; stone/50 #F5F7F6, /100 #ECF0EF, /200 #E4E9E8, /300 #D5DDDB, /500 #62706E, /600 #475553, /950 #111A19; copper/100 #F6E7DA, /200 #F7D2B2, /500 #C2703A, /600 #B8652F, /700 #9A5526; sand/50 #FBF7F2; mint/300 #7FD1C4. Scopes hidden, WEB code syntax var(--family-step).
- **Semantic remaps:** background neutral/50→neutral/0 (white-first); foreground, card-/popover-/secondary-foreground neutral/900→stone/950; muted-foreground neutral/600→stone/600; border neutral/200→stone/200; accent teal/50→mist/100; ring teal/600→teal/700. Unchanged: primary, secondary, muted, border-strong, input, destructive/success/warning, overlay.
- **Semantic added (18):** surface, surface-tint, surface-mist, surface-mist-subtle, surface-sand, surface-inverse, surface-inverse-deep, on-inverse, on-inverse-muted, on-inverse-accent, subtle-foreground, border-subtle, accent-copper, accent-copper-text, accent-copper-muted, data-lowest, data-lowest-inverse, data-average (all aliases, scoped, var(--name)).
- **Radius:** radius/item → radius/xl (12), control 14, card 20, media 24, module 40 (+ existing full). **Spacing:** space/20 80, space/24 96, space/30 120. **Size:** control/xl 56, control/2xl 76.
- **Text styles added (7):** Display/XL Black 60/84, Display/L ExtraBold 44/64, Heading/Section ExtraBold 40/58, Price/Hero Black 40/56, Price/Offer Black 30/42, Eyebrow Bold 13/20, Body/Lead Regular 18/32. Existing 14 styles kept.
- **Effects:** Elevation/L1, L2, L3 (teal-tinted rgb .02/.19/.18); Focus/Halo (4px spread, #0B6264 @25%) + rule: 2px `ring` stroke. Shadow/xs–lg kept, descriptions marked LEGACY.
- **Paint styles:** Atmosphere/Top, Atmosphere/Glow, Atmosphere/Inverse fade.
- **Icons:** Icon/chevron-up 184:8940, Icon/arrow-down 184:8942 (Icon/x already existed as 4:16 — audit corrected).
- **Review board:** Foundations page `2:114`, frame `184:8949` (primitives, semantics, measured contrast table 33 pairs / 0 fails, radius, spacing/size, Persian type specimens, elevation, focus, atmosphere, icons).
- **Expected side effects:** every screen bound to the remapped semantics (production templates, component docs, Round 1 baseline slices cloned from templates) now shows a white page background, R4 ink/stone text and mist accent. No layout or component structure changed.

## DS Migration — Phase B: Base UI (done 2026-09-30, awaiting review)
- **Foundation addition (systemic need from D3):** semantic `neutral-strong` (stone/950), `neutral-strong-hover` (neutral/800), `neutral-strong-foreground` (neutral/0). Also used by Tooltip (was using text/card tokens as fills).
- **Button `5:291`:** radius → radius/control 14; Large height → control/xl 56; focus = ring stroke (token `ring`) + Focus/Halo; new **Variant=Neutral** (7 variants: Medium Default/Hover/Focus/Disabled/Loading, Small, Large) — ink-filled high-emphasis neutral action (e.g. header sign-in); Primary teal unchanged. Fixed pre-existing bug: Loading variants had no Label link (now linked; spinner stays non-swappable).
- **Icon Button `26:337`:** radius/control + focus. No floating variant added (SaveToggle already covers the gallery case; revisit in Phase C/D if Back-over-image needs it).
- **Input `23:210` / Textarea `23:265` / Select `23:307`:** radius/control; focus (and Select Open) = ring 2px + Focus/Halo. Field `23:245` unchanged (no radius). Validation states unchanged.
- **Menu (generic):** new page «Menu» `187:8913`. `Select Menu` renamed **Menu** `23:308` (radius/card 20, Elevation/L3); **Menu Item** `23:286` moved there: radius/item 12, min-height 44 (hug, labels wrap), Selected uses `accent`, new **State=Focus**. Select keeps its own trigger and composes Menu.
- **Badge `26:40`:** radius/full (pill) + **Show dot** boolean (dot uses the tone's text colour). Tones unchanged.
- **Tooltip `26:178`:** bubble radius/item, Elevation/L3, neutral-strong fill.
- **Dialog `26:338`:** radius/media 24, Elevation/L3 (scrim = `overlay`). **Sheet `26:477`:** exposed-edge radius/media, L3, new **Safe area** boolean (34px inset in fixed footer).
- **Breadcrumb `45:193`/`45:159`:** 13px labels; Current truncates at 320 (maxWidth); **Mobile = parent path only** (current item removed).
- **Pagination item, Notice, Empty State:** radius → item/card. **Sign-in card:** radius/media + L3. **OTP:** no radius change needed.
- **Kept (focus alignment only):** Checkbox (box keeps radius/sm 4 by design), Radio, Switch, Chip, Tab, Breadcrumb Item, Pagination Item — all "Focus ring" layers now bound to `ring` + Focus/Halo with host-following radius. Separator, Avatar unchanged.
- **New primitives:** **Accordion Item** `188:27` (page `188:2`; Collapsed/Expanded/Focus; Title, Show divider; 52px header). **Drawer** `188:71` (page `188:29`; Level=Root/Nested; Title, Show footer, Safe area; 320 wide, right edge, radius/media on exposed edge, L3; usage over scrim `188:73`). **Segment** `188:104` + **Segmented Control** `188:117` (page `188:93`; Options=2/3; RTL order).
- **Review board:** page «Review — Phase B Base UI» `190:2`, frame `190:3`.
- **Legacy shadows remaining in base UI:** none. Legacy radius remaining: Checkbox box radius/sm (intentional).

## DS Migration — Phase C: Navigation & Shared Patterns (done 2026-09-30, awaiting review)
- **Migrated in place:** SearchField `31:74` (Header 52 / Hero 76, radius/control, surface fill, teal Submit Icon Button, focus ring+halo) + Suggestions `31:75` (radius/card, L3). Nav Link `47:60` (+State=Open; Active = primary Bold + 3px underline). Account Trigger `47:92` (Guest = Button Neutral «ورود / ثبت‌نام»; SignedIn 44h outline control «حساب من»; SignedInOpen mist + chevron-up). Nav List Item `47:450` (48h, item radius, Active = accent + primary Bold, drill chevron-left). Bottom Nav `47:270` + Item `47:198` (floating 343, radius/card, L3, mist active pill; variants RFQ On/Off × Auth Guest «ورود» / SignedIn «حساب من»). Logo `47:40` → set `194:9461` (Size Default/Compact × Tone Default/Inverse; still placeholder). Footer Link Group `50:23` (+Tone=Inverse; Tone=Default = PRE-R4).
- **Systemic Base UI change:** Drawer `188:71` Content / Footer are now INSTANCE_SWAP slots (placeholders `197:9888`, `197:9890`); Nested Back = new Icon/arrow-right `197:9832`. Drawer stays generic.
- **New:** Categories Trigger `192:9454` · Category Nav Row `194:9664` (Overflow=None/HasMore, priority+ rule) · Header / Desktop `194:9957` (Context HomeTop/HomeScrolled/Internal; «Show RFQ entry»; exposed Account Trigger + Category Nav Row) · Mega Menu `197:321` (+ Parent Item `195:333`, Link `195:340`) · Header / Mobile `197:9862` (Type Default ☰ / Back) · Mobile Search Row `197:9887` (Default/Filled; page-level ON/OFF) · Nav Drawer `197:10878` (Level Root/Categories/Category; content `197:9914`, `197:10100`, `197:10289`, legal footer `197:10381`; no Account/RFQ) · Footer / Desktop `212:10911` · Footer / Mobile `213:1062` (Collapsed/Expanded) · Section Heading `213:11511` (page «Section Heading»; Desktop/Mobile; Show eyebrow, Eyebrow, Title, Show description, Description, Show action) · text style Heading/Section Compact 22/34 ExtraBold.
- **«بیشتر»:** not a new component — Phase B Menu `23:308` at 248w holding only overflowed categories; hidden when Overflow=None.
- **Footer contrast (measured on composited skyline + fade, text removed):** desktop content zone worst bg L 0.070 → white 8.72, muted #C8E0DC 6.29, copper #F7D2B2 6.16; mobile logo over skyline 6.63, intro 8.07. No text above y=200 (desktop) / 80 (mobile crop). Focus on inverse = 2px on-inverse ring (teal ring ≈2:1 fails there). Fade unchanged.
- **Removed from production footer:** R4 exploration placeholders «[شمارهٔ پشتیبانی]» / «[ایمیل پشتیبانی]» (no support contacts until real channels approved); social slots renamed generic (no network names).
- **Legacy:** Site Header `47:181`, Mobile Menu `49:463`, Site Footer `50:83` renamed «LEGACY / PRE-R4 — …» with replacement pointers; still used by templates Home 68:3/69:333, Search 64:3202/64:3549, PDP 65:2/65:4071 and Round 1 baselines.
- **Review board:** page «Review — Phase C Navigation» `213:11517`, frame `213:11518`.
- **P1 closeout (done):** Icon contract — all 50 `Icon/*` are now 24×24 with ONE child vector «Vector» (36 multi-part Lucide icons flattened, geometry verified), stroke 2, round cap/join, bound to `foreground`, Scale constraints. Root cause was multi-layer icons: host colour overrides only matched the first «Vector». Existing swapped instances were re-derived by resetting each icon swap via the property default (298 instances); direct icon instances kept their overrides. Verified 53 swaps (Button Primary/Neutral/Outline, Icon Button, Bottom Nav Item Default/Active, Nav List Item Default/Active/Destructive) — all token-bound, 0 raw. Menu Item has no icon slot. Bottom Nav responsive: items fill equally, top-aligned content, labels wrap only at spaces; ≥360 inset 16 (375 item 67, 360 item 64, single-line, min label gap 4.1px, bar 66); <360 inset 8 (320 item 59, «استعلام / عمده» wraps, bar 78, gap ≥6.8px). 10px labels rejected. Review board sections «P1.1 — Icon swap verification» and «P1.2 — Bottom Nav narrow-width stress» (`221:11294`).
- **Open issues:** P2 — mobile footer: faint seam at the end of the tonal fade (~5 RGB levels). P2 — Focus/Halo on small controls (unchanged).

## DS Migration — Phase D: Abadin Domain Components (done 2026-09-30, awaiting review)
- **Migrated in place:** Price `30:116` (+Size=Card/Offer; new text style Price/Card Black 24/36; Type=Summary LEGACY → Price Context) · AvailabilityBadge `30:85` (dot pill, no icon) · SaveToggle `30:141` (44 target, L1, ring+halo) · ProductCard `33:154` (card radius 20, border-subtle, 8px inset media radius 12, brand in primary, Price Card, CTA «مقایسه فروشنده‌ها» Secondary + arrow) · Category Tile `66:28` (image-led, radius/media, deep-teal scrim, arrow chip; count only with data) · SupplierCard `33:376` (radius 20, mist tags, Outline CTA; no rating/counts/contact/website) · Contact Item `34:52` (56 row, icon chip) · ContactMenu `34:91` (+Surface=Popover/Plain) · Filter/Sort + RFQ token refresh (32 radii bound, Sort Sheet shadow → Elevation/L3).
- **Rebuilt (new, same API):** OfferRow `228:420` (Case Site/Contact/Unpriced/Unavailable/NoAction × Layout; no avatar per P1-24) — old `35:311` LEGACY. Offers Section `230:729` (+ Offer Column Header `230:282`) — old `57:432` LEGACY.
- **New:** Contact Sheet `231:11086` · Price Context `232:136` (State Range/LowestOnly/NoPrice/Unavailable × Layout; Amount/Unit/Range props) · PDP Compare Bar `233:24` (Price WithPrice/NoPrice) · Key-spec Cell `234:2` + Key-spec Strip `234:120` (Count 4/3/2 × Layout) · Price History `235:116` (Layout × Period 30/90).
- **Base UI systemic:** Sheet `26:477` Content is now an INSTANCE_SWAP slot (shared placeholder «Slot / Content placeholder» `197:9888`).
- **Review board:** page «Review — Phase D Domain» `236:698`, frame `236:699`.
- **P1 closeout (done):** Secondary audit — all Button/Secondary uses are the same lower-emphasis secondary action (ProductCard «مقایسه فروشنده‌ها», RFQ «افزودن به فهرست», RFQ «تغییر شهر تحویل», review «نمایش همه», legacy header RFQ entry). Three non-Button consumers used `secondary` as a neutral hover wash (Icon Button Ghost Hover, Chip Toggle Hover, Segment Hover) → rebound to `muted` (same neutral/100 value, no visual change). Then remapped: `secondary` → mist/100, `secondary-hover` → mist/200, `secondary-foreground` → teal/700 (6.11:1 / 5.40:1). Search Results @375 regression found and fixed: Price Size=Compact (`239:2` From, `239:7` Seller) + exposed Price/Compare on ProductCard; template 64:3549 cards use Compact + label-only CTA. Deferred to Search/PLP: unequal card heights in a row.
- **Open / flagged:** Home template tiles are fixed 180×170 → long names climb above the scrim (fix in Phase E by using ≥200×240). Offer order inside the available-priced group remains OPEN. P2: Button Small/Large exist only in State=Default (pre-existing sparse set); focus/hover/disabled for Large follow the Medium rules (ring + halo) but are not drawn.

## DS Migration — Phase E: Production templates (done 2026-09-30, awaiting review)
- **Production templates (built from the Round 4 compositions, local constructions swapped for production components):** Home page `68:2` — Desktop 1440 `243:488`, Desktop 1280 `243:16569`, Mobile 375 `245:2075`. Product Page `64:3201` — Desktop 1440 `247:819`, Desktop 1280 `247:16251`, Mobile 375 `247:18223`. Old templates 68:3, 69:333, 65:2, 65:4071 renamed LEGACY / PRE-R4 (kept for rollback).
- **Component fixes found during migration:** Category Tile — text-anchored scrim (grows with the name) + Size=Large/Small (long names never truncated); Breadcrumb Item Current label now linked to Label; Footer / Mobile bottom reserve 114 (Bottom Nav / Compare Bar + safe area); PDP Compare Bar price block hug height (unit was clipped); Account Menu shadow → Elevation/L3.
- **Template adjustments:** mobile Home category tiles 120 → 160 high; mobile Home hero search uses SearchField Size=Header; design annotations removed.
- **Review board:** page «Review — Phase E Production Templates» `248:18538`, frame `248:18539`.
- **Legacy:** all resolved and deleted in Phase F (see below).

## DS Migration — Phase F: Cleanup & production baseline (done 2026-09-30, awaiting review)
- **Baseline corrections included:** Header / Desktop HomeTop — the empty Search slot fills the space, so Logo + «مجله» stay at the right/start. OfferRow — decorative chevron beside the supplier name removed in all 10 variants; the name still links to the profile; the truck icon is unchanged.
- **Deleted pages:** Exploration Round 1, Round 2 and Round 3 (self-contained; nothing outside them referenced their Photo/* or R3/* components).
- **Deleted templates:** Home 68:3 and 69:333; PDP 65:2 and 65:4071 (the LEGACY / PRE-R4 ones).
- **Deleted components:**
  - LEGACY Offers Section 57:432
  - LEGACY OfferRow 35:311
  - LEGACY Site Header 47:181
  - LEGACY Mobile Menu 49:463 and 49:265
  - LEGACY Site Footer 50:83
  - Footer Link Group Tone=Default variants (the set now has Tone=Inverse only)
  - Price Type=Summary (replaced by Price Context)
- **Deleted styles:**
  - Shadow/xs, sm, md, lg — replaced by Elevation/L1–L3; they were only used on the Foundations specimen.
  - Heading/Display — replaced by Display/XL.
  - Price/Large — replaced by Price/Hero.
- **Variables:** none deleted (142 total). 22 primitive ramp steps are unused (teal, neutral, red, green, amber) but are kept so the ramps stay complete. Size/icon/sm/md/lg are unused but kept because icons are not yet bound to them (P2).
- **Search shell migration (the body is unchanged):**
  - Desktop 64:3202: Header wrap with Header / Desktop Context=Internal plus Footer / Desktop.
  - Mobile 64:3549: Header / Mobile Default, Mobile Search Row Default and Footer / Mobile. The Bottom Nav floats like Home (absolute, inset 16, 46 from the bottom).
- **Page order:**
  1. `00 · Cover / Index`
  2. `01 · Foundations`
  3. `02 · Icons`
  4. `—— 03 · Base UI ——`, then Button … Pagination
  5. `—— 04 · Navigation ——`, then Header, Mobile Nav, Account Nav, Footer
  6. `—— 05 · Domain Components ——`, then SearchField … RFQ Buyer Response
  7. `—— 06 · Patterns ——`
  8. `—— 07 · Templates ——`, then Home, Product Page, Search Results
  9. `—— Review / QA ——`, then Phase B–E boards
  10. `—— Archive ——`, then `Archive — Visual Exploration (Round 4)` (banner `265:531`)
- **Production Index:** `265:2` on the Cover page. Its rows link to each page and show status.
- **Renames and cleanup:**
  - Templates no longer carry «(production)».
  - Foundations frames `2:291` is now «Spacing, Radius» and `184:8949` is now «Foundations — Overview».
  - Stale docs updated: Header, Mobile Nav, Account Nav, Footer, Offers Section, OfferRow, Price, Home, PDP, Search.
  - Stale component descriptions updated (Shadow/* and Round 4 / LEGACY mentions): Tooltip, Dialog, Sheet, Logo, Account Menu, Footer Link Group, Footer / Desktop, Search Suggestions, Price, Price Context, ProductCard, Category Tile, SupplierCard, OfferRow, Key-spec Strip.
  - The OfferRow doc no longer claims a «default lowest price» order; ordering is OPEN.
- **Open findings:**
  - P2 — local texts on Home/PDP (R4 compositions) use raw type values, not text styles.
  - P2 — Footer Link Group keeps a single-option Tone property.
  - P2 — Search mobile Bottom Nav shows «خانه» as active (pre-existing; handled in the Search milestone).

- **Bottom Nav label fix (post-F):** labels shortened to «دسته‌بندی» and «ذخیره‌شده» (were «دسته‌بندی‌ها», «ذخیره‌شده‌ها») in all 4 variants → min label gap at 375 ≈7.5 → ≈12.5px, at 360 ≈9.5px; <360 unchanged («استعلام / عمده» wraps). Option pending owner: «استعلام» alone (gap ≈25px).
- **Footer revision (post-F, owner request):** empty top band removed (desktop content starts at 48, mobile at 24); skyline scaled to cover the whole footer behind content (desktop ×1.69 centred/bottom, mobile cover); tonal fade → full-height readability scrim #053232 (.30/.35 top → .65 → .82 bottom). Worst-case contrast over a lit window: white 6.73, muted 4.86. Footer Link Group titles copper Bold 14 → on-inverse white ExtraBold 17/28; mobile accordion dividers removed, rows 56. Mobile social = own line (label + wrapping icon row); desktop icon row wraps too. Home/PDP 375 bottom bars re-anchored (46 from bottom, constraint MAX). Desktop 508 tall, mobile 714 / 906.
- **Final pre-milestone polish (owner):** Bottom Nav labels locked: خانه · دسته‌بندی · استعلام عمده (NOT «استعلام») · ذخیره‌شده · ورود/حساب من. Verified 4 variants × 343/328/304: min label gap 12.6 (375), 9.6 (360), 12.3–17.8 (320, «استعلام عمده» wraps, bar 78); RFQ Off ≥27. Mobile footer skyline: same asset at 1.8× (was ~4.3× cover), cropped to native x≈335–540, top-anchored, «Image edge blend» dissolves ground edge (y 181–291) into deep-teal base. Measured (geometric, per text): muted 4.87, white ≥7.74, chevrons ≥9.18, focus ring ≥6.75. Home/PDP/Search 375 bottom chrome pinned 46 from bottom (MAX), footer reserve 114.

## Milestone — Search / Category / Brand PLP (done 2026-09-30, awaiting review)
- **Templates (page «Search / Category / Brand» `64:3200`):**
  - Search: Desktop 1440 `285:23156` (filters active), 1280 `286:2927` (no filters, mixed card states), Mobile 375 `286:21992` (filters active).
  - Search states: mobile Filter panel open `286:22922`, Sort sheet open `286:23101`, no results for the query at 1440 `286:23743` and 375 `286:25482`, no results after filters at 1440 `286:24622` and 375 `286:26128`.
  - Stress: 360 `287:28917`, 320 `287:29834`.
  - Category: 1440 `287:6766`, 375 `287:25245`. Brand: 1440 `287:26416`, 375 `287:27394`.
  - The old Search templates were deleted.
- **Shared architecture:** Listing Context → Results Toolbar → Product Grid rows → Pagination. On desktop, the Filter Panel is a 280 column on the right (container 1200, listing column 888, 3 columns). On mobile, «فیلتر» opens a full-screen panel and sort opens a short sheet; the grid has 2 columns.
- **New component:** Listing Context `285:19199` (page «Listing Context»). Variants Type Search/Category/Brand × Layout Desktop/Mobile; props Show description, Show image. Text is overridden per instance.
- **Migrated in place (R4):**
  - Results Toolbar `58:278`: Filters Active/None × Desktop/Mobile; the mobile dot is pinned to the button corner.
  - Filter Group `57:486`: H4 titles, border-subtle dividers, new props Show clear and Show more.
  - Filter Panel `57:656`: mobile adds «انتخاب‌های شما» and a footer with the safe area.
  - Sort Sheet `58:151`.
  - Product Grid `58:981`: Results, NoResults, NoFilterResults, Empty, Loading and Error × Desktop/Mobile; prop Show pagination.
- **Systemic component changes:**
  - ProductCard `33:154` restructured into Top (media + info) and Bottom (price row + CTA) with space-between. Its natural size is unchanged; when stretched, price and CTA align to the bottom. Instance overrides were preserved.
  - Checkbox `23:373` and Radio `23:401`: labels wrap (FILL + HEIGHT), are right-aligned, and the row has a 44px minimum.
  - Price Size=Compact: the unit wraps instead of truncating.
  - PLP atmosphere softened (dark ellipse hidden, the others at 0.5) so the copper eyebrow stays at or above 4.7.
- **Row rhythm:** Figma cannot stretch HUG rows, so templates use rows of ProductCard instances (the detached Product Grid layout) with each row set to the tallest card. In implementation this is a CSS grid with stretch. Home/PDP cards pick up bottom-aligned prices through propagation.
- **Bottom Nav logic:** Search and Brand have no active item; Category → «دسته‌بندی»; Home → «خانه». The description was updated with the locked labels.
- **Review board:** page «Review — Search / Category / Brand PLP» `289:26694`, frame `289:26695`.
- **OPEN decisions:**
  1. The Search filter set when results span several categories.
  2. The price filter in a category with mixed units.
  3. The default sort label for Category/Brand.
  4. Page size.
- **Closeout pass (2026-09-30):**
  - Multi-category Search shows only general filters (price per the unit rule, availability, brand where applicable). Category-specific attributes appear only in a narrowed context where they apply; the backend applicability rule is to be defined in implementation.
  - Price is unit-aware: no merged ranges and no conversion. The price group is hidden in mixed-unit sets (Search 1280, Brand 1440), and chips/helper text carry the unit («… تومان / کیسه»). Further mixed-unit behaviour is OPEN.
  - Default sort: Category/Brand «پیش‌فرض», Search «مرتبط‌ترین».
  - Products per page are configurable; the 9 desktop / 8 mobile cards are illustrative.
  - Availability «موجود/ناموجود» is kept, per PRD §12 and P1-22.
  - Long description and FAQ render only when real content exists.
  - ProductCard regression: Home 1440/1280/375 and PDP 1440/1280 cards are all HUG at natural height with 0 Top→Bottom gap — PASS. PDP 375 has no related-products cards (pre-existing).
  - The 360/320 stress frames are labelled STRESS / QA in their own row; their detached toolbar is labelled QA ONLY.
  - Review-board snapshots refreshed.

## Not done yet
- Final logo/wordmark (the `Logo` component is a placeholder).

## Round 4 — FINAL APPROVED VISUAL DIRECTION (owner approval 2026-09-30)
Status: APPROVED. This section supersedes earlier Round 4 notes where they conflict. Product behaviour still comes from the PRD.

**Visual source of truth:**
- `abadin-visual-direction.md` (canonical copy in the project root, next to `Abadin-PRD.md`).
- Production Design System migration is still pending.
- Existing DS components/templates are not evidence that the older visual treatment remains preferred.

**Core visual direction:**
- RTL-first; Vazirmatn only; light theme.
- `#0B6264` primary brand anchor; white-first surfaces with teal/mist atmosphere; copper is controlled accent.
- Rounded structural geometry and content-specific composition.
- Visual richness is allowed; visual noise that harms hierarchy/task completion is not.
- No general-purpose sidebar on Home or PDP.
- Real photography is intended; final image/color balance still needs validation with real placed photos, but this does not block the approved direction.
- Motion stays limited and purposeful.

**Final desktop header:**
- One coherent rounded two-level header assembly with one elevation treatment.
- Level 1: logo · limited dedicated nav (e.g. مجله) · Search where applicable · RFQ when active · account/auth.
- Divider.
- Level 2 tinted row: همهٔ دسته‌ها · data-driven major categories · بیشتر overflow · برندها · فروشندگان.
- Home top: Hero Search is primary; no duplicate header Search.
- Home scrolled: Level 1 only with Search.
- Internal discovery pages: Search visible from the start.
- Mega menu and «بیشتر» retain the approved navigation-completion behavior.

**Final mobile header/search:**
- Stable header on every page: Abadin logo fixed on LEFT → Home.
- RIGHT = ☰ on normal pages, Back on PDP/deep pages where appropriate.
- Middle remains empty.
- No page/product title, search icon or account in the header.
- Search is a separate full-width page-level Search Row.
- Search Row ON: Search Results, Category, Brand, supplier product listings and similar discovery pages.
- Search Row OFF: Home (Hero Search), PDP, focused Landing Pages.
- When ON, Search is always visible; no reveal/hide interaction.

**Final mobile PDP persistent action:**
- PDP has NO standard Bottom Nav.
- One persistent bottom bar only: displayable «از … تومان / واحد» + «مقایسهٔ فروشندگان».
- The CTA jumps to Supplier Offers on the SAME PDP and moves focus to the Offers heading.
- No price available → show only «مقایسهٔ فروشندگان».
- Hide the bar while the keyboard or contact sheet is open.
- No scroll-direction switching/state machine.

**Product-card marketplace rule:**
- Public discovery Product Card remains «مقایسه فروشنده‌ها».
- No cheapest-supplier shortcut, winner, recommendation or preferred-seller treatment.

**Final footer:**
- Architectural skyline is integrated as the footer background, not a separate image strip.
- Deep-teal tonal fade blends the skyline into the content surface.
- Desktop footer reduced to ~636px in the approved exploration; mobile ~685px.
- Social, legal, trust-mark and navigation IA unchanged.
- Exploration contrast values were estimated; production must measure WCAG contrast against the final background.

**Historical-note rule:**
- Earlier exploration sections remain useful history, but any conflicting header, mobile PDP, footer, color-status or visual-restraint note is superseded by this FINAL APPROVED section.

---

## PLP Content & Filter Closeout (2026-09-30) — reset hierarchy, order and placement SUPERSEDED by "PLP Visual Coherence Refinement" below

**Reset hierarchy**
- Desktop has ONE global «پاک‌کردن همه». It sits in the Results Toolbar beside the Active Filter chips and appears only when a filter is active.
- The sidebar Filter Panel header no longer has a global clear. Each group keeps its own «پاک‌کردن» (visible only when that group has a selection).
- Mobile: the Filter Panel's only global reset is the sticky-footer «پاک‌کردن», next to «اعمال فیلتر».
- Mobile removes single values via the «انتخاب‌های شما» chips. Per-group clears are hidden on mobile.

**Supporting-content order (PRD §13 / P1-17)**
- Order: Grid → Pagination → Long Description (collapsed) → FAQ → Footer.
- A FAQ-first alternative is shown on the review board as a comparison only. It is NOT applied, because it would need Product Owner approval and a PRD update.
- Spacing:
  - Pagination → section spacer: 40 desktop / 24 mobile.
  - Section: border-subtle top line, padding-top 64 / 40, gap between Long Content and FAQ 56 / 40.

**Long Content component** (page «Long-form Content»; set `301:36169`)
- Variants: Collapsed/Expanded × Desktop/Mobile.
- Structure: h2 title, then a content region (INSTANCE_SWAP «Content», rich CMS HTML), then a Ghost toggle «مشاهدهٔ بیشتر» / «مشاهدهٔ کمتر».
- Collapsed height is 360 desktop / 420 mobile, with a fade of 96/80 px: white → page background, aria-hidden, removed when expanded.
- If the content is ≤ collapsed height + 120px, render it in full with no toggle.
- If media (an image or table) would be cut by the boundary, the boundary moves to 24px above that element (presentation-only JS).
- Rich Content sample `301:3` covers h3, paragraphs, lists, inline links, a figure (16:9, width 100%) and a table.
  - Tables use a scroll wrapper with min-width 560.
  - Narrow widths show a scroll shadow and a hint ("Table overflow cue" property).
  - LTR codes use `dir=ltr`.
  - Use words («حداقل») instead of the ≥ sign in RTL text.
- **SEO (mandatory):**
  - The full content must be in the server-rendered HTML.
  - Collapsed = max-height + overflow hidden + fade only; JS only toggles the presentation.
  - No truncation, lazy fetch or injection.
- **A11y:**
  - The toggle is a `<button aria-expanded aria-controls>`, operable with Enter/Space.
  - Visible focus ring; target ≥44px.
  - The fade is never the only cue, because the button label changes too.
  - No focus trap. Links hidden in the collapsed overflow are not focusable.
  - Collapsing returns focus to the toggle.

**Conditional content**
- Category/Brand show Long Content and/or FAQ only when that content exists.
- Four cases are designed: both / FAQ only / LD only / neither (Pagination → Footer).


---

## PLP Visual Coherence Refinement (2026-09-30)

**Audit finding**
- The PLP used the correct components and tokens, but its page composition had fallen back to the pre-Round-4 language.
- It was one flat white surface from header to footer, with:
  - no edge structures (pipe section, measuring arc);
  - no section rhythm (white / mist / deep teal);
  - FAQ and Long Description sitting inside the sidebar grid, leaving an off-centre block and a large empty area.

**Page composition (Category/Brand; Search gets the edge structures only)**
- After Pagination the sidebar grid ends. A full-page "Supporting content zone" follows:
  - **FAQ band:** full-bleed mist (`surface-mist-subtle`, the same surface as the PDP offers band), padding 80/88 desktop, 48/56 mobile.
  - **Long Description:** a white reading zone, padding 80/96 desktop, 48/56 mobile.
  - Both use an **800 centred column** on desktop and full width minus 16px on mobile. Persian text stays RTL/right-aligned.
- Section headings use Section Heading `213:11511` Size=Mobile (compact 22) with an eyebrow: FAQ «پرسش و پاسخ», LD «راهنمای خرید». They stay smaller than the H1.
- Rhythm: white listing → mist FAQ → white LD → deep-teal footer, echoing Home and PDP.
- **Edge structures:** clones of the PDP ambient pipe section and measuring arc.
  - Page level: beside the sidebar top and beside the grid. FAQ band: at its edges.
  - Gutter only; never behind filters or cards.
  - Parallax 0.6×, static under reduced motion, aria-hidden.
  - Hidden at 1280 (the 40px gutter is under the 96px rule) and on mobile (the PDP mobile has none either).
- **Conditional cases:**
  - Neither → Pagination goes straight to the Footer.
  - FAQ only → mist band → Footer.
  - LD only → a border-subtle top line on the LD zone.

**Order**
- Grid → Pagination → FAQ → Long Description → Footer.
- This was the Product Owner's decision in this round. **PRD §13 / P1-17 still reads LD then FAQ and needs a PRD update. The PRD was not edited.**

**Filters**
- **Desktop Filter Panel header:** «فیلترها» at the RTL start (right) and the ONLY global «پاک‌کردن همه» at the end (left).
  - Property «Clear all (any filter active)»; off when no filter is active.
- Per-group «پاک‌کردن» was removed from Filter Group (the "Show clear" property was deleted).
- **Results Toolbar:**
  - No Clear all chip on desktop or mobile.
  - Desktop chips sit on one line (no wrap); Sort stays fixed at 220.
  - New variant Filters=Overflow: runtime fits whole chips, then shows the «N فیلتر دیگر» chip (Toggle chip + chevron-down, aria-expanded; no «+» because it mirrors in RTL).
  - That chip opens the **Active Filters Popover** `308:49204` (new component): the hidden chips, all removable; Esc/outside click closes it; no focus trap.
- **Chip Removable:** max-width 240, label FILL + ellipsis, gap 8. The full value goes in the accessible name.
- **Mobile:**
  - The chip row is one line with horizontal scroll and an edge fade (Overflow variant for many/long filters).
  - The only global reset is the Filter Panel footer «پاک‌کردن».
- **Stress:**
  - 1280 template `310:49488` with the popover open.
  - QA sheet `310:50436`: 1 / several / many / long, at 888, 375 and 320.

**Long Content**
- New «Show title» boolean. It is false in templates, where the Section Heading supplies the title.
- The SEO, a11y and boundary rules from the closeout are unchanged.

**Contrast on mist (measured analytically)**
- Eyebrow 5.17, title 16.1, answer text 7.1 — all AA.

---

## Shared Page Atmosphere + Filter Refinement Surface (2026-09-30) — PLP final correction

**Why the PLP differed**
- The PLP templates used a forked layer, "Atmosphere (top gradient — listing: softened for AA over context text)":
  - the top-right teal-mist ellipse (720×520, 55%) was hidden;
  - the other two ellipses were at layer opacity 50%;
  - at 1280 the frame was resized to 1280 instead of being cropped.
- Mobile PLP carried the same fork.
- The trigger was the Search eyebrow in copper text at 3.98:1 over the dark ellipse.

**Canonical primitive:** «Page Atmosphere / Top (shared)», component `315:19226` on 01 · Foundations, built from the Home reference.
- It is now used (as an instance) on Home 1440/1280/375, PDP 1440/1280/375 and all PLP templates and stress frames. The Home and PDP instances were verified identical to the previous layers, so there is no visual change.
- **Placement:**
  - Desktop (1440 and 1280): (0,0), cropped by the page frame.
  - Mobile: (−500,−200); PDP (−500,−300).
- Never fork, hide a layer, lower opacity or resize it.
- Doc frame: `316:64392` («دستور زبان بصری صفحه»).

**Page-level visual grammar (applies to all future public templates, including Supplier Profile)**
- **A. Standard desktop page top:** white-first page, the shared atmosphere instance, the floating standard Header, about 24px of breathing room, then page-specific context inside that environment.
- **B. Structural edge devices** (pipe section / measuring arc): secondary and optional.
  - Only in gutters of at least 96px; never behind content.
  - Parallax 0.6×, static under reduced motion, aria-hidden.
  - Hidden at 1280 and on mobile. They never replace A.
- **C. Section rhythm:** white / mist / sand / deep-teal footer, only where the content has a real transition.
- **D. Density:** Home most expressive, PDP most structured, PLP quietest. The quietness comes from content composition, never from weakening A.
- **E. Surfaces:** lines for structure; shadow only for genuinely elevated layers (floating header, menus, sheets, popovers).
- **Contrast failures over the atmosphere are fixed locally** (position, text token, local surface), never by weakening the atmosphere.

**Listing Context** (`285:19199`)
- The Search eyebrow is now `primary` teal text plus an 18×4 `accent-copper` bar (the PDP section-eyebrow grammar).
- Measured contrast (worst pixel under each text box, sampled from the rendered atmosphere):

| Text | Contrast |
|---|---|
| Eyebrow, desktop | 4.99 |
| Eyebrow, mobile | 5.95 |
| Title | 12.7 |
| Count | 5.6–6.5 |
| Breadcrumb | 5.46 |
| Description | 6.18 |

- No other compositional change. The P2 "extra listing-header shape" is closed without adding decoration.
- The Category photo slot remains optional; validate it with real photography.

**Filter Panel Desktop** (`57:487` in set `57:656`) — refinement surface
- White `card` fill, 1px `border-subtle` inside, radius 20, padding 16/20/4/20.
- The header has a bottom rule; the last group has no bottom rule. NO shadow.
- **Sticky behaviour:**
  - top = header bottom + 16;
  - max-height = viewport − top − 24;
  - internal scroll with the header row pinned and a bottom fade;
  - identical surface at page start and in the sticky state.
- **QA frames:**
  - before snapshot `316:57652`;
  - sticky mid-grid 1440 `316:60461`;
  - new Category 1280 `316:61586` and Brand 1280 `316:62540`.

**Review board**
- Section 8 `316:64401`: first viewport 1440 and 1280, filter sidebar A–E, full pages at 1440.
- Section 7 snapshots predate this correction.

---

## Composition System Maturity Pass (2026-10-01)

- **New Design System layer:** page «Composition System» `326:2`. Full text is in `claude/composition-system.md`.
- **New Base UI page «Disclosure»** `325:77209`, with the Disclosure set `301:36169`.
  - This is the former «Long Content», renamed and generalised: no title, a centred Outline pill between rules, a "Show fade" property and an exposed toggle label.
  - All PLP instances were renamed «Disclosure (Long Description)».
- **Listing Context** `285:19199`:
  - New variant property **Media** (Image / None); the «Show image» boolean was removed.
  - Search = Open Atmosphere (unchanged).
  - Category / Brand = Identity Layer (card @72%, border-subtle, radius 28/24, no shadow):
    - Category image is edge-aligned (320 wide on desktop; 120 tall on top on mobile).
    - Brand logo sits in a white tile.
    - None = the layer hugs its text (720) at the RTL start.
- **FAQ band (desktop):** a split composition in a 1200 container (1040 at 1280).
  - Heading column (320) at the RTL start, accordion list fills the rest, gap 64.
  - Mobile stays stacked.
- **Long Description:** centred 800 reading column plus Disclosure.
- **QA frames:**
  - Category mobile 360 `348:76292` and 320 `348:77006`;
  - BEFORE snapshots `325:18461` / `325:19554` / `325:20558` / `325:21396`.
- **Review board:** section 9 `348:81009` (before vs after).
