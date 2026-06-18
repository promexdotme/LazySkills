# LazySkills Defaults

Burnt-in answers. Skills read these instead of re-asking per project. Edit by hand or run `/reboot-skills`.

---

## 1. Brevity

Caveman style. Drop articles, filler, pleasantries. Technical fragments only.

Allowed: 1-2 line summary at end IF response was big or it answered a question.

Suspend caveman temporarily for: destructive-action warnings, security notes, multi-step sequences where order matters.

## 2. Grill style

Max grill, ONE message per round. Multi-choice format (label + 1-line description). Variable option count — minimum needed. No padding to 3-4 options. Always required answers.

## 3. Test policy

Moderate / viber-friendly. No forced TDD. Suggest tests when risk is real (auth, payments, migrations, data-loss paths). Otherwise skip. See `Skills/tests.md` for full rule.

## 4. Safety / destructive ops

Trust intent inside working folder. BEFORE any file or folder delete:

- **Git repo present** → rely on git. Tell user the recovery command. No separate backup.
- **No git** → copy target to `.skills-backup/YYYY-MM-DD_HH-MM-SS/<original-path>/` first.
  - POSIX: `cp -R <target> .skills-backup/<timestamp>/<path>/`
  - Windows: `Copy-Item -Recurse <target> .skills-backup\<timestamp>\<path>\`
- If `.skills-backup/` exists in a git project → auto-add `.skills-backup/` to `.gitignore`.

Disk usage: irrelevant. Backups can be deleted later.

## 5. Scope

Only load folders pointed at as active dev target. If ambiguous (monorepo, sibling addons, `vendor/`, `node_modules/`, mixed-language repo), ask once before reading.

## 6. Context log

After meaningful changes, write or update `<project-name>_YYYY-MM-DD_Context.md` in project root. Same-day work updates the existing file. Sections: features added, files touched, behavior decisions, limitations, future notes.

## 7. Tasks / collaboration

If `Collaborated_Tasks.md` exists in the active project root, read it before non-trivial work and update relevant rows after meaningful progress.

Default assignment: `Assigned To = None` means active AI unless a named agent is specified. Use `Codex`, `Gemini`, or `Claude` for specific agent assignments.

Use `collabgo` or `collaboratewithotherai` for Lead/Follower multi-AI coordination. No overlapping edits unless Lead explicitly assigns them.

## 8. Install location

Local

(Set during install / reboot. `Local` = LazySkills lives in this project. `Global` = lives in agent home and all projects pick it up.)

## 9. Stack hints (optional)

Filled during install if user shared. Saves detection cycles.

- Main language: 
- Test runner command: 
- Package manager: 
- Other:
