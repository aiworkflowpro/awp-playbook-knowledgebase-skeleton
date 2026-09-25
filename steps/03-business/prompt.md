# Step 3 · The Business

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

Fill `workspace/business/` with my work areas.

First, read `workspace/CLAUDE.md` to see what's already built.

Then read this spec file — its `⑦ Build Procedure` section tells you what questions to ask:

- `reference/awp-knowledge-management-standard/directory/kb-area-business-skeleton.md`

Follow the Build Procedure. Only create the arenas I name — don't invent ones I didn't mention.

Register what you built: add every arena you created to the subdirectory index in
`workspace/business/CLAUDE.md` — directory, what gets delivered there, trigger words — and
give each arena its own CLAUDE.md. An unindexed folder is one the next agent will never find.

After writing all files, print `tree workspace/business/` and wait for my go-ahead.
