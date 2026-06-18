# /tasks + /collabgo

Trigger: user types `/tasks`, `tasks`, `progress`, `task list`, `collaboratewithotherai`, `collabgo`, `collab lead`, `collab follower`, `collab follow as Codex/Gemini/Claude`, or asks multiple AIs to work together.

Shared file: `Collaborated_Tasks.md` in the active project root.

Known agents: `Codex`, `Gemini`, `Claude`.

Roles: `Lead`, `Follower`.

Core rule: no overlapping edits unless Lead explicitly assigns the overlap.

## Purpose

Use one updateable Markdown file for project tasks, progress, ownership, and multi-agent coordination.

This skill replaces scattered notes. It keeps a single task table with assignment, status, file boundaries, and Lead remarks/prompts.

## Assignment Rule

Use the `Assigned To` column near the start of each row so agents can quickly find their work.

- `None` means the active AI may work it unless the user says otherwise.
- `Codex`, `Gemini`, or `Claude` means only that agent should work it.
- `Lead` may edit task rows, assign work, clarify boundaries, and set prompts/remarks.
- `Follower` works only rows assigned to its agent name, plus rows assigned to `None` only if the Lead or user explicitly says to take unassigned work.

## Shared File Format

If `Collaborated_Tasks.md` does not exist, create it with this structure:

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

## Normal Task Mode

When user asks for tasks/progress:

1. Read `Collaborated_Tasks.md` if it exists.
2. If missing, create it only when task tracking is useful or user asked for it.
3. Add or update rows instead of writing separate TODO files.
4. Keep task IDs stable: `T001`, `T002`, `T003`.
5. Put assignee in `Assigned To`.
6. Put short Lead/user instructions in `Lead Prompt / Remarks`.
7. Put longer context under `Task Details`.
8. Update `Completion Log` after meaningful work.

Status values:

- `Todo`
- `In progress`
- `Blocked`
- `Review`
- `Done`
- `Cancelled`

## Collaboration Activation

When user says `collaboratewithotherai` or `collabgo`, determine role:

- If user says `lead`, act as Lead.
- If user says `follower`, `follow`, or `follow as <agent>`, act as Follower.
- If role is missing, ask once: `Lead or Follower?`

Examples:

```text
collabgo lead
collabgo follower
collab follow as Gemini
collabgo Claude follower
collaboratewithotherai Codex lead
```

## Lead Mode

Lead responsibilities:

1. Read existing `Collaborated_Tasks.md`.
2. Set `Lead` in Status.
3. Break work into non-overlapping tasks.
4. Assign each row to `Codex`, `Gemini`, `Claude`, or `None`.
5. Set `Role` per row: `Lead` or `Follower`.
6. Set file/folder boundaries in `Files/Area`.
7. Put direct agent instructions in `Lead Prompt / Remarks`.
8. Add longer instructions under `Task Details` when needed.
9. Do not assign two active agents to the same file unless one is review-only.
10. If overlap is risky, mark one row `Blocked` and explain the conflict.

Lead may work rows assigned to itself and may update any task metadata.

## Follower Mode

Follower responsibilities:

1. Read `Collaborated_Tasks.md`.
2. Determine active agent name: Codex, Gemini, or Claude.
3. Find rows where `Assigned To` matches that agent.
4. If no matching row exists, do not work. Say: `No assigned task found for this agent.`
5. Work only on assigned `Files/Area`.
6. Do not modify another agent's files, rows, or task details.
7. Update only own task rows, own task details, and Completion Log.

Follower must stop if:

- No task is assigned to this agent.
- Assigned files overlap another active agent.
- Task needs secrets, production credentials, destructive commands, or vague risky scope.
- Required files are missing.

## Conflict Rule

Before editing, check:

> Could this overlap with another active agent's task?

If yes:

1. Do not edit.
2. Mark own row `Blocked`.
3. Add conflict note to `Lead Prompt / Remarks` or task details.
4. Add Completion Log entry.
5. Suggest a safer split.

## Output Style

After work, respond briefly:

- role used
- task ID/status
- files changed
- commands run
- blocker or next AI action

No long explanation unless user asks.
