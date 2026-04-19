Scaffold a new document in the current knowledge-documentation workspace, pre-filled with the variant's required frontmatter.

Accepts `$ARGUMENTS`: the page title (required) and optional `--category=<name>` / `--type=<process|workflow|sop|checklist|flowchart|design|trial|report>` (variant-dependent).

## Procedure

1. **Detect variant** from workspace `CLAUDE.md`. Refuse to proceed if not in a knowledge-documentation workspace.

2. **Resolve target path** by variant:
   - `wiki` → `pages/<category>/<kebab-title>.md` (ask for category if missing).
   - `resource-library` → stage under `for-agent/inputs/to-add/<kebab-title>.md`.
   - `process-documentation` → `<type>s/<kebab-title>.md` (process, workflow, sop, checklist, flowchart).
   - `experiment-report` → `<type>/<kebab-title>.md` (design, trial, report) or `trials/<experiment>/run-NN/` for a trial run.

3. **Generate the file** with the variant's canonical skeleton:
   - YAML frontmatter or metadata header with title, category/type, date, version `0.1.0`.
   - Section headings required by that variant's CLAUDE.md format block.
   - A placeholder `> TODO: summary` at the top.

4. **If the parent directory is new**, create it and add a `.gitkeep` to any empty siblings the variant expects.

5. **Open the file's path** for the user to start editing. Do not write speculative content — only the required skeleton.

6. **Remind** the user to run `/knowledge-documentation:index-topic` and `/knowledge-documentation:cross-link` once content is drafted.
