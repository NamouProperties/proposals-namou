# Errors and fixes

## A local verification passes or fails against stale HTML

Navigating to the same local URL twice serves `index.html` from the browser cache, so
you test edits that never reached the page. Symptom: a value you just changed still
reads its old number in the DOM. Add a throwaway query string (`?v=2`, `?v=3`) on every
reload during verification. Two separate bugs were chased for several minutes this way
on 2026-07-25, one of them a CSS override that had already been fixed.

## A 360 panorama cannot be embedded from its share link

Insta360 share pages send `content-security-policy: frame-ancestors
https://*.insta360.com`, so an iframe is refused. The equirectangular JPEG inside the
page is reachable (3840x1920, around 2.4 MB) but its URL is CloudFront-signed with an
`Expires` about six days out, and the media host also requires a
`Referer: https://cloud-fra.insta360.com/` header. Hotlinking therefore breaks within
the week.

Download once and commit the file, then render it locally with the vendored Pannellum in
`assets/vendor/`. `_tmp-renders/360/fetch-panoramas.py` does the fetch. The share link
itself is permanent — that is not what expires, and the distinction is worth stating
plainly when someone asks.

## A panorama opens facing the wrong way

Do not guess the opening yaw from a thumbnail. Equirect x maps linearly to yaw, so
`_tmp-renders/360/yaw-ruler.py` renders each panorama's horizon band with a degree scale
printed across it and the angle can be read straight off. Two of nine were more than 90
degrees out when estimated by eye.

## A [hidden] panel still shows

The `hidden` attribute works through the UA stylesheet's `[hidden] { display: none }`,
which any author `display` declaration beats. A tab panel that is also a grid
(`.album__grid { display: grid }`) therefore ignores `hidden` and every panel renders at
once. Pair the class with an explicit `[hidden] { display: none }` rule.

## A wide table pushes the whole page sideways on a phone

`overflow-x: auto` on a wrapper does not clip if the wrapper is a grid or flex item:
those default to `min-width: auto`, so the item takes its min-content width from the
table's `min-width` and the page grows instead. Set `min-width: 0` on the item. Caught
at 375 px as 236 px of document overflow with `body { overflow-x: hidden }` masking it
visually — measure `document.documentElement.scrollWidth - window.innerWidth`, do not
trust the eye.

## An image edit ignores a layout or depth instruction

Never combine "preserve the camera angle, horizon and framing" with a request to
change depth, spacing or spatial layout. Depth in a photograph *is* camera position,
so the two instructions contradict and the model keeps the camera, shuffling only
the furniture inside the same perspective. Three attempts on the terrace render
failed this way before the cause was spotted.

Each API call is stateless, so this is never a case of the model "getting confused"
across attempts - re-read the prompt for a contradiction first. To change
composition, generate fresh with a described camera and use the previous image as a
mood and materials reference only.

## Invoke-WebRequest fails with 308 on Vercel URLs

Windows PowerShell 5.1 does not follow Vercel's 308 redirects (trailing-slash normalization). Use Python `urllib` for deploy checks instead.

## Hero type renders huge in a fallback font

If Satoshi fails to load, keep the fix in place: preload links for weights 300/400/500 plus the `"Satoshi Fallback"` `size-adjust` @font-face. Do not remove them when refactoring the head.

## curl fails with SSL error (exit 35) behind the proxy

Both Git Bash curl and Windows curl.exe fail TLS to external upload hosts. Use PowerShell `Invoke-WebRequest` / `Invoke-RestMethod` or Python `urllib` instead - both trust the proxy certificate here.

## Local preview 404s on every asset

Serve from `proposals/`, not from inside the slug folder, and open
`http://127.0.0.1:PORT/<slug>/`. Each proposal sets `<base href="/<slug>/">`, so
serving from the slug folder makes every relative asset resolve to
`/<slug>/assets/...` and 404 - which silently takes out GSAP, ScrollTrigger and
Lenis, so motion appears "broken" for a reason that does not exist in production.

This was previously recorded here as `http.server` "dropping connections". It is
not a connection problem; the requests are plain 404s. Check the console for the
request path before blaming the server.

## Vercel MCP cannot access namou-workspace

The claude.ai Vercel connector token is not scoped to the `namou-workspace` team (403). Verify deployments by polling the public URL for new content instead, or use the Vercel CLI with the token from `14_Proposals/.env-proposals.txt`.

