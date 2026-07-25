# Handoff — Family Farmhouse revision round

Updated 2026-07-25. Covers Jad's email of Friday 2026-07-24 and William's additions.
Read with `memory.md` (decisions), `errors.md` (known failures) and `context.md`
(publishing contract).

Live page: `https://proposal-namou.vercel.app/family-farm-al-hudaiba/`

**State: all eight of Jad's points are built locally and verified. Nothing is
committed or pushed yet — it is waiting on William's review.**

---

## Sources of truth

1. **Jad's email, "Family Farmhouse — Revisions", Fri 2026-07-24 07:25**, Gmail
   thread `19f93040b655e26b`. Eight numbered points. The authoritative brief.
2. **Google Meet transcript, "family farm", Wed 2026-07-22**, Drive id
   `1i_K1zMnkc_HyJXvRPZXXT1GP4CbyOxCkp0CLoW78yBU`. Carries the pool dimensions
   (10 m x 5 m), cabin count and siting, and what to delete from the plan.
3. **`Family_Farmhouse_Feasibility_OnePager`**, Drive id
   `1pNJprDexez_pJiDK7BxespUugt_7qA3UNRKWQpIZf6w`, owned by Jad. Source of the
   feasibility section. William approved publishing the numbers on 2026-07-25.
4. **360 photo links**, Drive doc id
   `1grZNfuQPFD0iEVHG39st6GFFpGCVAKyfsUxuZv3oQHI` — ten Insta360 share links with
   William's area labels.

---

## Built this round, not yet committed

| Jad's point | What shipped |
|---|---|
| 1 Terrace, not rooftop | `concept-terrace-evening.jpg` replaces the rooftop render; every "rooftop" in copy is now "the terrace"; "under the stars" is gone, evening dining kept. The CSS/JS class is `.terrace`, not `.rooftop`. |
| 2 Garden pool | New `#pool` section between the Dome and the terrace. 10 m x 5 m, sunbeds all round. **`concept-garden-pool.jpg` is William's placeholder (v1)** pending the final render. |
| 3 Cabins | Rewritten to the email's spec: five two-bedroom cabins, two masters, 2.5 baths, kitchenette, porch, private walled garden. No plunge pool (only the one-pager claims one, and the render has none). "Future rooms" gone. New v2 renders. |
| 4 Signature Suites | New `#suites` section after the mansion gallery: two three-bedroom suites, hall as the family's living room, four renders. |
| 5 Two site plans | `#plan` now crossfades `site-plan-phase-1.jpg` and `site-plan-phase-2.jpg` on a Phase 1 / Phase 2 toggle. The inaccurate `concept-expansion-aerial.jpg` and the old `site-plan-final.jpg` are deleted. |
| 6 Three routes | "Two ways forward" replaced with 01 Invest only / 02 Invest & operate / 03 Operate only, plus the structural line from the email. |
| 7 No nav bar | `.brandmark`: floating logo plus the Namou / Hospitality Joint Ventures lockup, top **right** (top-left collides with every media label). Lenis keeps `anchors: true` for the hero's own jump link. |
| 8 Closing gallery | `#album`: 16 new estate photos, tabbed per area, none repeated from higher up the page. Panels are lazy, so only the open tab downloads. |
| William's ask | `#feasibility`: Phase 1 capex, five-year forecast, payback, assumptions, sensitivity, and the musataha and no-rent foundation. |
| Also | `#explore`: nine self-hosted 360 panoramas on pins over the Phase 1 plan (Pannellum, vendored). |

### The 360 section

Insta360 share pages send `content-security-policy: frame-ancestors
https://*.insta360.com`, so they cannot be iframed, and the media URL inside each page
is CloudFront-signed with about six days of life. Both problems are solved by
downloading the equirectangular JPGs once and committing them:
`_tmp-renders/360/fetch-panoramas.py` pulls all ten, `compress-panoramas.py` writes the
web copies (3840x1920, 6.9 MB for ten). `yaw-ruler.py` prints a horizon strip per
panorama with a degree scale, which is how each pin's opening angle was set — do that
rather than guessing.

Link 4, "Majlis 2", is excluded per William's note; the file stays staged.

---

## Still to do

1. **Pin numbering and positions** — William is sending corrections. Each pin is one
   inline `left` / `top` percentage on a `.explore__pin` button.
2. **Final garden pool render** — replaces `assets/concepts/concept-garden-pool.jpg`
   under a new filename, with the old one deleted in the same commit.
3. **Phase 2 plan redraw** — the current `phase 2` image inverts Jad's request: it dims
   Phase 1 and sharpens only the horses and spa, rather than showing the whole estate
   undimmed. It works as a focus-shift pair, and Jad should be told that is what he is
   looking at. Both plans may also change slightly.
4. **Flag to Jad**: his email asks for three partnership routes and the one-pager
   describes two structures. The page follows the email for the routes and the one-pager
   for the economics, and omits the two-structure comparison so the page does not
   contradict itself. The one-pager also lists the Majlis as a shared lounge and bar
   while the render treats a hall as a suite's living room; the estate has more than one
   hall, so both can be true, but he should confirm.

## Decisions taken this round

- **The feasibility numbers are public.** William approved on 2026-07-25, and plans to
  share a Rebrandly link and take the page down after the presentation. Note that a
  Rebrandly password does not protect the canonical Vercel URL, which stays open.
- **The landowner's name is not on the page.** The one-pager names him five times; the
  page says "the owners" throughout. Nothing else was cut for confidentiality.
- `<meta name="robots" content="noindex, nofollow">` is set, so the page can be shared
  without being indexed.

---

## Working notes

- **Local preview:** serve from `proposals/`, not the slug folder, and open
  `/family-farm-al-hudaiba/`. Each page sets `<base href="/<slug>/">`.
- **Verify at 1536x730** as well as 1280 and 375. That viewport catches the
  pinned-section overflow class of bug.
- **Bust the cache when verifying** (`?v=2`): a plain reload serves the old
  `index.html`, so you end up testing edits that never reached the browser.
- **Image generation:** `gemini-3.1-flash-image` via `GEMINI_API_KEY`. Reuse a script in
  `_tmp-renders/` as the pattern.
- **Prompting trap:** never combine "preserve the camera angle, horizon and framing"
  with a request to change depth or spatial layout. Depth is camera position; the model
  will keep the camera. Generate fresh and use the old image for mood only.
- **Deploy:** push to `main`; Vercel deploys itself. Confirm live by polling the public
  URL with Python `urllib` — PowerShell will not follow Vercel's 308 and the Vercel MCP
  403s on this team.
- The 74 estate photos are not in this repo. They sit in
  `../proposal-family-farm-al-hudaiba-v2/photos/`, and `catalogue.md` beside them groups
  them by area. **Index N in that catalogue is the Nth file alphabetically**, which is
  how the gallery selection was resolved.
