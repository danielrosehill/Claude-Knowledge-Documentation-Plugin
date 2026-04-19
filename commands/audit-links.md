Scan the current knowledge-documentation workspace for broken, stale, or inconsistent links.

Accepts `$ARGUMENTS` as an optional path to scope the audit. Default: whole workspace.

## Procedure

1. **Collect all markdown files** under the workspace (excluding `logs/`, `.git/`, and any path listed in a workspace `.auditignore`).

2. **Extract links** of these kinds:
   - Internal relative links (`../category/page.md`, `./file.md`).
   - Asset references (images, diagrams).
   - External URLs.

3. **Check internal links**:
   - Target file exists.
   - Anchor (if any) matches an actual heading in the target.
   - Path casing matches actual filesystem.

4. **Check assets**: referenced file exists under `assets/` (or the variant's asset directory).

5. **Check external URLs** (optional, skip if offline): HEAD request with a 5s timeout. Flag 4xx / 5xx / DNS failures. Do not fail the audit on a single timeout.

6. **Emit report** to `logs/link-audit-YYYY-MM-DD.md` with three sections: Broken internal, Missing assets, Unreachable external. Include file path, line number, and suggested fix when possible.

7. **Offer to auto-fix** obvious issues (casing mismatches, renamed-but-not-updated files) with user approval.
