# Step 4 · The Rules

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

Fill `workspace/specs/` with my first rules.

First, read `workspace/CLAUDE.md` to see what's already built.

Then read these two spec files:

- `reference/awp-knowledge-management-standard/directory/kb-area-standards-skeleton.md` — its `⑦ Build Procedure` tells you how to create a standards area
- `reference/awp-knowledge-management-standard/naming/kb-naming-segment-convention.md` — the naming rules that standards must follow

Follow the Build Procedure. Write one or two rules this session — just enough to see what a standard looks like. A deeper dive into rule-writing comes in the next episode.

Every standard file must follow this structure:

```markdown
# [Title]

## Scope
What this rule applies to — all files? Only one folder? Only a certain file type?

## Rule
The actual constraint. One clear sentence. If someone reads only this line, they know what to do.

## Good example
One filename or document snippet that follows the rule.

## Bad example
The same thing done wrong — so the difference is obvious.

## Check
How the agent verifies compliance: what to look for, what command to run, or what pattern to match.
```

Interview me about what rules matter to me. After writing each standard, prove it works: create the same file twice — once breaking the rule, once following it — so I can see the difference.

Register what you built: add every standard to the file index in
`workspace/specs/CLAUDE.md`, one row per file with a one-line summary of the rule. An
unindexed rule is one the next agent will never apply.

After writing all files, print `tree workspace/specs/` and wait for my go-ahead.
