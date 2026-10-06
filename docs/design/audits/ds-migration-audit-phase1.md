# Production Design System Migration — Phase 1: Audit & Migration Plan

Date: 2026-09-30 · File: Abadin — Design System (`Qwx3QpLbhwbouq12QLvAL5`) · Status: **for review — nothing implemented**

Sources checked: `Abadin-PRD.md`, `abadin-visual-direction.md` (root), `abadin-figma-design` skill (updated), `abadin-senior-design-review-SKILL.md`, approved Round 4 frames on page `126:2` (Home `126:3`, PDP `133:165`, 1280 `151:8360`/`151:9425`, Mobile `152:645`/`156:696`, boards `147:253`, `167:809`, `171:877`, `173:930`, `174:962`).
Method: read the actual variables, text/effect styles and every production component set (variant properties, size, radius, effect style, token bindings). No node was changed.

Legend — **KEEP** compatible · **UPDATE** valid structure, needs Round 4 migration · **REBUILD** cannot safely carry approved behaviour/direction · **DEPRECATE** superseded/duplicate · **MISSING** required reusable pattern does not exist.
Scope — **F** foundational · **UI** shared UI · **D** Abadin domain. Risk = effect on existing screens (templates `68:2`, `64:3200`, `64:3201`, exploration pages).

---

## 0. Key findings (summary)

1. **Structure is healthy; visuals are pre-R4.** Components are well tokenised (radius, padding, fills bound to variables) and follow shadcn-style APIs. Most base UI can be migrated by changing tokens, not rebuilding.
2. **Foundations are the main gap.** No copper/sand/mint/deep-teal/footer-ink colours, no inverse/tint/atmosphere semantics, radius scale tops at 16 (R4 needs 12/14/20/24/40), type scale tops at 36 (R4 uses 40–60 display and 30+ price numerals), shadows are neutral-black not teal-tinted, `background` is grey (`neutral/50`) while R4 is white-first.
3. **Navigation is where rebuilds concentrate.** Site Header, Mobile Menu, Site Footer and the mobile header cannot express the approved two-level header, drawer levels, stable mobile logo, Search Row or skyline footer. Mega menu, «بیشتر», category row, Search Row, PDP compare bar and Accordion do not exist.
4. **Domain components keep their PRD-correct behaviour.** ProductCard, OfferRow, Price, ContactMenu etc. encode the right rules (P1-8, §15, C-01, P1-21/22/24). Only OfferRow/Offers Section need structural rework to match the R4 decision area.
5. **Cross-page risk:** Rounds 1–3 exploration frames are bound to production primitives; retuning primitives will silently alter them. Needs an owner decision (see §7).

---

## 1. Foundations

