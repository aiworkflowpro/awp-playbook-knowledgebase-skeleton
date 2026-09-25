# AGENTS.md

This repository walks a user through building a personal knowledge base for AI agents,
starting from an empty folder. It accompanies Episode 2 of the AI Workflow Pro series
"Build a Knowledge Base for AI Agents". The result is plain folders and Markdown files
that any agent can read as the user's memory.

## Where you are

Start in the repository root, `awp-playbook-knowledgebase-skeleton/`. Every path in this file
and in every step prompt is relative to that folder. Run `pwd` before each step; if the output
does not end with `awp-playbook-knowledgebase-skeleton`, `cd` there first. An agent running one
level up will not find the standard the steps tell it to read.

```text
awp-playbook-knowledgebase-skeleton/
├── steps/        read-only   eight prompt.md files, 00-setup to 07-engine
├── reference/    read-only   awp-knowledge-management-standard/, the standard (66 files)
├── solutions/    read-only   per-step answers and final/, the finished knowledge base
└── workspace/    writable    the user's knowledge base; starts empty
```

## Folder roles

| Folder | Role |
|--------|------|
| `steps/NN-slug/prompt.md` | One prompt per step. Step 0 sets up the working directory; steps 1 to 7 build the knowledge base. Each step names the standard files to read and what to build. `steps/07-engine/import/` holds the four sample files that step 7 imports. |
| `reference/awp-knowledge-management-standard/` | The Knowledge Base Management Standard: naming rules, directory patterns, area skeletons, methodology. Read only the files a step names. |
| `solutions/NN-slug/` | Short sample answers for each step, for comparison. |
| `solutions/final/` | The full knowledge base from the recorded run: 104 Markdown files, including the standard copied in at step 7. Compare structure and depth; never copy it into `workspace/`. |
| `workspace/` | The only place you write. Its contents are ignored by git, so nothing the user builds is committed back. |

## How a step runs

1. The user pastes a step prompt from `steps/`.
2. Read `workspace/CLAUDE.md` first (from step 2 on) to see what already exists.
3. Read the standard files that step names, and only those.
4. Ask the user questions one at a time, in plain language.
5. Build files inside `workspace/` using the user's own words.
6. Register what you built in the nearest `CLAUDE.md` index.
7. Print the folder tree and wait for the go-ahead before the next step.

Each step may start in a fresh agent session. Do not assume you remember an earlier step;
the knowledge base itself, through its `CLAUDE.md` indexes, is the memory.

## Rules

- Write only inside `workspace/`. `steps/`, `reference/` and `solutions/` are storage.
- Ask one question at a time. No jargon, no unexplained acronyms.
- Write every file from the user's answers, never from placeholder text.
- Follow the naming convention in `reference/awp-knowledge-management-standard/naming/kb-naming-segment-convention.md`.
- Follow the CLAUDE.md authoring standard in `reference/awp-knowledge-management-standard/directory/kb-entry-authoring-standard.md`.
- If an answer makes a folder unnecessary, skip it and explain why.
- Register what you build. After adding a file or folder, update that directory's `CLAUDE.md`
  index. An unindexed file is one the next agent will never find. A new top-level folder needs
  its own `CLAUDE.md` and a row in `workspace/CLAUDE.md`.
- If a step depends on an earlier one and `workspace/CLAUDE.md` is missing, stop and tell the
  user to run step 1 first.
- In step 7, install the standard into the workspace:

  ```bash
  cp -r reference/* workspace/specs/
  ```

  This episode ships one package, so it lands at
  `workspace/specs/awp-knowledge-management-standard/` with all 66 files. From then on the
  standard lives where the agent works, and later sessions read it without being pointed at it.
  That copy is intentional, not a duplicate to clean up.

## Checks

- Structure after step 7 should match `solutions/07-engine/tree.txt` at the top two levels;
  the user's file names and topics will differ.
- Naming check, from the repository root (zero results means compliant):

  ```bash
  find workspace/research workspace/dashboard -type f -name '*.md' ! -name 'CLAUDE.md' \
    | grep -vE '/([a-z0-9]+-)+[a-z0-9]+\.md$'
  ```
