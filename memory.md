# Memory

New entries go at the top. Date format: YYYY-MM-DD.

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