| Item | Current | Class | Reason | Required migration | Deps | Scope | Risk |
|---|---|---|---|---|---|---|---|
| Brand primitive | `teal/700 = #0b6264` | KEEP | Correct anchor | — | — | F | — |
| Teal ramp | teal/50–950 | UPDATE | R4 deep teal `#073F41` and mist `#E4F0EE` not in ramp (`teal/900 #0b4143`, `teal/50 #edf7f6` are close but not equal) | Add `teal/850 = #073F41`, `mist/100 = #E4F0EE`, `mist/50 = #EEF6F4`, `tint = #F3F7F6`; keep existing steps | — | F | Low (additive) |
| Neutral ramp | `neutral/900 #1a2221`, `600 #55625f`, `500 #6b7876`, `200 #dfe5e4` | UPDATE | R4 ink `#111A19`, stone `#475553`/`#62706E`, line `#E4E9E8`, surface `#F5F7F6` | Either retune steps 900/600/500/200/50 to R4 values **or** add R4 steps and remap semantics (see decision D1). Re-measure contrast | D1 | F | **High** if retuned (every screen + Rounds 1–3 shift) |
| Copper family | none | MISSING | Copper accent `#C2703A`, text `#9A5526`, soft `#F6E7DA`, light-on-dark `#F7D2B2` | Add `copper/*` primitives | — | F | None |
| Sand, mint, footer ink | none | MISSING | Sand `#FBF7F2` (reviews band), mint `#7FD1C4` (data on dark), footer `#06302F`→`#041E1D`, fade `#053232` | Add primitives | — | F | None |
| Semantic colour | 28 shadcn-style tokens | UPDATE | Missing R4 roles; `background → neutral/50` contradicts white-first | Set `background → neutral/0`; add `surface` (#F5F7F6), `surface-tint` (#F3F7F6, header L2), `surface-mist`, `surface-inverse` (deep teal modules/footer), `on-inverse`, `on-inverse-muted` (#C8E0DC), `accent-copper`, `accent-copper-text`, `accent-copper-muted`, `border-subtle`, `data/lowest` (mint/teal), `data/average` (#B8652F), `scrim` | D1, D2 | F | Medium (background change lightens every template — intended) |
| Atmosphere gradient | none (hand-built per frame) | MISSING | Top teal→mist→white glow is part of the direction | Paint style `Atmosphere/Top` (+ mobile crop); ambient edge elements as local assets, not components | colour | F | None |
| Typography | 14 styles, max Display 36 ExtraBold, Price/Large 28 | UPDATE | R4 uses Display 60 Black, section 40–44 ExtraBold, price 30 Black (offers), 44+ price context, eyebrow 13 Bold, body 15–18 at 1.7–1.75 | Add `Display/XL 60`, `Display/L 44`, `Heading/Section 40`, `Price/Hero`, `Price/Offer 30`, `Eyebrow 13`, `Body/Lead 18`; keep existing names for compatibility; verify line heights for Persian | — | F | Low (additive); Medium if existing sizes are retuned |
| Spacing | 0–64 (13 steps) | UPDATE | Section paddings 80/96/120 and gutters 40/80 used by R4 layout | Add `space/20 = 80`, `space/24 = 96`, `space/30 = 120` | — | F | None |
| Size | control sm36/md44/lg52, icon 16/20/24 | UPDATE | R4: header search 52, hero search 76, primary CTA 54–60, mobile targets ≥44 | Add `control/xl = 56`, `search/hero = 76`; keep 44 minimum | — | F | None |
| Radius | none/4/6/8/12/16/full | UPDATE | Approved hierarchy: controls 14 · items 12 · cards/rows/menus/header 20 · nested image 14 · media/tiles 24 · modules 40 · pills | Add semantic radius tokens `radius/control 14`, `radius/item 12`, `radius/card 20`, `radius/media 24`, `radius/module 40`; rebind components from `radius/lg` etc. | — | F | **Medium–High**: every rebind reshapes existing templates (intended) |
| Border / Divider | `border`, `border-strong`, Separator | KEEP (+UPDATE values) | Principle unchanged; values follow neutral decision | Map `border → #E4E9E8`; add `border-subtle` for level divider | D1 | F | Low |
| Elevation / Shadow | `Shadow/xs,sm,md,lg` neutral black | UPDATE | R4 uses teal-tinted shadows (rgb .02/.19/.18) and levels L0–L3; floating header, menus, bottom nav, compare bar | Create `Elevation/L1` (card hover/price context), `L2` (hover/active), `L3` (floating: header, menus, drawers, compare bar); keep old styles as aliases then DEPRECATE `Shadow/xs` | — | F | Low |
| Focus | Button: separate "Focus ring" rectangle (r12); Input: 2px teal stroke | UPDATE | R4 spec: 2px `#0B6264` + 3–4px 25% halo, radius follows host | Define `Focus/Ring` effect style + rule; align Button/Input/menus/rows | radius | F/UI | Low |
| Icons | 47 Lucide icons, `Icon/<name>` contract | KEEP | Contract fine | MISSING: `chevron-up` (currently rotated), `arrow-down` (correction in Phase A: `Icon/x` already exists as `4:16`); social icons are **not** Lucide — official brand-kit slots only | — | F | None |

---

## 2. Base UI

| Component (ID) | Class | Reason | Required migration | Deps | Scope | Risk |
|---|---|---|---|---|---|---|
| Button `5:291` (6 variants × 3 sizes × 5 states) | UPDATE | API good; radius 8, focus rectangle, no dark/ink style used for guest auth; Large 52 < R4 CTA 54–60 | Rebind radius → control 14; Large → 56; focus → Focus/Ring; decide dark auth style (D3) | radius, focus | UI | Medium |
| Icon Button `26:337` | UPDATE | Radius/focus only | Rebind radius; add "Floating" variant (white + L2, used for gallery Save/back) or reuse SaveToggle | radius | UI | Low |
| Input `23:210` / Field `23:245` / Textarea `23:265` | UPDATE | Structure valid | Radius 14, focus ring, surface fill option | radius, focus | UI | Low |
| Select `23:307` + Menu Item `23:286` + Select Menu `23:308` | UPDATE | Menu parts are generic enough to power «بیشتر», Account Menu and sort | Promote to generic **Menu / Menu Item** (radius 20/12, L3, rows ≥44, wrap long labels); Select composes it | radius, elevation | UI | Low |
| Checkbox `23:373` / Radio `23:401` / Switch `23:432` | KEEP | Correct states, 44 targets | Focus ring alignment only | focus | UI | Low |
| Tabs `26:142`/`26:143` | KEEP | Used in RFQ; counts only private | — | — | UI | — |
| Segmented control | MISSING | Price-history 30/90-day toggle | Small component on Menu/Tab tokens | radius | UI | None |
| Badge `26:40` | UPDATE | Radius 4 → pill; R4 availability uses pill + dot | Radius full; add dot option; tones unchanged | radius | UI | Low |
| Chip `26:115` | KEEP | Already pill, used by filters | — | — | UI | — |
| Tooltip `26:178` | UPDATE | Bubble r6 | Radius 12, ink fill, L3 | radius | UI | Low |
| Dialog `26:338` | UPDATE | r16, Shadow/lg | Radius 24, Elevation L3, scrim token | radius, elev | UI | Low |
| Sheet `26:477` | UPDATE | Top radius, fixed footer (P1-16) OK | Top radius 24, safe-area padding in footer, L3 | radius, elev | UI | Low |
| Drawer (side) | MISSING as primitive | Only exists inside Mobile Menu | Build `Drawer` primitive (right edge 320, header/back/close, scroll body, fixed footer, safe area, focus trap) | Sheet, Accordion | UI | None |
| Accordion | MISSING | Needed by mobile footer groups, PDP mobile spec groups, drawer | Generic `Accordion Item` (Collapsed/Expanded/Focus, 52 row) | icons | UI | None |
| Pagination `45:215`/`45:267` | UPDATE | Radius only | Radius 12 | radius | UI | Low |
| Breadcrumb `45:159`/`45:193` | UPDATE | Desktop OK (chevron-left, RTL). Mobile variant = collapsed middle + truncated current; approved mobile rule = **parent path only**, current omitted | Update Mobile variant; desktop quiet 13px; current truncates at 320 | type | UI | Low |
| Separator `44:138` | KEEP | — | — | — | UI | — |
| Notice `26:230` / Empty State `26:248` / Skeleton `26:238` | UPDATE | Radius 12 → card/module rules | Rebind radius | radius | UI | Low |
| Avatar `30:56` | KEEP | FR-G-07 default avatar | — | — | UI | — |
| OTP `58:2885` / Sign-in `59:294` | KEEP (+token refresh) | Behaviour correct | Radius/elevation via tokens only | tokens | UI | Low |

---

## 3. Navigation & shared patterns

| Component (ID) | Class | Reason | Required migration | Deps | Scope | Risk |
|---|---|---|---|---|---|---|
| Site Header `47:181` (Desktop/Mobile, Show RFQ) | **REBUILD** | Flat 1280×121 bar with bottom border; cannot express one rounded two-level assembly, Home-top empty search slot, scrolled state, category row overflow, signed-in/guest, RFQ on/off | New `Header / Desktop` assembly: Level 1 (logo · max 2 dedicated links · search slot · actions) + divider + Level 2 (tint). Variants: Context = HomeTop / HomeScrolled / Internal; RFQ On/Off; Auth Guest/SignedIn. Keep "RFQ only when on" rule (§19.9) | Logo, Nav Link, SearchField, Button, Account Trigger, Category Nav Row, elevation | Nav | High (all templates) |
| Secondary navigation (category row) | MISSING | Data-driven categories + priority+ overflow + active underline; never depends on 7 items | `Category Nav Row` with slots: «همهٔ دسته‌ها» trigger, category links (repeatable), «بیشتر», برندها, فروشندگان | Nav Link, Menu | Nav | None |
| Nav Link `47:60` | UPDATE | Needs active underline (3px teal), 48 target, trigger-open state | Add `Active` underline + `Open` state | tokens | Nav | Low |
| Account Trigger `47:92` | UPDATE | R4 guest = dark button, signed-in = outline + default avatar + chevron | Rebuild visuals on Button/Avatar; keep 3 statuses | Button, Avatar | Nav | Low |
| Mega menu «همهٔ دسته‌ها» | MISSING | Approved: parent column + groups/leaves, no counts/promos, keyboard contract | `Mega Menu` (panel r20, L3, 8px below header; parent row states Default/Hover/Active/Focus; group; leaf; «مشاهدهٔ همهٔ …»; scroll fade) | Menu tokens, Focus, elevation | Nav | None |
| «بیشتر» overflow | MISSING | Compact menu of overflowed categories only | Instance of generic **Menu** (248 wide) — no new component | Menu | Nav | None |
| Mobile header (Site Header Mobile variant) | **REBUILD** | Current mobile header ≠ approved: logo fixed left, ☰ or Back right, empty middle, no title/search/account | `Header / Mobile` variants: Type = Default(☰) / Back | Logo, Icon Button | Nav | Medium |
| Mobile Search Row | MISSING in production (exists as exploration comp `R4/Mobile Search Row 167:811`) | Page-level ON/OFF, always visible | Promote to production on SearchField tokens; Query property; clear slot | SearchField | Nav | None |
| Mobile Menu `49:463` (Guest/SignedIn, Show RFQ) | **REBUILD** | Approved drawer excludes Account and RFQ (owned by bottom nav) and uses in-drawer category levels; current variants encode the opposite | Rebuild as `Nav Drawer` on Drawer primitive: Level 1 / Categories / Category children; active path; fixed legal footer | Drawer, Nav List Item | Nav | Medium |
| Nav List Item `47:450` | KEEP (+UPDATE radius 12) | Good shared row; reused by drawer | Radius, focus | radius | Nav | Low |
| Bottom Nav `47:270` / Item `47:198` | UPDATE | Behaviour correct (RFQ On 5 / Off 4). Visual: full-width bar + border → R4 floating 343 r20 L3 with mist active pill; guest label «ورود»; documented exclusion on PDP | Restyle; add Auth Guest/SignedIn (label/avatar); note "hidden on PDP" in description | elevation, Avatar | Nav | Medium |
| Site Footer `50:83` | **REBUILD** | Flat footer; no skyline background layer, tonal fade, social slots, trust-mark slots, legal bar | `Footer / Desktop` & `/ Mobile`: skyline background layer + fade token, brand column, link groups, social slots (render only existing accounts), trust-mark slots (only marks held — BIZ-02), legal bar. Skyline as local asset component | Footer Link Group, Accordion, colour (inverse, copper-light) | Nav | High (all templates) |
| Footer Link Group `50:23` | UPDATE | Column/Collapsed/Expanded OK; mobile should use Accordion; data-driven groups | Mobile layouts via Accordion; on-inverse tokens | Accordion | Nav | Low |
| Account Nav `48:636` / Account Menu `48:637` / Workspace Switch `54:437` | UPDATE (tokens only) | Behaviour correct (P0-4, FR-G-04A); not redesigned in R4 | Radius/elevation/menu tokens; no structural change | Menu | Nav | Low |
| Logo `47:40` | KEEP (placeholder) | Final wordmark is a separate brand decision | Align mark used in R4 (teal square + ring) with placeholder | — | Nav | — |
| Section heading (eyebrow · title · description · optional action) | MISSING | Repeated across every R4 section | Small pattern component | type | Shared | None |

---

## 4. Abadin domain components

| Component (ID) | Class | Reason | Required migration | Deps | Scope | Risk |
|---|---|---|---|---|---|---|
| SearchField `31:74` (Header/Hero × states) + Suggestions `31:75` | UPDATE | API correct (no scope selector — matches R4). Visual: r8, 44/52; R4 header 52 surf field + teal square button; hero 76, 2px teal border, text submit | Resize sizes, radius 14, submit styles; Suggestions r20 L3 | radius, size, elevation | D | Medium |
| Price `30:116` (From/Seller/Summary/Unpriced/Unavailable) | UPDATE | Rules correct (P1-8, P1-12, P1-21). Needs R4 numeral styles; Summary superseded by Price Context | Apply Price text styles; keep From/Seller/Unpriced/Unavailable; DEPRECATE `Summary` after Price Context exists | type | D | Medium |
| Price Context (PDP: from-price, range, observed note, jump to offers) | MISSING | Approved PDP pattern | New domain component; jump is in-page only | Price, Button | D | None |
| PDP persistent comparison bar (mobile) | MISSING | Approved single persistent bottom layer; price optional | `Compare Bar` (WithPrice / NoPrice), safe-area, L3, 48 CTA with chevron-down; never Buy semantics | Price, Button, elevation | D | None |
| Key-spec strip (PDP) | MISSING | Compact 4-cell strip / mobile 2×2 | Data-driven cells (label, value, unit) | type | D | None |
| AvailabilityBadge `30:85` | UPDATE | Two states only (P1-22) ✓; visual → pill + dot | Build on updated Badge | Badge | D | Low |
| SaveToggle `30:141` | KEEP (+elevation token) | P1-11A heart on image ✓ | Shadow/xs → Elevation L2 | elevation | D | Low |
| ProductCard `33:154` (Search/Supplier × Priced/Unpriced/Unavailable) | UPDATE | Behaviour correct (no seller count, «مقایسه فروشنده‌ها», supplier context own price). Visual: r12, image full-bleed 198 | Radius 20, inset media r14, R4 price style, hover L2; keep all variants and CTA | radius, type, elevation, Price | D | Medium |
| SupplierCard `33:376` | UPDATE | P1-19 correct | Radius 20, border only | radius | D | Low |
| Category Tile `66:28` | UPDATE | R4 uses image-led tiles r24 (bento); count optional (P1-13) | Radius 24, image treatment; keep Show count | radius | D | Low |
| OfferRow `35:311` (Case × Layout) | **REBUILD (keep API)** | Behaviour correct (§15, C-01, P1-24, unavailable no price). Structure is a flat table row; R4 decision area = separate rounded rows (r20, ~108h), price 30 Black with «به‌روزرسانی قیمت» below, equal teal actions, unavailable hatched + outline, no markers, contact menu anchor | Rebuild visual structure; keep `Case` = Site/Contact/Unpriced/Unavailable/NoAction and `Layout` Desktop/Mobile; no winner/highlight | Price, Button, Badge, ContactMenu | D | High (PDP) |
| Offers Section `57:432` | **REBUILD** | Needs mist band, 44 title, column header row, row stack, footer note; in-group order stays OPEN | Rebuild pattern on new OfferRow + Offer Column Header (MISSING) | OfferRow | D | High (PDP) |
| ContactMenu `34:91` / Contact Item `34:52` | UPDATE | Rules correct (mobile first, ≤3 messengers, opens even with one channel) | Menu tokens (r20, L3); mobile = Sheet | Menu, Sheet | D | Low |
| Price History module | MISSING | Compact, secondary, only with valid data, LTR time axis, text summary | Data-viz module + Segmented control; no invented data | Segmented, data tokens | D | None |
| Filter Group `57:486` / Filter Panel `57:656` / Sort Sheet `58:151` / Results Toolbar `58:278` / Product Grid `58:981` | UPDATE (tokens) — **visual migration deferred** | Behaviour correct (P1-14/15/16). No approved R4 Search/PLP template yet; sidebar allowed on PLP | Token refresh only now; full visual migration after R4 Search/PLP template is designed and reviewed | tokens | D | Low now |
| RFQ components (`38:270`…`41:325`) | UPDATE (tokens only) | Not in R4 scope; behaviour correct | Token refresh; no structural change | tokens | D | Low |
| Reviews summary / review card | MISSING (not in audit list; noted) | R4 PDP has rating summary + cards (PRD §14.4, §17) | Later domain batch; display threshold remains an open product question | type | D | None |

---

## 5. DEPRECATE list

| Item | Replaced by | When |
|---|---|---|
| Site Header (both variants) `47:181` | Header / Desktop + Header / Mobile | After templates are swapped |
| Mobile Menu `49:463` | Nav Drawer | After templates are swapped |
| Site Footer `50:83` | Footer / Desktop + Mobile | After templates are swapped |
| Price `Type=Summary` | Price Context | After PDP migration |
| `Shadow/xs,sm,md,lg` | Elevation L1–L3 (aliases during transition) | After all rebinding |
| `radius/sm 4`, `radius/md 6` | kept only if still used by checkbox/tiny marks; otherwise removed | Final cleanup |
| Button "Focus ring" rectangle | Focus/Ring effect | Base UI phase |

Exploration-only components (Round 3 `R3/*`, Round 4 local frames) are **not** promoted except `R4/Mobile Search Row`, which becomes the production Search Row.

---

## 6. Migration sequence (minimises rework)

**Phase A — Foundations (single batch, then review)**
1. Colour primitives: add teal/850, mist, tint, copper, sand, mint, footer ink (additive).
2. Resolve D1 (neutral retune vs add), then semantic tokens: background white, surface/tint/inverse/on-inverse, copper accents, border-subtle, scrim, data colours. Measure all text pairs (WCAG AA).
3. Radius semantic tokens; spacing and size additions.
4. Type styles additions (display, section, price, eyebrow, lead).
5. Elevation L1–L3 teal-tinted + Focus/Ring; Atmosphere paint style; missing icons (x, chevron-up, arrow-down).
→ Gate: review Foundations page + contrast table.

**Phase B — Base UI** (token rebinds first, then new primitives)
Button, Icon Button, Input/Field/Textarea, generic Menu (from Select parts), Select, Badge, Tooltip, Dialog, Sheet, Breadcrumb (mobile rule), Pagination, Notice/Empty/Skeleton → then new: Accordion, Drawer, Segmented control.
→ Gate: review Base UI.

**Phase C — Navigation & shared patterns**
SearchField + Suggestions → Mobile Search Row → Nav Link / Account Trigger → Category Nav Row → Header / Desktop (all variants) → «بیشتر» (Menu instance) → Mega Menu → Header / Mobile → Nav Drawer (3 levels) → Bottom Nav → Footer Link Group → Footer / Desktop + Mobile → Section heading.
→ Gate: review against boards `147:253`, `167:809`, `171:877`, `173:930`.

**Phase D — Domain components**
Price → AvailabilityBadge → SaveToggle → ProductCard → Category Tile → SupplierCard → Offer Column Header + OfferRow (rebuild, same API) → Offers Section → ContactMenu → Price Context → Compare Bar → Key-spec strip → Price History module → token refresh for Filter/Sort/RFQ.
→ Gate: domain review.

**Phase E — Regression validation**
Rebuild Home and PDP templates (desktop 1440/1280, mobile 375) from migrated components; compare to approved R4 frames; measure contrast on real backgrounds (incl. footer fade); swap instances in Search Results template (tokens only); then DEPRECATE old nav/footer components. Real-photo validation remains a separate pending task.

---

## 7. Decisions needed before Phase A

- **D1 — Neutral ramp:** retune existing neutral steps to R4 values (cleaner, but changes Rounds 1–3 exploration frames that are bound to primitives) **or** add new steps and remap semantics only (safer for history). Recommendation: add + remap; optionally flatten/detach Rounds 1–3 first.
- **D2 — Warning vs copper:** keep `warning` = amber for system warnings and use copper only as brand accent (R4 "important note" = copper-muted), or merge. Recommendation: keep them separate.
- **D3 — Dark guest auth button:** R4 uses an ink-filled «ورود / ثبت‌نام». Add a Button variant (e.g. `Inverse`) or use Primary teal. Needs owner choice; affects Button API.
- **D4 — Search/PLP visuals:** confirm Filter/Sort visual migration waits for an R4 Search/PLP template (recommended) rather than being guessed now.

Not blocking: real imagery validation; reviews display threshold (open product question); final logo.
