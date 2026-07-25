# Memory

New entries go at the top. Date format: YYYY-MM-DD.

---

## 2026-07-25 - Family Farm: all eight of Jad's points built, awaiting review

- Built locally and verified at 1280 / 1536x730 / 375, **not committed**: terrace copy
  and render, garden pool section, premium cabin spec, Signature Suites, two-phase site
  plan toggle, three partnership routes, floating brandmark in place of the nav bar,
  tabbed closing gallery, feasibility section, and a nine-point 360 explorer. See
  `HANDOFF.md` for the point-by-point state.
- **The feasibility numbers go public** - William's call, 2026-07-25. The landowner's
  name does not: the one-pager names him five times, the page says "the owners". Page
  carries `robots: noindex, nofollow`. Worth repeating to him: a Rebrandly password does
  not protect the canonical Vercel URL, which stays open to anyone with the link.
- **Where the email and the one-pager disagree, the email wins for the partnership
  routes and the one-pager for the economics.** The two-structure comparison table is
  deliberately left off the page so three route cards and two structures cannot
  contradict each other in the same scroll.
- 360s are **self-hosted, not embedded**: Insta360 blocks iframes by CSP and its media
  URLs are signed with about six days of life. Nine equirects at 3840x1920 total 6.9 MB,
  rendered by vendored Pannellum, each loading only when its pin is clicked. Its own
  zoom and fullscreen chrome is switched off rather than restyled, and wheel-zoom is off
  so the viewer cannot trap the page scroll.
- Set each panorama's opening yaw from the degree ruler in `_tmp-renders/360/`, never by
  eye - two of nine were over 90 degrees out on the first pass.
- The `.rooftop` class is now `.terrace` throughout, CSS and JS. The filename
  `assets/rooftop-view.jpg` is deliberately unchanged; a filename is not copy.
- Gallery selection: `catalogue.md` index N in the sibling photos folder is the Nth file
  alphabetically. Verified against eight known pairs, so the mapping is reliable.
- `phase 2.png` inverts Jad's brief (it dims Phase 1 rather than showing the whole
  estate sharp). Kept as a focus-shift pair because the two drawings are pixel-aligned;
  both images are due to be redrawn.

## 2026-07-25 - Family Farm: Jad revision round, 7 renders approved and staged

- Working from Jad's email "Family Farmhouse - Revisions" (Fri 2026-07-24, Gmail
  thread `19f93040b655e26b`, 8 points, no attachments) plus the 2026-07-22 Meet
  transcript (Drive `1i_K1zMnkc_HyJXvRPZXXT1GP4CbyOxCkp0CLoW78yBU`). See
  `HANDOFF.md` for the full state of this round.
- The "rooftop" is really a covered first-floor terrace. All 16 "rooftop"
  occurrences become "the terrace" and "under the stars" is dropped - the space is
  roofed and the phrase cannot survive. Evening dining stays, per Jad.
- Seven renders approved and staged in `_tmp-renders/`, not yet committed: terrace
  v9, cabin exterior v3, cabin interior v3, suite hall, suite majlis, suite
  bedrooms A v2 and B v2. Garden pool has two candidates, neither approved.
- Renderer: Gemini `gemini-3.1-flash-image` at 2K 16:9, driven from the real estate
  photos. Scripts kept beside the outputs in `_tmp-renders/`.
- **Prompting trap worth remembering:** "preserve the camera angle, horizon and
  framing" contradicts any request to change depth or spatial layout, because depth
  *is* camera position. Three attempts silently kept the camera. Fixed by generating
  fresh and using the old image for mood only.
- The 74 estate photos are not in this repo - they sit duplicated in the two
  sibling `proposal-family-farm-al-hudaiba*` folders, and
  `catalogue.md` there groups them by area. There are no 360 panoramas in the set,
  so Jad's request for 360s in the closing gallery needs new assets.
- **`Family_Farmhouse_Feasibility_OnePager`** (Drive
  `1pNJprDexez_pJiDK7BxespUugt_7qA3UNRKWQpIZf6w`, Jad, edited 2026-07-25) is marked
  Private & Confidential and carries the owner's name, AED 5.77M capex, a five-year
  P&L and the JV waterfall. William wants it reflected at the end of the page;
  everything under a slug folder is public, so this needs an explicit decision on
  what may be shown. It also contradicts the email on the partnership routes (two
  structures vs three) and lists the Majlis as a shared lounge and bar rather than a
  suite living hall. Both unresolved.

## 2026-07-25 - Family Farm: rooftop parallax + pinned gallery overflow fixed

- The rooftop ("Upstairs, the day ends slowly") parallax had been dead: its
  ScrollTriggers were created before the pinned mansion gallery, so they measured
  the page without that pin's 4,061 px spacer and ran their whole scrub 4,061 px
  too early. Measured drift matched the pin distance exactly. Fixed with
  `refreshPriority: 1` on both pinned triggers. `ScrollTrigger.refresh()` never
  helped because refresh *order* was the fault.
- Any tween added before a pin has the same latent bug. New pinned triggers get
  `refreshPriority: 1` from the start.
- `.zoomable img` carried a 0.8 s hover transition that also applied under the
  rooftop scrub, easing toward each per-frame transform and smearing the drift.
  Now `transition: none` for that one image.
- The mansion gallery ran 872 px tall in a 730 px window while pinned, hiding the
  bottom 142 px. Cause was the fixed `58dvh` slide cap ignoring a heading block
  that is 281 px on the mansion and 191 px on the day track. Section is now
  `height: 100dvh` with the track on `flex: 1 1 auto; min-height: 0`, slides sized
  from leftover height via `aspect-ratio` and capped at `max-width: 58vw`.
