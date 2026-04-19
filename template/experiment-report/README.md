# {{WORKSPACE_NAME}}

Experiment and evaluation workspace for **{{EXPERIMENT_FOCUS}}**, maintained with the [knowledge-documentation Claude Code plugin](https://github.com/danielrosehill/Claude-Knowledge-Documentation-Plugin).

## Structure

- `design/` — experiment design documents.
- `trials/` — raw trial data, one folder per run.
- `analysis/` — charts, stats, intermediate analysis.
- `reports/` — final reports.

## Commands

- `/knowledge-documentation:new-page "Title" --type=design`
- `/knowledge-documentation:new-page "Title" --type=report`
- `/knowledge-documentation:cross-link` — wire reports to their designs and trials
- `/knowledge-documentation:version-doc <path>`
- `/knowledge-documentation:compile-handbook` — compile a combined report