## Lenis or GSAP motion is missing

Do not depend on unpkg or jsDelivr at runtime for core presentation behavior. Keep pinned copies of Lenis, GSAP, ScrollTrigger, and required styles inside the proposal's `assets/vendor/` folder.

For the Family Farm proposal, confirm the page adds the `lenis` class to `<html>`, GSAP applies inline animation styles, and vertical scrolling advances a pinned gallery's `scrollLeft`.

## A scroll animation is stuck at its start or end value

A pinned section adds its scroll distance to the page, so every trigger created
*before* the pin measures a document that is short by exactly that distance. The
later animation then plays out one pin-distance too early - it has already
finished by the time you reach the section, so it reads as frozen.

Give every pinned ScrollTrigger `refreshPriority: 1` so pins measure first. To
confirm the diagnosis, compare a trigger's `start` against reality:

```js
const st = ScrollTrigger.getAll().filter(t => t.trigger === el)[0];
Math.round(st.start) - Math.round(el.getBoundingClientRect().top + scrollY - innerHeight);
```

A non-zero result is the drift, and it will match a pinned track's
`scrollWidth - clientWidth`. `ScrollTrigger.refresh()` does not fix it - refresh
order is the bug.

## A scrubbed animation lags or smears

A CSS `transition` on the same property GSAP scrubs makes the browser ease toward
each new per-frame value. Scope hover transitions away from any element under a
scrub, as `.rooftop > .zoomable img { transition: none; }` does.

## Pinned section is cut off by the bottom of the window

While pinned, the section's top is locked to the viewport top, so anything past
`100dvh` is unreachable. Do not size the media inside it with a fixed guess like
`58dvh` - a heading that wraps to one more line silently pushes the media under
the window edge, and it only shows up on short screens.

Cap the section with `height: 100dvh` and let the track absorb the remainder
(`flex: 1 1 auto; min-height: 0`), sizing slides from that leftover height with
`aspect-ratio` plus a `max-width` cap for tall screens. Verify with
`section.getBoundingClientRect().height - innerHeight === 0` at 1536x730, which
is the size that catches it.

## Proposal returns 404

Confirm the page exists at `proposals/<slug>/index.html` and that the Vercel project's root directory is exactly `proposals`.

## URL incorrectly includes `/proposals/`

The Vercel root directory is missing or wrong. Set it to `proposals`; the public path should contain only the proposal slug.

## GitHub push does not trigger Vercel

Confirm the Vercel project is linked to `NamouProperties/proposals-namou`, the production branch is `main`, and the GitHub integration still has access to the repository.

## Page loads but media is missing

Use relative paths such as `assets/image.jpg`. Check filename casing because Vercel paths are case-sensitive.

## Updated asset looks stale

Assets may be cached aggressively. Prefer a new filename for changed images or videos instead of replacing an existing immutable asset URL.

**Delete the superseded file in the same commit.** Renaming for a cache bust leaves the old asset tracked and deploying forever. Four orphans (17 MB, including a 16 MB replaced hero video) accumulated this way before the 2026-07-23 sweep. After any rename or section removal, check for assets no longer referenced:

```bash
cd proposals/<slug>
for f in $(git ls-files assets/ | grep -Ev 'vendor/|fonts/'); do
  grep -q "$(basename "$f")" index.html || echo "ORPHAN: $f"
done
```

## Git push hangs for minutes, then times out

Git Credential Manager pops a GUI "Select an account" picker when more than one
GitHub account is stored (here: `NamouProperties` and `will-rads`) and no default
is configured. An agent shell is non-interactive, so the dialog blocks until the
command is killed - the push itself is fine and completes the moment someone
clicks. `git ls-remote` stays fast because it uses a cached credential, which
makes this look like a slow-network problem when it is not.

Fix - name the account for the remote (already set locally in this repo):

```bash
git config --local credential.https://github.com.username will-rads
```

Add `--global` instead to stop the picker in every repo on this machine.

## Git authentication fails

The stored GitHub PAT may be rejected in a Bearer header by Git. Use GitHub's `x-access-token:<PAT>` Basic authentication form without printing or saving the token.

## Large file rejected by GitHub

Keep every individual file below GitHub's 100 MB limit. Compress larger videos before committing.

## Standalone Jad link

Do not rename, repoint, or delete the existing `family-farm-al-hudaiba` Vercel project while that link is in use. The shared-repository version is a separate deployment.
