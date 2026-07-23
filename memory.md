# Memory

New entries go at the top. Date format: YYYY-MM-DD.

---

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
