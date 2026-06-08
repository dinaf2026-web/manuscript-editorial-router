# manuscript-editorial-router — Claude Code Skill

The dispatcher for the **Manuscript Editorial Suite**. When an editorial ask is broad
or ambiguous — *"review my book"*, *"is this ready"*, *"full editorial pass"*, *"go
over this chapter"* — this skill decides which critique pass(es) the request needs,
runs them in the right order for the book's genre, and hands off. It does not critique
or score itself; it only routes.

## The six passes it routes to

| Pass | Skill |
|------|-------|
| Craft & acquisitions | `manuscript-publisher-critique` |
| Continuity / canon | `manuscript-continuity-audit` |
| Mystery logic (mystery/thriller) | `manuscript-fair-play-audit` |
| Cinematic / blocking | `manuscript-cinematic-scene-audit` |
| Line craft | `manuscript-prose-immersion-audit` |
| Sales surface (KDP) | `manuscript-listing-critique` |

It also recognizes ledger-maintenance asks and routes them to
`manuscript-canon-ledger`.

## What it does

- **Disambiguates** overlapping requests by *object* (a manuscript vs. a blurb; clue
  logic vs. overall craft; "is the writing alive" vs. "does the scene film").
- **Gates by genre** — only runs the fair-play mystery pass for mystery/crime/
  thriller; skips it (and says why) for memoir, literary, romance, etc.
- **Orders multi-pass reads** — continuity → fair-play → cinematic → prose-immersion
  → publisher, so each pass can reference the prior findings. Listing is independent.

## How it knows your book

On run it walks **up** from your working folder for `.manuscript/profile.md` (the
suite profile); its `genre`/`passes` decide what's applicable. No project is
hard-coded — if there's no profile, it offers to set one up, then routes with
genre-general defaults.

> This is the **6-pass** router (includes the cinematic pass). It supersedes the
> 5-pass router that ships in earlier copies of the suite.

## Install

```powershell
# Windows (PowerShell)
Copy-Item .\manuscript-editorial-router "$env:USERPROFILE\.claude\skills" -Recurse -Force
```
```bash
# macOS / Linux
cp -r manuscript-editorial-router ~/.claude/skills/
```

The router dispatches to the other suite skills — install those too for full
function. Then ask Claude: **"full editorial pass on this chapter."**

## Author
[@dinaf2026-web](https://github.com/dinaf2026-web)

## License
MIT
