---
name: new-workspace
description: Provision a new knowledge-documentation workspace on disk. Use when the user wants to start a wiki, curated resource library, process/SOP documentation set, or experiment report workspace. Accepts a workspace name and a variant. Scaffolds the workspace, personalises CLAUDE.md from the user's global memory, and (by default) creates a GitHub repo.
disable-model-invocation: true
allowed-tools: Bash(mkdir *), Bash(cp *), Bash(cat *), Bash(git init *), Bash(git add *), Bash(git commit *), Bash(gh repo create *), Bash(gh auth status), Bash(git push *), Read
---

# Provision Knowledge-Documentation Workspace

Creates a new workspace for structured knowledge documentation. This plugin's commands (`/knowledge-documentation:index-topic`, `/knowledge-documentation:cross-link`, etc.) are globally available once installed — this skill only provisions the **data scaffold** (CLAUDE.md, content directories, README) that those commands read from and write to.

## Arguments

`$ARGUMENTS` is parsed as:

- **First positional**: workspace name (kebab-case, used as directory and GitHub repo name). Required.
- **Second positional** (optional): target parent path. Defaults to `~/repos/github/my-repos`.
- **`--variant=<wiki|resource-library|process-documentation|experiment-report>`** (optional): which scaffold to copy. Default: `wiki`.
- **`--local-only`** (optional): skip GitHub repo creation and push. Default: create a public GitHub repo and push.
- **`--private`** (optional): create the GitHub repo as private. Default: public.

### Examples

```
/knowledge-documentation:new-workspace home-network-wiki
/knowledge-documentation:new-workspace ai-tools-list --variant=resource-library
/knowledge-documentation:new-workspace ops-sops --variant=process-documentation
/knowledge-documentation:new-workspace prompt-length-study --variant=experiment-report --private
```

## Procedure

### 1. Parse arguments

Extract workspace name, target parent path, variant, and flags from `$ARGUMENTS`. If the workspace name is missing, ask the user for it before proceeding.

### 2. Resolve the scaffold path

The bundled scaffold lives at `${CLAUDE_SKILL_DIR}/../../template/<variant>/`. Confirm it exists. If the variant isn't one of `wiki`, `resource-library`, `process-documentation`, `experiment-report`, tell the user which variants are available.

### 3. Read ambient facts

Read `~/.claude/CLAUDE.md` if it exists. Extract OS, locale, timezone, and user identity facts. These will personalise the workspace's CLAUDE.md at step 6.

### 4. Create the workspace directory

```bash
mkdir -p <target-parent>/<workspace-name>
cp -r ${CLAUDE_SKILL_DIR}/../../template/<variant>/. <target-parent>/<workspace-name>/
```

Do **not** copy any `.claude/` tree. The plugin's primitives are global.

### 5. Personalise CLAUDE.md

Open the new workspace's `CLAUDE.md` and:

- Replace any placeholder identity with the facts from step 3.
- Add a short header noting the workspace name and variant.
- If ambient facts include OS/locale, embed them so downstream commands can skip re-asking.

### 6. Prompt for variant-specific facts

Ask the user only for facts this plugin can't infer:

- **wiki**: the wiki's subject/scope (write into `CLAUDE.md` as `WIKI_SCOPE`).
- **resource-library**: the curation topic (write as `RESOURCE_TOPIC`).
- **process-documentation**: the domain (e.g., "deployment ops", "incident response") — write as `DOC_DOMAIN`. Ask if authoritative sources should be listed (SOP-style grounding).
- **experiment-report**: the experiment series name / research area (write as `EXPERIMENT_FOCUS`).

### 7. Initialise git and (optionally) publish

```bash
cd <target-parent>/<workspace-name>
git init
git add .
git commit -m "Initial workspace from knowledge-documentation plugin"
```

Unless `--local-only` is set:

```bash
gh repo create <workspace-name> --<public|private> --source=. --push
```

Use `--public` by default, `--private` if flag was passed.

### 8. Print next steps

Tell the user:

- Workspace path.
- Variant chosen.
- Which plugin commands apply next (e.g., `/knowledge-documentation:new-page` to add content, then `/knowledge-documentation:index-topic` to refresh the index).
- Reminder that the workspace is **data** — they can delete/move it freely without losing the plugin's commands.

## Notes

- The scaffold path must be resolved via `${CLAUDE_SKILL_DIR}/../../template/` (not `${CLAUDE_PLUGIN_ROOT}` — that variable isn't exported in skill bash injection, only in hooks/MCP).
- Never copy `.claude/commands/`, `.claude/agents/`, or `.claude/skills/` into the new workspace. If the user wants workspace-local overrides, they can add them manually later.
- Don't hard-code any personal paths or identifiers here — everything comes from user memory or prompts.
