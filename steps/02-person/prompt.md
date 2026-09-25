# Step 2 · The Person

> Paste everything below the line into your agent.

---

**Where you are** — repository `awp-playbook-knowledgebase-skeleton`, Episode 2 · Build a Knowledge Base from an Empty Folder.

Run `pwd` first. It must end with `awp-playbook-knowledgebase-skeleton`. If it does not, `cd` into that
folder before doing anything else; every path below is relative to it.

- `steps/`, `reference/` and `solutions/` are storage — the step prompts, the standard package,
  and the finished answers. Read from them, never write into them.
- `workspace/` is your workspace. Everything you produce goes there.

This step builds on the earlier ones. If `workspace/CLAUDE.md` does not exist, stop and tell me
to run step 1 first — do not guess.

Fill `workspace/owner/` and `workspace/brand/` with real content about me.

First, read `workspace/CLAUDE.md` to see what's already built.

Then read these two spec files — each has a `⑦ Build Procedure` section that tells you exactly what questions to ask and what files to create:

- `reference/awp-knowledge-management-standard/directory/kb-area-owner-skeleton.md` — for the owner area
- `reference/awp-knowledge-management-standard/directory/kb-area-brand-skeleton.md` — for the brand area

Follow each Build Procedure in order. Ask me one question at a time. Write every file using my own words — from my answers, not from placeholder text.

After writing all files, prove it works: write a two-line intro of me in my brand voice.

Register what you built: add every new file to the file index in `workspace/owner/CLAUDE.md`
and `workspace/brand/CLAUDE.md`, and update `workspace/CLAUDE.md` if the area
description changed. An unindexed file is one the next agent will never find.

Then print `tree workspace/owner/ workspace/brand/` and wait for my go-ahead.
