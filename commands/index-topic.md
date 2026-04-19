Generate or refresh the index / table of contents for a topic area in the current knowledge-documentation workspace.

Accepts `$ARGUMENTS` as an optional topic or category name. If omitted, scan the workspace root and rebuild the top-level index (e.g., `SIDEBAR.md`, `TOC.md`, or `README.md`'s index section, depending on the variant).

## Procedure

1. **Detect variant**: Read `CLAUDE.md` in the current workspace to determine the variant (`wiki`, `resource-library`, `process-documentation`, `experiment-report`). If no `CLAUDE.md` exists, ask the user.

2. **Discover content**: Walk the relevant content directory for the variant:
   - `wiki` → `pages/<category>/*.md`
   - `resource-library` → README sections + `for-agent/ref/`
   - `process-documentation` → `processes/`, `workflows/`, `sops/`, `checklists/`
   - `experiment-report` → `design/`, `reports/`

3. **Build entries**: For each document extract title (first `# heading`), one-line summary (first paragraph or `> summary` blockquote), category/topic, and last-modified date.

4. **Emit index**: Write or update the index file the variant expects:
   - `wiki` → regenerate `SIDEBAR.md` (nested by category) and `TOC.md` (flat alphabetical).
   - `resource-library` → update the resource list block in `README.md` between taxonomy anchors.
   - `process-documentation` → update `handbook/INDEX.md`.
   - `experiment-report` → update `reports/INDEX.md`.

5. **Preserve user content**: Only touch index regions delimited by `<!-- INDEX:START -->` / `<!-- INDEX:END -->` markers. Insert those markers if missing, preserving surrounding prose.

6. **Report**: Summarise what was added, removed, or updated.
