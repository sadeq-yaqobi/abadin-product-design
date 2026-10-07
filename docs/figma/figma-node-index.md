# Figma node index

File: **Abadin — Design System** — https://www.figma.com/design/Qwx3QpLbhwbouq12QLvAL5 (Sadeq's team)

Figma is the source of truth for design output. This index only points to nodes; it is compiled from the records in this repository. If a node here disagrees with Figma, Figma wins and this file must be updated.

Link pattern: `https://www.figma.com/design/Qwx3QpLbhwbouq12QLvAL5/?node-id=<id with ":" replaced by "-">`

## Templates (production)

| Page | Node | Frames |
|---|---|---|
| Home | `68:2` | 1440 `243:488` · 1280 `243:16569` · 375 `245:2075` |
| Product Page | `64:3201` | 1440 `247:819` · 1280 `247:16251` · 375 `247:18223` |
| Search / Category / Brand | `64:3200` | Search 1440 `285:23156` · 1280 `286:2927` · 375 `286:21992`; Category 1440 `287:6766` · 1280 `316:61586` · 375 `287:25245`; Brand 1440 `287:26416` · 1280 `316:62540` · 375 `287:27394` |
| Supplier Profile | `373:3` | 1440 `375:134` · 375 `375:91298` · validation 1280 `375:1722` · 360 `375:92511` · 320 `375:93108`; doc `433:5533` |
| Brand Listing | `450:3` | 1440 `452:2` · 375 `453:91537`; states `454:1278`; category states `460:1678`; validation `455:1504`; doc `456:1630` |
| Supplier Listing | `467:2` | 1440 `467:3` · 375 `467:93947`; desktop states `468:1560`; mobile states `470:2028`; validation `471:2496`; doc `472:2977` |
| Supplier Registration | `484:2` | Seller Guide 1440 `484:3` · 375 `492:98636`; Step 1 1440 `488:645` · 375 `489:1192`; Steps 2–4 + Review desktop `490:1301` · mobile `492:97699`; auth `493:15`; status desktop `494:15` · mobile `494:100821`; validation `496:15`; targeted 1280/360/320 `496:101428`; doc `499:103888` |
| Buyer Account | `510:571` | Overview 1440 `511:2` · 375 hub `512:2`; Saved Products `513:106159` · `513:106553`; My Reviews `515:3894` · `515:4191`; RFQ List `516:4769` · `516:5108`; RFQ Detail `518:5780` · `519:116143`; Account Information `524:14865` · `524:15114`; RFQ Detail interaction desktop `519:112897` · mobile `522:12941`; change mobile `526:15713`; states desktop `528:15963` · mobile & toasts `529:16345`; responsive 1280/360/320 `529:121862`; doc `531:25718` |

## State and QA frames

| Area | Nodes |
|---|---|
| Search states | filter panel `286:22922`, sort sheet `286:23101`, no results 1440/375 `286:23743`/`286:25482`, no filter results 1440/375 `286:24622`/`286:26128`, stress 360/320 `287:28917`/`287:29834`, popover 1280 `310:49488`, filter QA `310:50436` |
| Category identity QA | 360 `348:76292`, 320 `348:77006`; conditional content `302:36730`, `302:37709`, `302:38687`, `302:39665`, `302:40643` |
| Brand identity QA | `445:95982` |
| Supplier Profile states | `376:3191`, `376:3344`, `376:3492`, `376:93057`, `376:93656`, `377:4868`, `377:4931`, `431:5041`, `431:5298`, `432:5576`; components used `433:5510`; decisions `433:5523` |

## Components (selected)

| Component | Node | Page |
|---|---|---|
| Button | `5:291` | Button |
| Input / Field | `23:210` / `23:245` | Input & Field |
| Select | `23:307` | Select |
| Menu / Menu Item | `23:308` / `23:286` | Menu `187:8913` |
| Radio | `23:401` | Radio |
| Chip | `26:115` | Chip |
| Notice / Skeleton / Empty State | `26:230` / `26:238` / `26:248` | — |
| Dialog / Sheet | `26:338` / `26:477` | — |
| Breadcrumb / Pagination | `45:193` / `45:267` | — |
| Avatar | `30:56` | Avatar |
| Disclosure | `301:36169` | Disclosure `325:77209` |
| Nav Link | `47:60` (Active `47:50`) | Header |
| Header / Desktop · Header / Mobile | `194:9957` · `197:9862` | Header |
| Mobile Search Row | `197:9887` | SearchField |
| Bottom Nav | `47:270` | Mobile Nav |
| Footer / Desktop · Footer / Mobile | `212:10911` · `213:1062` | Footer |
| Page Atmosphere / Top (shared) | `315:19226` | 01 · Foundations |
| SearchField / Suggestions | `31:74` / `31:75` | SearchField |
| Price · Price Context | `30:116` · `232:136` | — |
| ProductCard | `33:154` | ProductCard |
| SupplierCard | `33:376` | SupplierCard `30:8` |
| City Picker | `466:191` | City Picker `466:2` |
| OfferRow · Offers Section | `228:420` · `230:729` | — |
| ContactMenu · Contact Sheet | `34:91` · `231:11086` | — |
| PDP Compare Bar | `233:24` | PDP Compare Bar |
| Category Tile | `66:28` | Category Tile `66:2` |
| Brand Tile · Brand Logo Placeholder | `450:49` · `454:92315` | Brand Tile `450:2` |
| Listing Context | `285:19199` | Listing Context `285:44` |
| Supplier Identity | `375:133` | Supplier Identity `373:2` |
| Section Heading | `213:11511` | Section Heading `213:11479` |
| Filter Group · Filter Panel · Sort Sheet · Results Toolbar · Product Grid | `57:486` · `57:656` · `58:151` · `58:278` · `58:981` | Filter & Sort / Product Grid |
| Active Filters Popover | `308:49204` | Filter & Sort |
| Form Section Header · Checklist Item · Contact Channel Input · Weekly Hours Row | `481:95693` · `481:95706` · `482:52` · `482:77` | Supplier Onboarding `481:95668` |
| Image Upload (Logo Upload `482:144` deprecated) | `502:225` | Supplier Onboarding `481:95668` |
| Registration Status Card | `483:199` | Supplier Onboarding `481:95668` |
| Toast | `512:105799` | Notice |
| Segmented Control · Workspace Switch · Sign-in Card | `188:117` · `54:437` · `59:294` | — |

RFQ components are listed in [`docs/design/design-system-notes.md`](../design/design-system-notes.md) (Stage 3, Stage 5). Changed in Buyer Account (milestone 11): RFQ Summary Row `41:1094`, RFQ Comparison Line `40:1037`, RFQ Item Comparison `40:1038`, RFQ Supplier Response Card `41:325`; Contact Sheet `231:11086` (fills width).

## System pages

| Page | Node |
|---|---|
| Cover / Production Index | `0:1` / `265:2` |
| Foundations | `2:114` |
| Composition System | `326:2` |
| Review — Phase B / C / D / E | `190:2` / `213:11517` / `236:698` / `248:18538` |
| Review — Search / Category / Brand PLP | `289:26694` (left untouched per Owner) |
| Archive — Visual Exploration (Round 4) | `126:2` |
