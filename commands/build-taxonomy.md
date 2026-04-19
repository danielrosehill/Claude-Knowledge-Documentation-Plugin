Analyse content in the current knowledge-documentation workspace and propose or apply a category taxonomy.

Accepts `$ARGUMENTS`: `--apply` to actually move files; default is dry-run (propose only).

## Procedure

1. **Detect variant** from `CLAUDE.md`. Taxonomy shape differs:
   - `wiki` → category folders under `pages/`.
   - `resource-library` → top-level sections in `README.md`.
   - `process-documentation` → topic folders under `processes/` and `sops/`.
   - `experiment-report` → experiment series folders under `design/` and `trials/`.

2. **Survey content**: For each document collect title, headings, frontmatter tags, and a short sample of body text. Cluster by topical similarity.

3. **Propose taxonomy**: Generate a category tree with:
   - Suggested category names (kebab-case, noun phrases).
   - Each document mapped to exactly one primary category (plus optional secondary tags).
   - A `CHANGES.md` preview listing moves/renames.

4. **Present to user**: Show the proposed tree, expected moves, and rationale. Ask for approval or revisions.

5. **Apply (only if `--apply`)**:
   - Create new category directories.
   - Move files with `git mv` to preserve history.
   - Update internal links to reflect new paths.
   - Run `/knowledge-documentation:index-topic` afterwards to refresh indices.

6. **Log** the taxonomy change to `logs/taxonomy-YYYY-MM-DD.md` (create `logs/` if absent) with the before/after tree.
