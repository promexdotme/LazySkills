# LazySkills 2026-06-17 Context

## Features added

- Added unified task/progress and multi-AI collaboration workflow.
- Added `/tasks` and `collabgo` behavior.
- Added `Collaborated_Tasks.md` shared task file format with assignment, status, file boundaries, and Lead remarks/prompts.
- Added Lead/Follower rules for Codex, Gemini, and Claude.
- Added task/progress behavior to always-on rules and defaults.

## Files touched

- `Skills/tasks-collab.md`
- `TasksAndCollab.md`
- `Collaborated_Tasks.md`
- `Start.md`
- `README.md`
- `Skills/always-on.md`
- `Skills/install.md`
- `defaults.md`
- `collab.txt`

## Behavior decisions

- `Assigned To = None` means the active AI may work the task unless a named agent is specified.
- Named assignees are `Codex`, `Gemini`, and `Claude`.
- `collabgo lead` creates or updates the shared task list and assigns non-overlapping work.
- `collabgo follower` reads the same task list and works only rows assigned to that agent.
- No overlapping edits are allowed unless Lead explicitly assigns the overlap.
- Lead prompts and remarks live in the task row, with longer details under `Task Details`.

## Limitations

- The shared task file is Markdown, so agents must edit carefully to avoid table formatting drift.
- Followers need the user or environment to identify which agent name they are acting as when ambiguous.

## Future notes

- Consider adding a compact task status legend to `Start.md` if users ask for visible task states often.
- Consider adding examples for review-only overlapping assignments.
