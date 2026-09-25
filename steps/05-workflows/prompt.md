# Step 5 · The Workflows

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

Fill `workspace/workflows/` with my first pipeline.

First, read `workspace/CLAUDE.md` to see what's already built. Also read `workspace/specs/` so you can reference my rules in the check step.

Then read this spec file:

- `reference/awp-knowledge-management-standard/directory/kb-area-workflows-skeleton.md` — its `⑦ Build Procedure` tells you what questions to ask

Follow the Build Procedure. Write one workflow this session — just enough to see what a pipeline looks like. Workflow methodology comes in a later episode.

Every workflow file must follow this four-part structure:

```markdown
# [Workflow Name]

## Trigger
When does this run? A schedule ("every Monday"), a command ("when I say: new draft"), or an event ("when a file lands in inbox/").

## Steps
Numbered list of what to do, in order. Each step is one action the agent can execute. Include any research, writing, or file operations. Be specific — "search the web for X" not just "research."

## Check
How to verify the output is good. Reference a standard from specs/ if one applies. List what to look for: word counts, required sections, naming rules, anything measurable.

## Lands in
Where the finished output goes — which folder in business/, dashboard/, or elsewhere. The workflow definition stays in workflows/; only the output moves.
```

Interview me about one task I repeat. Break it into steps with me, then write the workflow file.

After writing the workflow, run it once for real — actually execute every step and show me the output. Apply the check at the end.

Register what you built: add the workflow to the file index in
`workspace/workflows/CLAUDE.md`, and index the run output in the CLAUDE.md of whatever
folder the "Lands in" section sent it to. An unindexed file is one the next agent will never find.

After running, print `tree workspace/workflows/` and wait for my go-ahead.
