# Namou Proposals

Central repository for Namou's public proposal presentations.

## Architecture

- GitHub: `NamouProperties/proposals-namou`
- Vercel project: `proposal-namou` under `namou-workspace`
- Vercel root directory: `proposals`
- Production branch: `main`
- Public URL pattern: `https://proposal-namou.vercel.app/<slug>/`

Each proposal is a self-contained static site inside `proposals/<slug>/`.

```text
proposals/
  family-farm-al-hudaiba/
    index.html
    assets/
```

## Adding a proposal

1. Create `proposals/<slug>/`.
2. Add its `index.html` and local assets.
3. Keep all asset paths relative to that folder.
4. Commit and push to `main`.
5. Confirm the matching Vercel deployment is READY.
6. Verify `https://proposal-namou.vercel.app/<slug>/`.

Do not commit source PDFs, research, credentials, local previews, or private handoff files. Once a URL has been shared, keep its slug stable.

## Current proposals

- `family-farm-al-hudaiba` - Family Farm Boutique Hotel presentation
