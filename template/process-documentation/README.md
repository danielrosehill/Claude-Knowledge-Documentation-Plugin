# {{WORKSPACE_NAME}}

Process and SOP documentation for **{{DOC_DOMAIN}}**, maintained with the [knowledge-documentation Claude Code plugin](https://github.com/danielrosehill/Claude-Knowledge-Documentation-Plugin).

## Structure

- `processes/` — step-by-step procedures.
- `workflows/` — higher-level workflows that orchestrate multiple processes.
- `sops/` — formal SOPs grounded in authoritative sources.
- `checklists/` — quick-reference checkbox lists.
- `flowcharts/` — decision flowcharts (Mermaid).
- `handbook/` — compiled handbook output.

## Commands

- `/knowledge-documentation:new-page "Title" --type=<process|workflow|sop|checklist|flowchart>`
- `/knowledge-documentation:index-topic` — refresh `handbook/INDEX.md`
- `/knowledge-documentation:cross-link` — link SOPs to processes and workflows
- `/knowledge-documentation:version-doc <path>` — bump version and append history
- `/knowledge-documentation:compile-handbook` — assemble `handbook/process-handbook.md`
