# Handoff — Family Farmhouse

Updated 2026-08-03 (evening). Read with `memory.md` (dated decisions), `errors.md`
(known failures) and `context.md` (publishing contract).

Live page: `https://proposal-namou.vercel.app/family-farm-al-hudaiba/`
Postcard version: `https://proposal-namou.vercel.app/postcard-hotels/` — a
personalized, unlisted copy for The Postcard Hotel carrying their commercial
terms. Built 2026-08-03 from Jad's 4:04pm email; see the 2026-08-03 memory entry
for what differs. Never link it from anywhere public.

**State: family-farm live and current as of commit `d5a279e`.** Jad's 2026-07-24
revision round and his 2026-07-25 image round are both shipped. The wellness/spa
recreation from the Saturday VN was cancelled by Jad ("stop for now") after
Postcard liked the family-boutique concept.

**Uncommitted right now:** edits to `report/family-farm-al-hudaiba-phase-1-feasibility.html`
and an untracked PDF export beside it. Read the warning about `report/` before you
commit either. Do NOT sweep them into the postcard-hotels commit.

---

## Where things live

| What | Where |
| --- | --- |
| The public page | `proposals/family-farm-al-hudaiba/index.html`, one self-contained file, inline CSS and JS |
| Page assets | `assets/` — `concepts/` (AI renders), `gallery/` (real photos), `panoramas/` (360s), `vendor/` (GSAP, ScrollTrigger, Lenis, Leaflet, Pannellum) |
| The feasibility document | `report/family-farm-al-hudaiba-phase-1-feasibility.html`, a standalone 3-page A4 doc. **Not** part of the website and not linked from it |
| Staging, gitignored | `_tmp-renders/` — renders awaiting approval, heavy originals, and the 360 scripts |

The Vercel root directory is `proposals`, so anything outside it is never deployed.

---

## Toolchain — what this page is built with

- **Concept renders: Gemini.** Renderer of record is **`gemini-3.1-flash-image`** — this
  is "Nano Banana 2" — thinking high, 2K, 16:9, via `GEMINI_API_KEY` from the Windows
  user environment. The first round used `gemini-3.1-flash-lite-image` at ~1K 3:2;
  everything since is the flash model above, so keep using it and the set stays
  consistent. Reuse a script in `_tmp-renders/` as the pattern.
- **No video generation happens on this page.** The two clips it does carry (hero
  arrival, egg collecting) were made earlier with Kling and are already committed. If a
  new clip is ever needed, the house rules live in the Namou project memory
  (`feedback_higgsfield_models.md`): default **Kling 3.0 at 1080p**, escalate only to
  **Seedance 2.0 Fast**, never full Seedance 2.0. Use the Higgsfield MCP, not the CLI.
- **360 panoramas: Pannellum**, vendored in `assets/vendor/`. Scripts in
  `_tmp-renders/360/`.
- **Compression:** ffmpeg for video (CRF 23-26, `+faststart`, `-an`, roughly 5 MB),
  Pillow for stills. Renders land at 2048 px wide, gallery photos at 1600 px.
- **Deploy:** push to `main` and Vercel deploys itself.

---

## Sources of truth

1. **Jad's email, "Family Farmhouse — Revisions", Fri 2026-07-24 07:25**, Gmail thread
   `19f93040b655e26b`. Eight numbered points. Shipped.
2. **Jad's email of 2026-07-25**, Gmail thread `19f99baceb2df761` — four annotated
   screenshots. The Gmail connector returns the body but **not** the attachments, so the
   screenshots have to be read another way. Three of the four are shipped.
3. **Google Meet transcript, "family farm", Wed 2026-07-22**, Drive id
   `1i_K1zMnkc_HyJXvRPZXXT1GP4CbyOxCkp0CLoW78yBU`. Pool dimensions (10 m x 5 m), cabin
   count and siting.
