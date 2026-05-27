# AGENTS.md — Ireland Weekend Trip Plans

> **RULE:** When you receive new instructions from the user, FIRST update this file before doing anything else. Append the new instruction to `## session log` at the bottom in **compaction format** — the structured sections: Goal, Constraints & Preferences, Progress, Key Decisions, Next Steps. Also keep the `## session log` entries compact and factual. This is the project's memory.

## Group
- user + wife + baby (3mo) + 2 friends = 5 pax
- max 1.5hr drives between stops (dublin departure excluded)
- weekend: sat 30 – sun 31 may

## Output rules
- single sharable .html (no local files, no api keys)
- photos via pexels cdn `images.pexels.com/photos/{id}/...`
- maps via google `maps?q=...&output=embed` (no api key) — NOTE: `maps?q=` only shows pins; use `saddr`/`daddr` for route lines
- clickable images → lightbox, tabbed by plan
- accommodations: sleep 5, under €200/night, real bookable direct links only
- galway is waypoint only — no galway itinerary stops
- **ONLY plans north of the Dublin-Galway line** — no plans in southern Ireland (below lat ~53.3°N)
- **NO Northern Ireland/UK** — all stops must be in Republic of Ireland

## Current 3 plans (all north of Dublin-Galway line, all ROI)

| # | plan | region | accommodation | sleep | €/night |
|---|------|--------|---------------|-------|---------|
| 1 | Connemara & Mayo | west | apt 263 clifden (loveconnemaracottages.com) | 5 | ~100 |
| 2 | Sligo & Donegal | northwest | mountain view grange beg (selfcater.com) / kit's cottage | 5 | ~145 |
| 3 | Achill Island & North Mayo | west/north | sound cottage, achill island (selfcater.com) | 6 | ~52 |

## Research sources
- tripadvisor.ie top tours
- viator — same routes top-ranked
- getyourguide — similar top itineraries
- selfcater.com — verified available properties
- pexels.com — cdn images

## Rejected / replaced
- athlone / midlands → replaced
- boyne valley / meath → replaced
- carlingford & louth → user didn't like
- wicklow & kilkenny → user didn't like (south of Dublin line)
- cashel & cork → user didn't like (south of Dublin line)
- causeway coast & antrim → user can't go to Northern Ireland

## Pexels image IDs per plan

### Plan 1 — Connemara & Mayo
- 15424415 (cong), 18549116 (kylemore), 21923111 (connemara), 30283523 (clifden harbour), 5568718 (doolough), 33856353 (killary), 9772544 (keem bay), 15934810 (westport)

### Plan 2 — Sligo & Donegal
- 6974660 (strandhill), 17938479 (benbulben), 28774067 (sligo coast), 34443645 (sligo town), 1649273 (donegal coast), 15934813 (slieve league)

### Plan 3 — Achill Island & North Mayo
- 29579005 (achill coast), 9772544 (keem bay), 29361156 (achill island), 5765122 (achill cliffs), 35036863 (achill beach), 13050819 (keem bay), 1686024 (downpatrick head), 12530564 (downpatrick), 10428434 (ceide fields), 1204996 (mayo coast)

## Known concerns / map fixes
- google maps `maps?q=...&output=embed` does NOT show route lines — use `saddr`/`daddr` format instead
- carlingford map needed `+Louth` to disambiguate from blackrock (dublin)
- galway removed as itinerary stop (per user)
- all maps use `saddr=...&daddr=...to:...&output=embed` format for route lines

## Session log