- Only bit screens under roughly 880 px tall, which is why it survived review on a
  tall monitor. Check 1536x730 - it is the size that catches this class of bug.
- `errors.md` corrected: local preview failures were never `http.server` dropping
  connections. Proposals set `<base href="/<slug>/">`, so you must serve from
  `proposals/` and open `/<slug>/`, or every asset 404s and the motion libraries
  silently never load.

## 2026-07-23 - Orphan asset sweep + parent CLAUDE.md now points here

- Deleted 4 tracked-but-unreferenced assets (~17 MB): the superseded 16 MB hero encode `concept-family-arrival-expat-v2-kling-6s.mp4`, `site-plan.jpg` (replaced by `site-plan-final.jpg`), and `dome-terrace.jpg` + `dome-wide.jpg` (left over from the dome gallery removed in the Jad round).
- Cause: the cache-bust rename rule in `errors.md` never said to delete the old file. Rule updated with an orphan-check one-liner - run it after any rename or section removal.
- `14_Proposals/CLAUDE.md` previously described only the older `proposal-claude-<slug>/` Vercel-CLI system and never mentioned this repo. It now leads with the two-system split and points here for new work.
- Bulk-migrating the old `proposal-claude-*` folders into this repo is blocked on confidentiality: purchase-offer and title PDFs plus `.env.local` files sit loose beside `index.html`, and only 5 of 14 folders have a `.vercelignore`. Any migration must copy `index.html` + `assets/` only, per folder.

## 2026-07-23 - Family Farm: William edit round (fonts, Barn, map, galleries, videos)

- Satoshi fonts now preloaded + a `size-adjust` Segoe fallback (`"Satoshi Fallback"`) so the hero never blows up if the font race is lost.
- "Little Palms" renamed to "The Barn" everywhere user-visible; anchor id stays `#little-palms` so shared links keep working.
- Wynn pin at exact casino coordinates from Jad: `25.6879, 55.7555`. Route polyline still traced to the old destination - last stretch draws straight to the pin (offer re-fetch if it bothers anyone).
- Opening statement says "UAE residents" (was "families").
- Mansion gallery now uses the same shell-based scroller pattern as the day track, slides locked to the photos' native 16:9 (`aspect-ratio` + width capped to `58dvh * 1.7778`) so nothing crops on small laptops.
- Dome section: two real pool angles stacked (`.dome-stack`) matching the concept render height; plan hotspots + info card deleted; site plan is `assets/site-plan-final.jpg` (595 KB) in an exact 3:2 box.
- Estate statement section is now a sand-light band with hairline top border - closes the white-on-white dead gap after the map.
- Video replacements ship under NEW filenames (egg-collecting v3, hero arrival v3-hero); hero source compressed 37 MB -> 4.6 MB (ffmpeg CRF 26, faststart, audio stripped). Heavy originals go to `_tmp-renders/`.

## 2026-07-23 - Family Farm: Jad feedback round shipped

- Deployed commit `8d2d990` addressing Jad's nine feedback points plus the verbal treehouse note.
- New Location section: vendored Leaflet (`assets/vendor/leaflet-1.9.4.*`) with red farm-to-airport and blue farm-to-Wynn driving routes; route geometry is stored locally in `assets/route-data.js` (fetched once from OSRM at build time - no routing API at page load). Farm pin: 25.6236 N, 55.9122 E. Distances: airport 8.9 km / ~10 min, Wynn Al Marjan 24 km / ~30 min, Dubai ~1 hr.
- Dome repositioned as evening dining pavilion (pool moves outdoors); pool-gallery section removed; 4:00 pm day card now shows the outdoor pool concept.
- New Clientele section (family staycations + parents' evening at Wynn while children are in supervised care - no gambling language, per house rules).
- All 7 activity cards are photo cards; tree climbing includes the timber treehouse per Jad's inspiration references.
- 15 AI concept renders live in `assets/concepts/concept-*.jpg`, all labelled "Concept imagery". Renderer of record: Gemini `gemini-3.1-flash-lite-image` (thinking high, 3:2, ~1K) via `GEMINI_API_KEY`; the dome render is Higgsfield GPT Image 2 (2K). Real photos keep "The estate today" labels.
- Site plan renamed and compressed: `IMG_3838.PNG` (3.9 MB) -> `assets/site-plan.jpg` (650 KB).
- `_tmp-renders/` at repo root is the gitignored staging area for renders awaiting approval.

## 2026-07-23 - Motion libraries moved local

- The live Family Farm proposal was not initializing Lenis, GSAP, or ScrollTrigger because its runtime CDN dependencies were unavailable in the presentation browser.
- Pinned copies of GSAP 3.13.0, ScrollTrigger 3.13.0, Lenis 1.3.25, and the Lenis stylesheet now live under `proposals/family-farm-al-hudaiba/assets/vendor/`.
- Core presentation motion must use local versioned files rather than runtime CDN dependencies.
- Browser verification confirmed Lenis initialized, GSAP applied animation styles, and vertical scrolling advanced the pinned Mansion gallery horizontally.

---

## 2026-07-22 - Shared proposal repository established

- Created the shared architecture based on the live Namou brochure repository pattern.
- Repository: `NamouProperties/proposals-namou`.
- Proposal folders live at `proposals/<slug>/`.
- Vercel project: `proposal-namou` under `namou-workspace`.
- Vercel root directory: `proposals`.
- Canonical URL pattern: `https://proposal-namou.vercel.app/<slug>/`.
- Added the first proposal at `proposals/family-farm-al-hudaiba/`.
- The existing standalone project and URL remain untouched because the presentation was already being shared.
- Future proposal publishing should use this repository and slug pattern rather than creating one Vercel project per proposal.
