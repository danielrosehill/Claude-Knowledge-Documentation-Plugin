# Resource Library Workspace

Workspace name: `{{WORKSPACE_NAME}}`
Variant: `resource-library`
Topic: `{{RESOURCE_TOPIC}}`

This repository is a curated resource list — repositories, tools, datasets, papers, or services — organised by taxonomy rather than popularity.

## Philosophy

These lists prioritise organised taxonomy over popularity metrics. The goal is mapping an ecosystem into logical clusters for orderly exploration, not chasing stars.

## Directory Layout

- `README.md` — the published resource list. Primary output.
- `for-agent/inputs/to-add/` — drop new resource notes here before integration.
- `for-agent/inputs/processed/` — resources already integrated into `README.md`.
- `for-agent/ref/` — reference material (category definitions, inclusion criteria, excluded resources).

## Resource Entry Format

Each resource in `README.md` should include:

```markdown
- **[Name](URL)** — one-line description. `tags: tag1, tag2` — optional metrics (stars, last commit).
```

Group entries under category headings (H2) and, where needed, subcategory headings (H3). Maintain alphabetical order within each group unless a curated ordering is defined in `for-agent/ref/ordering.md`.

## Workflow

1. Drop new candidates into `for-agent/inputs/to-add/` as short markdown stubs.
2. `/knowledge-documentation:build-taxonomy` — propose/refresh the category tree.
3. `/knowledge-documentation:index-topic` — regenerate the resource sections of `README.md` between `<!-- INDEX:START -->` / `<!-- INDEX:END -->` markers.
4. `/knowledge-documentation:audit-links` — periodically verify all resource URLs still resolve.

## Inclusion Criteria

Defined in `for-agent/ref/inclusion.md`. Edit that file to tune what gets accepted.
