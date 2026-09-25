# Step 6 · The Knowledge

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

Fill `workspace/research/` with my first knowledge entries.

First, read `workspace/CLAUDE.md` to see what's already built.

Then read this spec file:

- `reference/awp-knowledge-management-standard/directory/kb-area-research-skeleton.md` — its `⑦ Build Procedure` tells you how to organize research

Follow the Build Procedure. Remember: dimension folders on the outside, time folders on the inside. Never deeper than four levels.

Register what you built: add every topic to the subdirectory index in
`workspace/research/CLAUDE.md` with its trigger words, and give each topic its own CLAUDE.md
listing the material underneath it. An unindexed topic is one the next agent will never find.

After writing all files, print `tree workspace/research/` and wait for my go-ahead.
