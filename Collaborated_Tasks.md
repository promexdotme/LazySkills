# Collaborated Tasks

## Status

Lead: Codex
Current goal: Publish current local LazySkills updates to GitHub
Known agents: Codex, Gemini, Claude
Last updated by: Codex
Last updated: 2026-08-27

## Global Rules

- Read this file before doing work.
- Use the task table as the source of truth.
- `Assigned To = None` means active AI unless a named agent is specified.
- Do not edit files/areas assigned to another active agent.
- No overlapping edits unless Lead explicitly assigns the overlap.
- If blocked, update the task row and add a completion log note instead of guessing.
- After finishing, update status, files changed, commands run, result, and blockers.
- Do not touch secrets, `.env`, production config, payment keys, or credentials.
- Run only safe commands unless the user explicitly approves risk.

## Task List

| ID | Assigned To | Role | Status | Priority | Files/Area | Task | Lead Prompt / Remarks | Updated |
|---|---|---|---|---|---|---|---|---|
| T001 | Codex | Lead | Done | High | `Skills/tasks-collab.md`, `TasksAndCollab.md`, `Start.md`, `README.md`, `Skills/always-on.md`, `Skills/install.md`, `defaults.md` | Add combined Tasks + Collab skill | Use same shared task list for normal progress and multi-AI coordination. | 2026-06-17 |
| T002 | Codex | Lead | Done | High | `GraphifyAddForLargeSets.md`, `Skills/graphify.md` | Publish newer local Graphify commands | Preserve local command fixes while integrating two newer remote commits, then push and verify `main`. | 2026-08-27 |

## Task Details

### T001

Context:
- User wanted one major skill that covers updateable task tracking and multi-AI collaboration.
- Shared file must be `Collaborated_Tasks.md`.
- Assignment belongs in the same row. `None` means active AI unless a named agent is specified.
- Known agents: Codex, Gemini, Claude.
- No overlapping edits unless Lead assigns them.

Acceptance:
- Add Markdown skill for `/tasks` and `collabgo`.
- Add guide/template docs.
- Wire into Start and README.
- Update always-on/default/install behavior.
- Remove `collab.txt`.

Do not touch:
- Secrets or external project config.

Commands:
- Read docs.
- Apply Markdown edits.
- Verify status/diff.

## Completion Log

### 2026-08-27 - Codex

Status: Done
Files changed: `GraphifyAddForLargeSets.md`, `Skills/graphify.md`, `Collaborated_Tasks.md`, `LazySkills_2026-08-27_Context.md`
Commands run: `git fetch`, `git diff`, `git add`, `git commit`, `git rebase`, `git push`, `git ls-remote`
Result: Integrated remote Graphify/collaboration commits, preserved newer local Graphify commands, and pushed verified `main` update.
Blockers: None

### 2026-06-17 - Codex

Status: Done
Files changed: `Skills/tasks-collab.md`, `TasksAndCollab.md`, `Start.md`, `README.md`, `Skills/always-on.md`, `Skills/install.md`, `defaults.md`, `Collaborated_Tasks.md`
Commands run: `Get-Content`, `git status --short`
Result: Added unified task/progress and collaboration workflow. Removed `collab.txt`.
Blockers: None
