# Dashboard

> Run results — task output and status snapshots, organized by month. Output folder ready.

This area records what the agent actually did: outputs of completed tasks and status snapshots of the business over time. Month folders hold the history of runs.

## Subdirectory Index

| Directory | Content |
|-----------|---------|
| `output/` | Run results, one subfolder per run, by month — `output/{YYYYMM}/` |

The current month folder `output/202608/` exists and is empty: the structure is in place, no runs
recorded yet. Every future workflow run lands in the current month folder, one subfolder per run.