### 2026-05-27 — Session 1
- Created project directory C:\Users\ph002\Documents\personal\
- Built 5-plan trip-plan.html
- Replaced athlone/midlands with wicklow/kilkenny
- Replaced boyne valley/meath with causeway coast
- Fixed map embeds (switched to `maps?q=...&output=embed`)
- Replaced causeway coast with cashel/cork (user can't go to NI)
- Fixed all maps back to `saddr/daddr` format for route lines

### 2026-05-27 — Session 3
- **Goal:** Always update AGENTS.md first with new instructions, using compaction format (Goal, Constraints & Preferences, Progress, Key Decisions, Next Steps sections)
- **Progress:** Updated the AGENTS.md rule to specify compaction format for session log entries
- **Key Decisions:** All future instructions will be logged in compaction format before any work begins

### 2026-05-27 — Session 4
- **Goal:** Remove all rate/price mentions from within the 3 plan tab sections in trip-plan.html
- **Progress:** Removed prices from accommodation stops and accommodation info boxes in all 3 plans.
- **Key Decisions:** Rates removed from plan tab detail sections.

### 2026-05-27 — Session 5
- **Goal:** Add animated hero slideshow, full-screen vertical swipeable carousel, scroll-snap, mobile-friendly landing page feel
- **Progress:** Replaced gradient hero with 3-image crossfade slideshow. Replaced overview grid with full-viewport vertical carousel with scroll-snap. Added bounce arrow and plan count.
- **Key Decisions:** `scroll-snap-type: y proximity` on body so carousel cards snap smoothly. Hero and tab sections don't snap. Footer changed to "Created with love by Prashanth".

### 2026-05-27 — Session 2
- User didn't like: carlingford/louth, wicklow/kilkenny, cashel/cork
- **Decision:** Only 3 plans total, all north of Dublin-Galway line
- **Decision:** Added Achill Island & North Mayo as Plan 3
- Created AGENTS.md as project memory (planning.md archived)
- Pexels researched: achill coast (29579005), keem bay (9772544, 13050819), achill island (29361156), achill cliffs (5765122), achill beach (35036863), downpatrick head (1686024, 12530564), ceide fields (10428434), mayo coast (1204996)
- Accommodation found: Sound Cottage, Achill Island — sleeps 6, 3 beds, from €52/night
- Rewrote trip-plan.html: removed 3 plans, added Achill plan, 420 lines total

### 2026-05-27 — Session 6
- **Goal:** Fix Node.js 20 deprecation warning in GitHub Actions deploy
- **Progress:** Upgraded `actions/checkout@v4`→`v6`, `actions/configure-pages@v5`→`v6`, `actions/upload-pages-artifact@v3`→`v5`, `actions/deploy-pages@v4`→`v5`. These versions target Node 24 natively, eliminating the need for `FORCE_JAVASCRIPT_ACTIONS_TO_NODE24` env var (removed).
- **Key Decisions:** Use latest action versions with native Node 24 support; drop workaround env var.

### 2026-05-27 — Session 7
- **Goal:** Fix labels, dots, and down arrow hidden behind Safari address bar on mobile
- **Progress:** Changed `.hero` `height:100vh`→`100dvh`, `.carousel-card` `min-height:100vh`→`100dvh`. Dropped unreliable `env(safe-area-inset-bottom)` in favor of generous fixed `bottom` values (`4rem` dots, `2.5rem` place, `9.5rem` arrow desktop, `8.5rem/4.5rem` mobile). Added `viewport-fit=cover` meta tag.
- **Key Decisions:** Ditch `env()` for generous fixed rems — more reliable across iOS versions, content is flexbox-centered so there's room.

### 2026-05-27 — Session 8
- **Goal:** Fix plan title/subtitle hidden behind sticky tabs when switching plans; add up arrows for scrolling back up through carousel
- **Progress:** Added `scroll-margin-top:3.5rem` to `.container` so plan content clears the sticky tab bar on scroll. Added `.carousel-arrow-up` buttons to each carousel card: card 0 scrolls to hero, cards 1-2 scroll to previous card. Added upward float animation to up arrows. Dropped `env(safe-area-inset-bottom)` for fixed rem values (`top:4rem` desktop, `top:3.5rem` mobile) to clear notch.
- **Key Decisions:** Up arrows get upward float animation matching down arrows. Fixed top values for notch clearance.

### 2026-05-27 — Session 9
- **Goal:** Enable left/right image navigation in lightbox via swipe, arrow buttons, and keyboard
- **Progress:** Added `<` `>` nav buttons, swipe detection (50px threshold), counter "N / M", and ←/→ keyboard nav. Added `touch-action:none` to lightbox overlay to prevent page scroll-through. Lightbox images deduplicated into gallery array for circular navigation.
- **Key Decisions:** Touch swipe uses `{passive:true}` with `touch-action:none` CSS — no `preventDefault()` needed. Gallery dedupes identical image URLs.
