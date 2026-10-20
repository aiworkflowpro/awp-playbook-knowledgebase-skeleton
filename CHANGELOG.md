# Changelog

All notable changes that affect people following this playbook are recorded here.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the
project uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-10-19

First public release, tagged `v1.0.0` together with the video tag
`video-knowledgebase-skeleton`.

### Added

- `steps/`: the eight prompts, from step 0 (setup) to step 7 (import your old files). Steps 2
  to 7 stop and point you back to step 1 if `workspace/CLAUDE.md` does not exist.
- `reference/awp-knowledge-management-standard/`: the knowledge management standard the
  prompts follow, read-only.
- `solutions/`: a sample answer for every step (`solutions/NN-slug/`) and the finished
  knowledge base (`solutions/final/`).
- `workspace/`: the empty folder where your agent builds your knowledge base.
- `AGENTS.md` as the single instruction file for agents; `CLAUDE.md` and `GEMINI.md` import it.
- `playbook.yaml` with video, chapter and series metadata.
- Link check (lychee), text checks (typos, markdownlint) and a language check in GitHub Actions.
