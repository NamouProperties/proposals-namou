# Memory

New entries go at the top. Date format: YYYY-MM-DD.

---

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
