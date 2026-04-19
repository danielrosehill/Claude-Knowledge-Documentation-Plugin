# {{WORKSPACE_NAME}}

A structured wiki workspace maintained with the [knowledge-documentation Claude Code plugin](https://github.com/danielrosehill/Claude-Knowledge-Documentation-Plugin).

## Structure

- `pages/` — wiki pages grouped by category.
- `assets/` — images, diagrams, attachments.
- `SIDEBAR.md` — auto-generated sidebar navigation.
- `TOC.md` — auto-generated flat table of contents.

## Working with this wiki

Install the plugin and use:

- `/knowledge-documentation:new-page "Title" --category=<name>`
- `/knowledge-documentation:index-topic` — refresh `SIDEBAR.md` / `TOC.md`
- `/knowledge-documentation:cross-link` — wire up related pages
- `/knowledge-documentation:audit-links` — find broken links
- `/knowledge-documentation:compile-handbook` — bind the wiki into a single handbook
