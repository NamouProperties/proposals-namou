# Context

## Purpose

This repository is the shared publishing home for Namou proposal presentations. It follows the same model as `NamouProperties/namou-brochures`: one GitHub repository, one Git-linked Vercel project, and one folder per public slug.

## Current architecture

```text
GitHub main branch
  -> proposals/<slug>/
  -> Vercel project proposal-namou
  -> Vercel rootDirectory = proposals
  -> https://proposal-namou.vercel.app/<slug>/
```

- Repository: `NamouProperties/proposals-namou`
- Vercel team: `namou-workspace`
- Vercel project: `proposal-namou`
- Production branch: `main`
- Framework: none; static files only

## Current proposal

- Folder: `proposals/family-farm-al-hudaiba/`
- Canonical URL: `https://proposal-namou.vercel.app/family-farm-al-hudaiba/`
- Previous standalone URL: `https://family-farm-al-hudaiba.vercel.app/`

The standalone project remains live because it was already shared. Future updates and new proposals belong in this repository and the shared `proposal-namou` Vercel project.

## Publishing contract

- Every proposal must be self-contained inside its slug folder.
- Use relative asset paths so pages work at nested URLs.
- Commit only public presentation files.
- Never commit tokens, environment files, confidential source documents, research folders, or internal handoff notes.
- Push complete proposal changes in one commit where practical.
- Confirm the Git-linked Vercel deployment reaches READY before sharing the new URL.
