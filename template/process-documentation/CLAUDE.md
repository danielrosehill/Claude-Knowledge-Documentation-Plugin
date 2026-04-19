# Process Documentation Workspace

Workspace name: `{{WORKSPACE_NAME}}`
Variant: `process-documentation`
Domain: `{{DOC_DOMAIN}}`

This repository merges process documentation and SOP-builder patterns into one workspace — processes, workflows, standard operating procedures, checklists, flowcharts, and a compiled handbook.

## When to use which content type

- **`processes/`** — step-by-step procedure documents for single tasks. One file per process. Group into topic subfolders as the collection grows.
- **`workflows/`** — higher-level workflow documents that describe how multiple processes connect, decision trees, and end-to-end flows.
- **`sops/`** — formal standard operating procedures grounded in authoritative sources. Use when the procedure must cite compliance standards or external regulations.
- **`checklists/`** — markdown checkbox lists for recurring quick references.
- **`flowcharts/`** — decision flowcharts using Mermaid diagrams.
- **`handbook/`** — compiled output assembled by `/knowledge-documentation:compile-handbook`. Do not hand-edit files here.

## Authoritative Sources (SOP grounding)

If SOPs in this workspace must be grounded in external standards, list them here:

- *(edit — e.g. OSHA guidelines, NIST frameworks, ISO standards, internal policy docs)*

## Document Formats

### Process (`processes/`)

```markdown
# Process Title

Brief one-line description.

**Version:** X.Y.Z
**Last updated:** YYYY-MM-DD

## Purpose
Why this process exists.

## Prerequisites
What must be in place before starting.

## Steps
1. ...
2. ...

## Expected Outcome
What the completed process produces.

## Troubleshooting
Common failure modes and fixes.
```

### SOP (`sops/`)

```markdown
# SOP: Title

**Version:** X.Y.Z
**Last updated:** YYYY-MM-DD
**Sources:** [Authority 1](URL), [Authority 2](URL)

## Purpose
## Scope
## Prerequisites
## Procedure
## Post-Procedure
## References
```

### Checklist (`checklists/`)

```markdown
# Checklist: Title

- [ ] Item 1
- [ ] Item 2
```

### Flowchart (`flowcharts/`)

```markdown
# Flowchart: Title

​```mermaid
flowchart TD
  A[Start] --> B{Decision}
​```
```

## Workflow

1. `/knowledge-documentation:new-page "Title" --type=process` (or `sop`, `checklist`, `flowchart`, `workflow`) — scaffold with the right skeleton.
2. Draft content.
3. `/knowledge-documentation:cross-link` — link SOPs to their related processes and workflows.
4. `/knowledge-documentation:version-doc <path>` on substantive revisions.
5. `/knowledge-documentation:compile-handbook` when ready to publish a bound handbook.
