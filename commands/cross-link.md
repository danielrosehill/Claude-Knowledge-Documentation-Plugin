Detect related documents in the current knowledge-documentation workspace and insert cross-references between them.

Accepts `$ARGUMENTS` as an optional path or glob to scope the pass. Default: the whole workspace.

## Procedure

1. **Detect variant** from `CLAUDE.md`. Different variants expose different link conventions (`wiki` uses relative `../category/page.md`, `process-documentation` links SOPs to related processes, `experiment-report` links reports to their design and trials).

2. **Build a term index**: Scan each document's title, headings, and any front-matter tags. Produce a `term → canonical document path` map.

3. **Find link candidates**: For every document, search its body for mentions of other documents' titles or tag aliases. Skip mentions already inside code fences, existing links, or headings.

4. **Propose diffs**: For each candidate, show the user a unified diff inserting a link. Group diffs by source document. Ask for approval in batches.

5. **Apply approved changes** and ensure every edited document has (or gains) a `## See Also` / `## Related` section at the bottom linking to the referenced docs.

6. **Update reverse links**: If A now links to B, ensure B's `See Also` section also lists A (bidirectional by default — variant CLAUDE.md may override).

7. **Report**: Summarise inserted links, skipped ambiguous matches, and any broken references detected along the way.
