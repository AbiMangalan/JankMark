# JankMark (public repo) — Context for Claude Code

> This is the PUBLIC distribution repo. It contains NO source code.
> Source lives in the private sibling repo: `D:\Workspace\JankMark-src\`

## What this repo is

**JankMark** is a zero-overlay Android performance profiler made by
Abi Mangalan (GitHub @AbiMangalan / YouTube: SoC Benchmarks).

This repo's sole purpose:
- Be the landing page where users download, read docs, and give feedback.
- Host compiled Windows installers via **GitHub Releases**.
- Host user-facing documentation in `docs/`.
- Host issue templates and Discussions for community feedback.

**Source code is never committed here.** Installers are dropped into Releases
manually (or later via CI from the private `JankMark-src` repo).

## Local directory layout

```
D:\Workspace\JankMark\          ← this repo (public)
D:\Workspace\JankMark-src\      ← source repo (private, never publish)
```

## Files in this repo

| Path | Purpose |
|---|---|
| `README.md` | Main landing page — features, install, links |
| `CHANGELOG.md` | User-facing release notes, one section per version |
| `SECURITY.md` | Vulnerability disclosure policy |
| `LICENSE` | Proprietary, closed-source notice |
| `MAINTAINER_NOTES.md` | Private ops notes (git-ignored, never pushed) |
| `docs/CONNECTING.md` | USB + wireless ADB setup guide |
| `docs/INSTALL.md` | Windows install + SmartScreen note |
| `docs/FAQ.md` | Common questions |
| `docs/TROUBLESHOOTING.md` | Wireless re-pairing, USB issues, log collection |
| `assets/` | Brand images for README / social preview |
| `.github/` | Issue templates, Discussions config |

## What to update and when

**On every release:**
1. `CHANGELOG.md` — add a section for the new version.
2. Create a GitHub Release, tag `vX.Y.Z`, attach the installer `.exe`.

**When docs change in JankMark-src:**
- Copy `TROUBLESHOOTING.md` from `D:\Workspace\JankMark-src\TROUBLESHOOTING.md`
  into `docs/TROUBLESHOOTING.md` here.
- Update `docs/CONNECTING.md` / `docs/FAQ.md` if connection or feature behavior
  changed.

**When branding changes:**
- Drop new assets in `assets/` and update image references in `README.md`.

## House rules for Claude Code in this repo

- **Never add source code** — not even snippets or build scripts.
- **Never add developer-facing docs** (architecture, API, contribution guides).
  Those belong in the private repo.
- Keep docs written for end users: smartphone reviewers, enthusiasts, non-devs.
- `MAINTAINER_NOTES.md` is git-ignored — keep it that way.
- Before editing `README.md`, read it first; don't duplicate or contradict the
  existing features list. Update conservatively — users cite README text in reviews.

## Current release status (as of 2026-06-23)

- **v0.2.1-beta** is the target first public release. Source is code-complete in
  `JankMark-src` and **pushed to `master`** (includes the 2026-06-23 pre-release
  UI/UX polish pass); tests green (53/53), ruff clean, mypy 21.
- Installer is not yet built/uploaded. README, CHANGELOG, and docs/METRICS here
  are updated to the 0.2.1-beta feature set.
- Steps remaining: local device testing → `just build` → `just installer` in
  `JankMark-src` → upload the installer to GitHub Releases here → push tag
  `v0.2.1-beta`.
