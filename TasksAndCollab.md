# Tasks and Collaboration

Use this guide when a project needs persistent task tracking or multiple AI agents working in the same codebase.

Main skill: [Skills/tasks-collab.md](Skills/tasks-collab.md)

Shared project file: `Collaborated_Tasks.md`

## What This Adds

- One task list for active work.
- Assignment in the same row as each task.
- Default assignee `None`, meaning the active AI may work it unless someone is named.
- Lead/Follower collaboration mode for Codex, Gemini, and Claude.
- File ownership boundaries to avoid overlapping edits.
- Lead prompts/remarks in the task row, with longer details under each task.
- Completion log for progress, blockers, commands, and changed files.

## Recommended `Collaborated_Tasks.md` Template

Create this file in the active project root when task tracking or AI collaboration is useful:

```md
# Collaborated Tasks

## Status

Lead: None
Current goal: None
Known agents: Codex, Gemini, Claude
Last updated by: None
Last updated: None

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
| T001 | None | Lead | Todo | High | TBD | Define current work | Add exact scope before coding. | TBD |

## Task Details

### T001

Context:
- TBD

Acceptance:
- TBD

Do not touch:
- TBD

Commands:
- TBD

## Completion Log

### TBD - None

Status:
Files changed:
Commands run:
Result:
Blockers:
```

## Commands

`/tasks`

Read or create `Collaborated_Tasks.md`, update task rows, and use it for progress tracking.

`collabgo lead`

Act as Lead. Split work into non-overlapping tasks and assign rows to Codex, Gemini, Claude, or None.

`collabgo follower`

Act as Follower. Read `Collaborated_Tasks.md`, find rows assigned to the current agent, and work only those rows.

`collabgo follow as Gemini`

Act as Gemini Follower and work only rows assigned to Gemini.

## Assignment Examples

| ID | Assigned To | Role | Status | Priority | Files/Area | Task | Lead Prompt / Remarks | Updated |
|---|---|---|---|---|---|---|---|---|
| T001 | Codex | Lead | In progress | High | `app/Http/Controllers/*` | Refactor controller flow | Keep route names stable. | 2026-06-17 |
| T002 | Gemini | Follower | Todo | Medium | `resources/views/orders/*` | Update Blade views | Do not touch controller files. | 2026-06-17 |
| T003 | Claude | Follower | Todo | Medium | `tests/Feature/orders/*` | Add regression tests | Match Codex route behavior after T001. | 2026-06-17 |
| T004 | None | Follower | Todo | Low | `docs/*` | Update docs after implementation | Active AI may take this. | 2026-06-17 |

## Safety

If two tasks point at the same file or logic path, stop and mark one task `Blocked` unless Lead explicitly assigned the overlap.

Followers should never expand scope. Lead coordinates; Followers execute.
