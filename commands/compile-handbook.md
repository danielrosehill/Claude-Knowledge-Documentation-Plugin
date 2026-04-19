Assemble individual documents in the current knowledge-documentation workspace into a bound handbook or compiled guide.

Accepts `$ARGUMENTS`: optional output format (`md` default, `pdf`, `epub`) and `--scope=<category>` to limit the compile.

## Procedure

1. **Detect variant**. Not all variants produce a handbook — only these do:
   - `wiki` → `handbook/wiki-handbook.md` (all pages, grouped by category).
   - `process-documentation` → `handbook/process-handbook.md` (processes then workflows then SOPs).
   - `experiment-report` → `reports/compiled-report-YYYY-MM-DD.md` (one final report assembled from design + analysis + report per experiment).
   - `resource-library` → refuse: the README itself is the compiled artifact.

2. **Collect source documents** in the variant's canonical order. Respect `--scope` if provided.

3. **Concatenate** with:
   - A generated title page (workspace name, date, version).
   - A generated table of contents with anchor links.
   - Each source document demoted by one heading level (H1 → H2) so the handbook's own H1 is the title.
   - Page/section breaks between documents (`\n\n---\n\n`).

4. **Rewrite internal links** so cross-references inside the handbook use anchors (e.g., `#process-deploy`) rather than relative paths.

5. **Write output** to the path named in step 1.

6. **If format is `pdf` or `epub`**, pipe the markdown through `pandoc` with a sensible default template. If `pandoc` is not installed, tell the user and leave the markdown in place.

7. **Report** the output path, document count, and total word count.
