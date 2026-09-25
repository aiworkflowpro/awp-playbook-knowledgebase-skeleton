# Step 7 · The Engine

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

Set up `workspace/dashboard/` and `workspace/inbox/`, import real files through the inbox, then move the standard into the knowledge base.

First, read `workspace/CLAUDE.md` to see what's already built.

**Phase 1 — Build dashboard:**

Read `reference/awp-knowledge-management-standard/directory/kb-area-dashboard-skeleton.md` — follow its `⑦ Build Procedure`. Create `workspace/dashboard/output/{YYYYMM}/` for the current month.

Register it: `workspace/dashboard/CLAUDE.md` gets a subdirectory index row for `output/`
saying that run results land in the current month folder, one subfolder per run.

**Phase 2 — Build inbox and process imports:**

Read `reference/awp-knowledge-management-standard/directory/kb-area-inbox-skeleton.md` — follow its `⑦ Build Procedure` to create `workspace/inbox/`.

Then copy the four sample files from `steps/07-engine/import/` into `workspace/inbox/`:

```text
Working directory: awp-playbook-knowledgebase-skeleton/ — run `pwd` first and `cd` there if you are not in it.

cp steps/07-engine/import/*.md workspace/inbox/
```

Now process them — there are four files to import:

Read `reference/awp-knowledge-management-standard/directory/kb-area-inbox-ingest.md` — the document ingestion specification. Follow it exactly:

1. Process one document at a time: read full content, determine which of the eight top-level folders it belongs to, read that folder's CLAUDE.md.
2. For each document, choose one of two modes:
   - **Place**: the document is independent and complete — copy it as-is to the target folder, rename per naming convention.
   - **Extract**: the document contains information that should update existing files — read the target file first, merge without duplication.
3. Show me each proposal (source → target, mode, confidence) and wait for my confirmation before executing.
4. Register every placed or updated file in its target folder's CLAUDE.md index before moving on to the next document. An unindexed file is one the next agent will never find.
5. After all documents are processed, move the originals from `workspace/inbox/` to `workspace/inbox/archive/{YYYYMM}/{YYYYMMDD}-import-batch-archive/` — never delete. Write an `import-log.md` in that batch folder with one row per document: source file, target, mode, date.

**Phase 3 — Move the standard into the knowledge base:**

Up to now you have been reading the standard from `reference/` — storage, where
the material is kept. From here on it lives in your workspace instead:

```text
Working directory: awp-playbook-knowledgebase-skeleton/ — run `pwd` first and `cd` there if you are not in it.
All paths below are relative to that folder.

Copy every package in reference/ into workspace/specs/, keeping each package
folder and its structure exactly as it is:

    cp -r reference/* workspace/specs/

This episode ships one package, so it must end up at
workspace/specs/awp-knowledge-management-standard/ with all 66 files.

Then register it in workspace/specs/CLAUDE.md — a row in the subdirectory index with
trigger words, plus a changelog line.
```

`reference/` is storage. `workspace/` is where your agent works. A rule your agent follows
every day belongs in the workspace, not in a folder it has to reach outside for. From this
point on, the standard that built this knowledge base is *inside* the knowledge base — and
every future session picks it up automatically, without you pointing at it.

After all three phases, print `tree workspace/ -L 2` and wait for my go-ahead.
