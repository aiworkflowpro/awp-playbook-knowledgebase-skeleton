# Step 0 · Setup

> Paste everything below the line into your agent.

---

**Where you are** — nowhere yet. This step creates the working directory for Episode 2
(Build a Knowledge Base from an Empty Folder). Run it from wherever you keep your projects.
If you are already inside `awp-playbook-knowledgebase-skeleton`, skip the clone.

After this step, `awp-playbook-knowledgebase-skeleton/` is the working directory for every
later step, and the folders inside it do different jobs:

- `steps/`, `reference/` and `solutions/` are storage — the step prompts, the standard package,
  and the finished answers. Read from them, never write into them.
- `workspace/` is your workspace. Everything you produce goes there.

Clone the playbook repo:

```text
Working directory: the folder where you keep your projects — the clone lands inside it.

git clone https://github.com/aiworkflowpro/awp-playbook-knowledgebase-skeleton
```

Then go into the repo, confirm where you are, and make sure the `workspace` folder exists:

```text
Working directory: the same folder as above — the first command moves you into the repo.

cd awp-playbook-knowledgebase-skeleton
pwd
mkdir -p workspace
```

`pwd` must end with `awp-playbook-knowledgebase-skeleton`. Every path in every later step is
relative to that folder, so from now on run `pwd` at the start of each step and `cd` there if
you are not in it.

Tell me when it is done. Do not read any files yet — just clone, check the folder, and confirm.
