# Changelog

All notable changes that affect people following this playbook are recorded here.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the
project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2026-09-25

First public release, tagged `v1.0.0` together with the video tag
`video-002-knowledgebase-skeleton`.

### Changed

- Restructured the repository into four folders: `steps/` (the eight prompts),
  `reference/` (the standard, read-only), `solutions/` (per-step answers and the finished
  knowledge base) and `workspace/` (where your agent builds).
- The video shows the older layout. Paths map as follows:
  - `course/steps/` → `steps/`
  - `course/reference/awp-spec-knowledge-management/` → `reference/awp-knowledge-management-standard/`
  - `course/examples/` → `solutions/NN-slug/`, one folder per step
  - `course/examples/07-import/` → `steps/07-engine/import/`
  - `knowledge-base-complete/` → `solutions/final/`
  - `knowledge-base/` → `workspace/`
- Renamed the standard package to the four-segment name `awp-knowledge-management-standard`,
  including the `document_id` of every file inside it.
- Step 0 now runs `mkdir -p workspace`, because the folder ships with the repository.
- Steps 2 to 7 stop and point you back to step 1 if `workspace/CLAUDE.md` does not exist.
- The step 1 sample tree now shows `specs/`, matching the prompt. The step 6 sample tree is
  now taken from the finished knowledge base and uses `materials/`, as the standard requires.

### Added

- `AGENTS.md` as the single instruction file for agents; `CLAUDE.md` and `GEMINI.md` import it.
- `playbook.yaml` with video, chapter and series metadata.
- Sample answers for step 0 (`solutions/00-setup/expected.txt`) and step 7
  (`solutions/07-engine/tree.txt`).
- Link check (lychee) and text checks (typos, markdownlint) in GitHub Actions.

### Removed

- `knowledge-base-starter/`. Episode 2 starts from an empty folder, so there was nothing in it.
