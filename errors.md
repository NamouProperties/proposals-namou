# Errors and fixes

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

## Git authentication fails

The stored GitHub PAT may be rejected in a Bearer header by Git. Use GitHub's `x-access-token:<PAT>` Basic authentication form without printing or saving the token.

## Large file rejected by GitHub

Keep every individual file below GitHub's 100 MB limit. Compress larger videos before committing.

## Standalone Jad link

Do not rename, repoint, or delete the existing `family-farm-al-hudaiba` Vercel project while that link is in use. The shared-repository version is a separate deployment.
