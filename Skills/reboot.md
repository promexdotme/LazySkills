# /reboot-skills

Re-ask the install questions. Rewrite `defaults.md`.

---

## Trigger

User types `/reboot-skills`.

---

## Step 1 — Confirm

Show current `defaults.md` contents inline. Then warn:

> Reboot defaults? Will overwrite `defaults.md` with new answers.
>
> 1. Yes, reboot
> 2. Cancel

Wait for explicit yes.

---

## Step 2 — One merged question per area

ONE message. Each area shows current value + lets user keep or change.

User can answer "1: keep" to keep all, or list per-question changes (e.g., "Q1: 2", "Q3: change to caveman-lite").

```
Reboot. 6 areas. Reply with numbers per question, or "1" alone to keep all.

Q1. Brevity
   Current: <show current setting>
   1. Keep
   2. Change to: caveman-lite (concise full sentences)
   3. Change to: normal English, no preamble
   Other (free text)

Q2. Grill style
   Current: <show current>
   1. Keep
   2. Change to: only when /grill typed
   3. Change to: auto-grill non-trivial work
   Other

Q3. Test policy
   Current: <show current>
   1. Keep
   2. Change to: always TDD for new features
   3. Change to: skip tests entirely unless asked
   Other

Q4. Safety / destructive ops
   Current: <show current>
   1. Keep
   2. Change to: confirm before every delete
   3. Change to: block destructive ops, give command for me to run
   Other

Q5. Scope discipline
   Current: <show current>
   1. Keep
   2. Change to: read everything I point at, don't ask
   3. Change to: ask before reading any folder
   Other

Q6. Context log
   Current: <show current>
   1. Keep
   2. Change to: only when I explicitly ask
   3. Change to: disable
   Other
```

---

## Step 3 — Stack hints (optional)

> Stack hints? Saves detection cycles. Skip if not wanted.
>
> 1. Keep current
> 2. Update — paste new values
> 3. Skip / clear

If updating, ask:
- Main language?
- Test runner command?
- Package manager?

---

## Step 4 — Location (only ask if first reboot OR user asks)

> Location?
>
> 1. Keep current (`<show current>`)
> 2. Move to global
> 3. Move to local

If global:
- Detect agent type by reading the project's instructions file (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, `.github/copilot-instructions.md`, etc.).
- Move `LazySkills/` to detected agent home:
  - Claude → `~/.claude/LazySkills/` (Windows: `%USERPROFILE%\.claude\LazySkills\`)
  - Codex → `~/.codex/LazySkills/`
  - Cursor / Copilot / unknown → ASK the user where their global instruction folder lives.
- Add a stub line in current project's instructions file:
  ```
  Read <absolute-path-to-global>/LazySkills/Start.md before responding.
  ```
- Note: local `LazySkills/` always overrides global.

If local: move/copy `LazySkills/` to current project root if not already there.

---

## Step 5 — Rewrite defaults.md

Apply all changes. Update timestamp at top of file. Confirm in one line:

> Defaults rewritten. Ready.
