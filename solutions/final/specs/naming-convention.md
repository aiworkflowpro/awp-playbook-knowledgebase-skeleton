# Naming Convention

## Scope

This rule covers **content that accumulates**: research material, reports, drafts, published pieces, run results. You will end up with many of them, and you will look for them by date and topic — so date and topic go in the name.

It does not cover:

| Not covered | Why |
|---|---|
| `CLAUDE.md` and other fixed system files | The tools that read them require those exact names |
| One-topic-per-area files — `owner/profile.md`, `brand/identity.md` | The directory already says the scope; the filename only has to say the topic |
| Everything under `specs/` and `skills/` | A standard or a Skill is a package with a fixed internal shape (`SKILL.md`, `workflow/step01-*.md`). That shape is what makes it readable and runnable |
| Files imported from elsewhere, until you rewrite them | Renaming someone else's file breaks the trail back to the source |

One test: **will there be many of these, arriving over time?** If yes, use the four-part name. If it is the single file that describes an area, keep it short.

## Rule
Every filename follows the four-part structure: `{type}-{object}-{scope}-{date}.md` — lowercase, hyphens between parts, no spaces, no special characters, and dates always in compact form (`YYYYMMDD`, never `YYYY-MM-DD`).

- `type` — what kind of file it is (video, post, report, note)
- `object` — what it is about (script, thread, analysis)
- `scope` — where it belongs (youtube, x, owner, brand)
- `date` — compact date, no dashes

In time-sorted folders (like `inbox/`), the date leads: `{date}-{type}-{object}-{scope}.md`.

Keep the whole filename under 60 characters.

(Source: inbox/old-naming-rules.md, 2026-08-24 — only the 60-character cap was new; lowercase, hyphens, and compact dates were already in this rule.)

## Good example
- `video-script-youtube-20260824.md`
- `20260824-post-x-thread-ai.md` (in inbox, date first)
- `report-analytics-youtube-20260824.md`

## Bad example
- `Video Script v2 FINAL.md` — capitals, spaces, vague version words
- `video-script-youtube-2026-08-24.md` — wrong date format, breaks the four-part count
- `my_script_final_v2.md` — wrong structure

## Check
Run this against the areas the rule covers — zero results means compliant:
```bash
find workspace/research workspace/dashboard -type f -name '*.md' \
  ! -name 'CLAUDE.md' 2>/dev/null \
  | grep -vE '/([a-z0-9]+-)+[a-z0-9]+\.md$'
```
The pattern allows both orders — `video-script-youtube-20260824.md` and the date-first form used in time-sorted folders.
