# Install - First Run

Run when `defaults.md` does not exist yet, OR user explicitly asks to install LazySkills.

---

## Step 1 - Greeting

> LazySkills first-run setup. 7 quick questions. ~30 seconds.
>
> Reply "1" to accept all recommended defaults, or list per-question answers.

---

## Step 2 - Ask the 7 questions

ONE message, multi-choice format. Each independent. User can answer per-line.

```text
Q1. Brevity
   1. Caveman style - drop pleasantries, technical fragments only (Recommended)
   2. Caveman-lite - concise full sentences
   3. Normal English, just no preamble

Q2. Grill style
   1. Max grill, batched ONE message per round (Recommended)
   2. Only when I type /grill
   3. Auto-grill only for non-trivial work

Q3. Test policy
   1. Viber moderate - suggest tests when stakes are real (Recommended)
   2. Always TDD for new features
   3. Skip tests entirely unless I ask

Q4. Safety / destructive ops
   1. Trust intent inside working folder, backup before delete (Recommended)
   2. Always confirm before delete
   3. Block destructive ops, give me the command to run myself

Q5. Scope discipline
   1. Stick to active dev folder, ask if ambiguous (Recommended)
   2. Read everything I point at, don't ask
   3. Always ask before reading any folder

Q6. Context log
   1. Write/update <project>_YYYY-MM-DD_Context.md after meaningful changes (Recommended)
   2. Only when I explicitly ask
   3. Disable

Q7. Tasks / collaboration
   1. Use Collaborated_Tasks.md when present, support /tasks + collabgo (Recommended)
   2. Only use when I explicitly ask /tasks or collabgo
   3. Disable task/collab tracking
```

---

## Step 3 - Optional stack hints

> Stack hints? Saves detection cycles. Skip if not wanted.
>
> 1. Skip
> 2. Share - paste main language, test runner command, package manager

---

## Step 4 - Write defaults.md

Render answers into `defaults.md`. Confirm in one line:

> Defaults written. 1 question left.

---

## Step 5 - Ask global vs local

> Last question. Move LazySkills to a global location so every future project picks it up automatically? Or stay local to this folder?
>
> 1. Stay local (Recommended for first use - try it here, decide later)
> 2. Move to global

If global:
- Detect agent type by reading the project's instructions file (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, `.github/copilot-instructions.md`).
- Move `LazySkills/` to:
  - Claude -> `%USERPROFILE%\.claude\LazySkills\` (Windows) or `~/.claude/LazySkills/` (POSIX)
  - Codex -> `~/.codex/LazySkills/`
  - Cursor / Copilot / unknown -> ASK user for their global instruction folder.
- Add stub to current project's instructions file:
  ```text
  Read <absolute-path-to-global>/LazySkills/Start.md before responding.
  ```
- Local `LazySkills/` always overrides global if both exist.

---

## Step 6 - Done

> Ready.
