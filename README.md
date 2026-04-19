# knowledge-documentation-plugin

Claude Code plugin for structured knowledge documentation — wikis, curated resource libraries, process/SOP documentation, and experiment reports. Ships indexing, cross-linking, taxonomy, and versioning primitives plus a provisioning skill to spin up a fresh documentation workspace.

Part of the [danielrosehill Claude Code marketplace](https://github.com/danielrosehill/Claude-Code-Plugins).

## What you get

### Primitives (always available once the plugin is installed)

Knowledge-base commands (`/knowledge-documentation:*`):

- `index-topic` — generate or refresh an index/TOC for a topic area
- `cross-link` — detect and insert cross-references between related pages
- `build-taxonomy` — analyse content and propose or apply a category taxonomy
- `version-doc` — version-stamp a document and update its history footer
- `audit-links` — scan for broken or stale links across the workspace
- `new-page` — scaffold a new page with the variant's required frontmatter
- `compile-handbook` — assemble individual documents into a bound handbook/guide output

### Provisioning skill

- `/knowledge-documentation:new-workspace <name> [--variant=wiki|resource-library|process-documentation|experiment-report] [--local-only] [--private]`

Scaffolds a new workspace (CLAUDE.md + variant-specific directory structure), personalises it from `~/.claude/CLAUDE.md`, and (by default) creates a public GitHub repo for it.

## Pattern

Primitives live in the plugin → globally available from any cwd.
Workspace scaffolds are provisioned as **data** → no `.claude/` tree inside provisioned workspaces.
Plugin updates never touch your workspace data.

See [PLAN.md in Claude-Workspace-Reshaping-190426](https://github.com/danielrosehill/Claude-Workspace-Reshaping-190426) for the full pattern spec this plugin follows.

## Variants

- `wiki` — interlinked pages with category folders, SIDEBAR/TOC, and uniform page metadata.
- `resource-library` — curated resource lists (repos, tools, datasets) with an inputs→integration pipeline.
- `process-documentation` — merged process-docs + SOP-builder workspace: processes, workflows, SOPs, checklists, flowcharts, handbook.
- `experiment-report` — design → trials → analysis → reports lifecycle for experiments and evaluations.

## Cluster

Structured knowledge base primitives. Distinct from `content-writing` (prose) and `ai-engineering` (prompts). See the [Wave 2b plan](https://github.com/danielrosehill/Claude-Workspace-Reshaping-190426).

## Install

Via the danielrosehill marketplace:

```
/plugin marketplace add danielrosehill/Claude-Code-Plugins
/plugin install knowledge-documentation
```

## License

MIT.
