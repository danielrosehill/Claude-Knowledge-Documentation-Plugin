Version-stamp a document and update its history footer.

Accepts `$ARGUMENTS`: the path to the document to version. Optional `--bump=major|minor|patch` (default `minor`) and `--note="..."` to record the change rationale.

## Procedure

1. **Read the document**. Locate its version metadata. Expected forms (in order of precedence):
   - YAML frontmatter `version:` field.
   - A `**Version:** X.Y.Z` line near the top.
   - A `## History` section at the bottom with dated entries.

2. **If no version metadata exists**, initialise it:
   - Add a metadata block appropriate to the variant (frontmatter for `wiki`, inline for `process-documentation`, etc.).
   - Set version to `1.0.0`.
   - Create a `## History` section.

3. **Bump the version** according to `--bump`. Default `minor`.

4. **Update `Last updated`** to today's date (ISO `YYYY-MM-DD`).

5. **Append a history entry**:
   ```
   - YYYY-MM-DD — vX.Y.Z — <note or summary of changes since last version>
   ```
   If `--note` was not supplied, compare against the last committed version (via `git diff` on the file since its previous version bump) and generate a one-line summary.

6. **Report** the new version and path to the updated file. Do not commit automatically — leave that to the user or a wrapping workflow.