4. **`Family_Farmhouse_Feasibility_OnePager`**, Drive id
   `1pNJprDexez_pJiDK7BxespUugt_7qA3UNRKWQpIZf6w`. Source of the feasibility document.
5. **360 photo links**, Drive doc id `1grZNfuQPFD0iEVHG39st6GFFpGCVAKyfsUxuZv3oQHI` —
   ten Insta360 share links with William's area labels.

---

## Still to do

1. **Make the repo private** — William approved pushing regardless (2026-08-04, Jad's
   deadline morning) and will flip visibility himself. The Postcard page deployed
   2026-08-04 with Jad's final corrections (Al Hamraniyah, 395k core + 600k expansion,
   one- to two-bedroom cabins); `properties.namou.ae/postcard-hotels` resolves and is
   confirmed live.
2. **Jad's fourth screenshot point** — a bare block wall that should look painted and
   renovated. Not done: the source image was never identified.
3. **360 pin positions** — William reviewed them 2026-08-03: fine as they are. Pin 10
   (second majlis) on the Postcard page was placed by inference next to pin 2; nudge
   only if William flags it.
4. **Phase 2 site plan redraw** — the current `site-plan-phase-2.jpg` inverts Jad's
   request: it dims Phase 1 and sharpens only the horses and spa, instead of showing the
   whole estate undimmed. It works as a focus-shift pair because both drawings are
   pixel-aligned, and Jad should be told that is what he is looking at. Both plans may
   change slightly.

---

## Warnings

### `report/` is committed to a PUBLIC GitHub repository

`NamouProperties/proposals-namou` is public. `report/` sits outside the Vercel root, so
it never deploys — but "not deployed" is not "not public". The feasibility document is
readable right now at
`raw.githubusercontent.com/NamouProperties/proposals-namou/main/report/...`, and it
carries the Private & Confidential mark, the AED 5.77M Phase 1 investment, the five-year
P&L and the fifty-year musataha. It does not carry the landowner's name.

Deleting the file later does not undo this — it stays in the git history. Decide with
William before adding the PDF or committing further changes. The clean options are to
make the repo private, keep the report out of git entirely (move it under
`_tmp-renders/` or another gitignored path), or accept it deliberately.

### The public page and the one-pager disagree on partnership routes

Jad's email asks for three routes (invest only, invest and operate, operate only). The
one-pager describes two structures. The page follows the email for the routes and the
one-pager for the economics, and deliberately omits the two-structure comparison so the
two cannot contradict each other. Jad has not confirmed which is current.

### The one-pager treats the Majlis as a shared lounge

It lists "Majlis lounge & bar" as a facility, while the suite renders treat a hall as a
suite's private living room. The estate has more than one hall, so both can be true, but
Jad should confirm.

### Never on the page

The landowner's name, AdMind as the target partner, the AED 2M renovation figure Jad
quoted verbally, Jad's own equity intentions, and CBRE.

---

## Working notes

- **Local preview:** serve from `proposals/`, not the slug folder, and open
  `/family-farm-al-hudaiba/`. Each page sets `<base href="/<slug>/">`.
- **Bust the cache when verifying** (`?v=2`): a plain reload serves the old `index.html`,
  so you end up testing edits that never reached the browser.
- **Verify at 1536x730** as well as 1280 and 375. That viewport catches the
  pinned-section overflow class of bug.
- **Prompting trap:** never combine "preserve the camera angle, horizon and framing" with
  a request to change depth or spatial layout. Depth is camera position; the model will
  keep the camera. Generate fresh and use the old image for mood only.
- **Changed asset = new filename AND delete the old one in the same commit**, then run
  the orphan check in `errors.md`.
- **Confirm a deploy** by polling the public URL with Python `urllib`. PowerShell will
  not follow Vercel's 308 and the Vercel MCP 403s on this team.
- The 74 estate photos are not in this repo. They sit in
  `../proposal-family-farm-al-hudaiba-v2/photos/`, and `catalogue.md` beside them groups
  them by area. **Index N in that catalogue is the Nth file alphabetically.**
