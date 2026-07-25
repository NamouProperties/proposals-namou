# Handoff — Family Farmhouse revision round

Written 2026-07-25. Covers the revision round triggered by Jad's email of Friday
2026-07-24. Read this with `memory.md` (decisions), `errors.md` (known failures)
and `context.md` (publishing contract).

Live page: `https://proposal-namou.vercel.app/family-farm-al-hudaiba/`

---

## Sources of truth — read these before acting

1. **Jad's email, "Family Farmhouse — Revisions", Fri 2026-07-24 07:25**, to
   william@namou.ae. Gmail thread id `19f93040b655e26b`. Eight numbered points.
   No attachments, no links. **This is the authoritative brief for this round —
   work from the email itself, not from the summary below.**
2. **Google Meet transcript, "family farm", Wed 2026-07-22**, Jad + Rayane Antar +
   William. Drive id `1i_K1zMnkc_HyJXvRPZXXT1GP4CbyOxCkp0CLoW78yBU`. Carries hard
   specs the email omits (pool dimensions, cabin count and siting, why the Dome
   changes use, the Barn's capacity, the swings, what to delete from the plan).
3. **`Family_Farmhouse_Feasibility_OnePager`**, Drive id
   `1pNJprDexez_pJiDK7BxespUugt_7qA3UNRKWQpIZf6w`, owned by Jad, created
   2026-07-24, still being edited (last seen modified 2026-07-25 07:57).
   William wants this reflected at the end of the page. **See the warning below.**

---

## Done this round

### Two motion bugs fixed and pushed (commit `56dddd6`)

- **Rooftop parallax was dead.** Its ScrollTriggers were created before the pinned
  mansion gallery, so they measured the page without that pin's 4,061 px spacer and
  ran their whole scrub 4,061 px early. Fixed with `refreshPriority: 1` on both
  pinned triggers. Any tween created before a pin has the same latent bug.
- **`.zoomable img` had a 0.8 s hover transition** that also applied under the
  rooftop scrub, smearing it. Disabled for that one image.
- **Mansion gallery overflowed the viewport while pinned** — 872 px tall in a 730 px
  window, hiding the bottom 142 px. Section is now capped to the viewport with the
  track absorbing the remainder. Verified at 375 / 1280×800 / 1536×730 / 1920×1080.

### Seven concept renders approved, staged in `_tmp-renders/`, NOT yet committed

All generated with Gemini `gemini-3.1-flash-image` at 2K, 16:9, from the real
estate photos in `../proposal-family-farm-al-hudaiba-v2/photos/`. Generation
scripts sit beside the outputs in `_tmp-renders/`.

| Source file in `_tmp-renders/` | Target name in `assets/concepts/` | Purpose |
|---|---|---|
| `concept-terrace-evening-v9-2k.jpg` | `concept-terrace-evening.jpg` | Replaces the rooftop image (Jad #1) |
| `concept-cabin-exterior-v3-2k.jpg` | `concept-cabin-exterior-v2.jpg` | Replaces cabin exterior (Jad #3) |
| `concept-cabin-interior-v3-2k.jpg` | `concept-cabin-interior-v2.jpg` | Replaces the bunk-nook interior (Jad #3) |
| `concept-suite-hall-v1-2k.jpg` | `concept-suite-hall.jpg` | New — Signature Suites hero (Jad #4) |
| `concept-suite-majlis-v1-2k.jpg` | `concept-suite-majlis.jpg` | New — second suite living hall (Jad #4) |
| `concept-suite-bedroom-a-v2-2k.jpg` | `concept-suite-bedroom-a.jpg` | New (Jad #4) |
| `concept-suite-bedroom-b-v2-2k.jpg` | `concept-suite-bedroom-b.jpg` | New (Jad #4) |

On commit, delete the superseded `concept-rooftop-night.jpg`,
`concept-cabin-exterior.jpg` and `concept-cabin-interior.jpg`, then run the orphan
check in `errors.md`. Compress before committing.

### Reference photos used

The 74 estate photos are **not** in this repo. They live, duplicated, in
`../proposal-family-farm-al-hudaiba/photos/` and
`../proposal-family-farm-al-hudaiba-v2/photos/` (192 MB each, byte-identical).
`../proposal-family-farm-al-hudaiba-v2/catalogue.md` groups all 74 by area and maps
index numbers to filenames — **use it instead of scanning images.** There are no
360 panoramas in the set; the Drive download never contained any.

Key files: terrace `BF4DA442`, suite hall `ECD08800`, majlis `3F653FAD`,
bedrooms `D44B2998` and `39BB6441`, villa exterior `1F50EFCD`, garden `62A073EC`.

---

## Still to do

### Blocked

1. **Two site plans (Jad #5)** — Phase 1 in colour with Phase 2 dimmed, and Phase 2
   undimmed showing stables and spa. Jad wrote "I'll supply them" about the correct
   parcel boundaries. Nothing has arrived by email. The current expansion drawing is
   wrong and must not be reused. He also said in the meeting that he had sent
   material on WhatsApp — check there before chasing him.
2. **Bottom gallery (Jad #8)** — all photos plus 360° views, tabbed per area
   (Majlis, halls, bedrooms, Dome, kitchen, terrace, gardens, animal areas, palms).
   Needs assets we do not have: the 360s do not exist in the 74. Heaviest item on
   the list; will need a compression pass before anything is committed.

### Open, not blocked

3. **Garden pool (Jad #2)** — two renders exist in `_tmp-renders/`
   (`concept-garden-pool-v1-2k.jpg`, `-v2-2k.jpg`); neither approved. v1 is brighter
   and better composed but its swimwear reads western-resort, which is a risk for a
   UAE family pitch. v2 is calmer and more modest. Spec from the transcript:
   rectangular, 10 m × 5 m, sunbeds all round, beside the mansion.
4. **Copy: "rooftop" → "the terrace"** — 16 occurrences. Drop "under the stars"
   entirely; the terrace is covered at one end and the phrase cannot survive. Keep
   the evening-dining concept, which Jad explicitly asked to retain.
5. **Cabin copy** — replace "simple timber cabins", remove "Future rooms" (2
   occurrences). Cabins are Phase 1; only the expansion land is future.
6. **Partnership section (Jad #6)** — replace "Two ways forward". See the conflict
   below before writing this.
7. **Remove the nav bar (Jad #7)** — logo only, floating, with the lockup
   **Namou / Hospitality Joint Ventures**. This also brings the page back in line
   with the house "no site chrome" rule. Note it removes the anchor links, which
   makes Lenis's `anchors: true` setting idle.
8. **Feasibility content at the end of the page** — William's request. Read the
   warning below first.

---

## Warnings — resolve before building

### The feasibility one-pager is marked Private & Confidential

`Family_Farmhouse_Feasibility_OnePager` carries the footer *"Private &
Confidential"* and contains the landowner's name, the AED 5.77M Phase 1 investment
breakdown, a five-year P&L, rate assumptions, the musataha term and the JV
waterfall. **Everything under a slug folder on this repo is public.** Publishing it
as-is would put the owner's name and the venture's economics on an open URL.

Do not paste it in. Either agree with Jad and William exactly which figures may go
public, or reduce it to a non-confidential summary. Flagged to William 2026-07-25;
awaiting his decision.

### The one-pager contradicts Jad's email on the partnership routes

- **Jad's email (#6)** asks for **three** routes: 01 Invest only, 02 Invest &
  operate, 03 Operate only, plus the line *"Each partnership is structured as a
  joint venture with long-term registered land rights."*
- **The one-pager** describes only **two** structures: Operator as Investing Partner
  (Invest & Operate), and Operator as Tenant (Lease / Operate only). It also
  specifies a **50-year registered musataha**, which is more precise than the
  email's wording.

Ask Jad which is current before building the section. The one-pager is the newer
document, but the email is the direct instruction.

### The one-pager contradicts what we rendered for the second suite

The one-pager lists **7 keys: 2 Signature Suites + 5 Premium Cabins**, and lists the
**"Majlis lounge & bar"** as a facility alongside the Dome restaurant — that is, a
shared guest space, not a suite. We rendered the majlis (`3F653FAD`) as the second
Signature Suite's private living hall. Those cannot both be true.

Either the second suite uses a different hall, or `concept-suite-majlis.jpg` should
be relabelled as the Majlis lounge and bar. Confirm with Jad.

### The one-pager adds specification the email did not

- Cabins include a **private garden and plunge pool**. The approved cabin exterior
  render has a walled garden but **no plunge pool**.
- Kids' World is named: Barn club, adventure playground, **shaded kids' pool**,
  animal welfare upgrades.
- Opening target **Q4 2027**; the Dome becomes a licensed restaurant and bar.

Decide whether the page should carry these before the renders are finalised.

### Confidential material that must never reach the page

From the meeting transcript: the landowner's name, AdMind as the target partner, the
~AED 2M renovation figure Jad quoted, Jad's own equity intentions, and CBRE. None of
it belongs on a public URL.

---

## Working notes

- **Local preview:** serve from `proposals/`, not the slug folder, and open
  `/family-farm-al-hudaiba/`. Each page sets `<base href="/<slug>/">`, so serving
  from inside the slug folder 404s every asset and silently kills GSAP, ScrollTrigger
  and Lenis. See `errors.md`.
- **Verify at 1536×730.** That viewport catches the pinned-section overflow class of
  bug; 1280×800 does not.
- **Image generation:** `gemini-3.1-flash-image` via `GEMINI_API_KEY` from the
  Windows user environment. Reuse a script in `_tmp-renders/` as the pattern.
- **Prompting trap:** never combine "preserve the camera angle, horizon and framing"
  with a request to change depth or spatial layout. Depth is camera position; the two
  instructions contradict and the model will silently keep the camera. To change
  composition, generate fresh and use the old image for mood only.
- **Deploy:** push to `main`; Vercel deploys itself. Confirm live by polling the
  public URL with Python `urllib` — PowerShell will not follow Vercel's 308 and the
  Vercel MCP 403s on this team.
