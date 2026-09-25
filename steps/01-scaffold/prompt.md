# Step 1 · The Skeleton

> Paste everything below the line into your agent.

---

**Where you are** — repository `awp-playbook-knowledgebase-skeleton`, Episode 2 · Build a Knowledge Base from an Empty Folder.

Run `pwd` first. It must end with `awp-playbook-knowledgebase-skeleton`. If it does not, `cd` into that
folder before doing anything else; every path below is relative to it.

- `steps/`, `reference/` and `solutions/` are storage — the step prompts, the standard package,
  and the finished answers. Read from them, never write into them.
- `workspace/` is your workspace. Everything you produce goes there.

Build my knowledge base skeleton in `workspace/`.

Read this one spec file first — it explains how to write CLAUDE.md signpost files:

- `reference/awp-knowledge-management-standard/directory/kb-entry-authoring-standard.md`

Then create the root router `workspace/CLAUDE.md` — this is the file every later step opens
first to see what already exists.

Then create these eight top-level folders inside `workspace/`, each with a CLAUDE.md:

| Folder | What it holds |
|--------|--------------|
| `owner/` | Who I am — background, skills, decisions, communication style |
| `brand/` | How I sound — identity, positioning, expression, visual assets |
| `business/` | Where my work lands — products, services, operations data |
| `specs/` | My rules — naming, writing, development conventions |
| `workflows/` | My pipelines — creation, publishing, research, operations |
| `research/` | What I know — topics, references, analysis |
| `dashboard/` | Run results — task output, status snapshots, by month |
| `inbox/` | Staging area — new files land here, get sorted into the right folder |

Each CLAUDE.md should follow the authoring standard you just read: one-line positioning quote at the top, a brief description of the area, and "skeleton only for now" (current-state law — don't index files that don't exist yet).

Before you start building, interview me — ask these three questions one at a time:

1. What is your name, and what do you do?
2. What do you want the agent to handle first?
3. Is there anything the agent should never touch?

Use my answers to customize the CLAUDE.md files.

Register what you built: `workspace/CLAUDE.md` must carry a subdirectory index with one row
per folder — directory, what it holds, trigger words. An unindexed folder is one the next agent
will never find.

After building, print `tree workspace/` and wait for my go-ahead before moving on.
