# Document Format

## Scope
All content files in this knowledge base, from now on. `CLAUDE.md` index files follow their own authoring standard and are exempt.

## Rule
Every document opens with a metadata block (document_id, language, publication, title) fenced by `---`, then the title (`# Title`), then the body. The metadata comes first because that is the only position a YAML front-matter parser reads. Write in plain, simple English that a beginner can follow. One topic per file; keep files short and focused. Write from Leo's actual words and real facts — never placeholder or invented content.

## Good example
```markdown
---
document_id: awp-knowledge-base/video-script
language: en
publication: public
title: "Video Script"
---

# Video Script

Body written in plain simple English, one topic, short and focused.
```

## Bad example
- A file with no title and no metadata block
- Long unbroken paragraphs mixing many topics
- Placeholder text like "Lorem ipsum", "TODO", or invented facts Leo never said

## Check
- Content files (not `CLAUDE.md`) open with a `---` metadata block, followed by a `# ` title line
- `CLAUDE.md` files start straight at the `# ` title — they carry no metadata block
- No placeholder words anywhere (specs/ files are excluded — they list these words as examples): `grep -rn 'TODO\|Lorem\|TBD' workspace/ --include='*.md' | grep -v 'specs/'` — zero results means compliant
