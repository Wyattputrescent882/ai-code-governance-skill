---
name: ai-code-governance
description: Governance workflow for AI coding agents such as Codex, Claude Code, Cursor, and Copilot Workspace. Use when implementing features, fixing bugs, refactoring, reviewing AI-generated code, adopting governance in an existing project, creating or updating AGENTS.md, CLAUDE.md, CODEX.md, architecture docs, project indexes, dependency policies, and coding standards. Enforces search-before-write, reuse of existing components/hooks/services/stores/utils/types, dependency control, small maintainable changes, verification, and clear change reports.
---

# AI Code Governance

Use this skill to turn an AI coding agent into a project maintainer: inspect first, reuse existing architecture, make the smallest useful change, verify it, and leave the project easier to continue.

This skill applies both when starting a new project and when joining an existing project midstream.

## Choose The Mode

- **Project adoption**: Use when the user asks to add, install, initialize, or improve AI coding governance for a repo, including Codex or Claude Code setup.
- **Engineering task**: Use when the user asks for feature work, bug fixes, refactors, reviews, dependency changes, build/tooling changes, or cleanup of AI-generated code.
- If both apply, do project adoption first, then do the engineering task.

## Project Adoption Workflow

When adding this skill to an existing project, do not assume the templates describe reality. Build the rules from the actual codebase.

1. Inspect the current repo: `README`, package/build config, test config, source tree, existing `AGENTS.md`, `CLAUDE.md`, `CODEX.md`, and `docs/`.
2. Identify authoritative implementations: request/client layer, routing, state, UI primitives, hooks/composables, services, utilities, types, design tokens, tests, and scripts.
3. Create or update project rules:
   - `AGENTS.md`: shared coding-agent rules.
   - `CLAUDE.md`: Claude Code entry point; point to or import `AGENTS.md`.
   - `CODEX.md`: Codex entry point; point to `AGENTS.md`.
   - `docs/architecture.md`: architecture contract and layer boundaries.
   - `docs/project-index.md`: real reusable modules and ownership map.
   - `docs/dependency-policy.md`: approved dependencies and prohibited duplicates.
   - `docs/coding-standards.md`: project-specific coding rules.
   - `docs/agent-workflows.md`: task, review, refactor, and dependency workflows.
4. Replace template examples with real project paths. If a fact is unknown, mark it as `TBD` or `needs confirmation`; never present a guessed path as authoritative.
5. If governance files already exist, merge conservatively. Preserve project-specific rules and remove only clear duplication.
6. Recommend quality scripts, but do not modify `package.json` or lockfiles unless the user approves the dependency/tooling change.
7. End with an adoption report: files created/updated, discovered reusable modules, unresolved unknowns, recommended next checks.

For Claude Code project-level installation, the same skill can also live at `.claude/skills/ai-code-governance/SKILL.md`. For personal Claude Code use, install it at `~/.claude/skills/ai-code-governance/SKILL.md`.

## Engineering Task Workflow

1. Read available project rules: `AGENTS.md`, `CLAUDE.md`, `CODEX.md`, `docs/architecture.md`, `docs/project-index.md`, `docs/dependency-policy.md`, `docs/coding-standards.md`, and `docs/agent-workflows.md`.
2. Search before writing. Prefer `rg`/`rg --files` and inspect existing components, hooks/composables, services, stores, utils, types, styles, tests, and scripts.
3. Form a concise implementation plan that names the files to reuse and change. If the user explicitly asks for plan-only or approval-first work, stop after the plan. Otherwise proceed with the smallest safe implementation.
4. Reuse or extend existing modules. Add a new module only when there is no suitable owner and the new file has one clear responsibility.
5. Gate dependency changes. Before modifying `package.json` or lockfiles, explain why existing tools are insufficient and ask for confirmation.
6. Keep the change scoped. Do not modify unrelated files, rewrite large modules, or create parallel implementations.
7. Verify with the project's available commands. Common checks include `npm run lint`, `npm run typecheck`, `npm run test`, `npm run format`, `npm run dupcheck`, `npm run unused`, and `npm run check`.
8. Update governance docs when the change creates or removes an authoritative reusable module, public workflow, dependency decision, or architecture rule.
9. End with a change report: what changed, what was reused, dependency impact, verification results, and remaining risks.

## Non-Negotiables

- Do not duplicate an existing component, hook/composable, service, store, utility, type, request wrapper, date library, validation layer, modal/button/loading/empty component, or state-management approach.
- Do not add unapproved dependencies.
- Do not keep mock, temporary, fallback, compatibility, or experimental code unless the user explicitly asked for it.
- Do not bypass checks by weakening lint, type, or test rules.
- Do not claim a command passed if it was not run or does not exist.
- Do not hardcode style values when the project has design tokens or a style system.

## Search Checklist

Search using task-specific names plus these generic terms:

```text
component
hook
composable
service
store
utils
helper
type
interface
request
client
api
format
validate
modal
button
loading
empty
error
storage
token
```

## Output Shapes

For approval-first work, use this plan shape:

```md
## Understanding
...

## Existing Implementation
- ...

## Reuse Plan
- ...

## Change Plan
- Modify: ...
- Add: ...
- Remove: ...

## Dependency Impact
No new dependencies. / Needs approval because ...

## Verification
- ...

## Risks
- ...
```

For completed work, use this summary shape:

```md
## Summary
...

## Files
- Modified: ...
- Added: ...
- Removed: ...

## Reuse
...

## Deduplication
...

## Dependencies
...

## Verification
- ...

## Risks / Next Steps
...
```

## Supporting Resources

- `templates/`: starter project governance files for AGENTS, Claude Code, Codex, and docs.
- `prompts/`: reusable prompts for preflight, implementation, refactor, and review workflows.
- `snippets/`: optional quality-check config examples.
