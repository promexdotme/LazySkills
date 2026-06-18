# LazySkills

> By **PROMEXDOTME**

**Pay less. Build more. Stop burning tokens on filler.**

LazySkills is a tiny, opinionated agent skill pack that turns ANY coding agent — Claude, Codex, Cursor, Copilot — into a faster, cheaper, more disciplined collaborator. Drop it in any project, point your agent at `Start.md`, and stop watching your wallet evaporate one *"Sure! I'd be happy to help with that..."* at a time.

---

## Why LazySkills

### Token bills are real money

Every "Certainly!", "Of course!", "Let me explain..." is paid output tokens. Multiply by every prompt, every project, every day, every team member. The bill is bigger than you think.

LazySkills strips the fluff. Same code. Same correctness. Less wallet damage.

### One question, one round trip

Most agent question loops cost 3-5 round trips of single-question pingpong. LazySkills batches every clarification into ONE message with multi-choice answers. One round trip. Every time. Less context spent, less time burned.

### Default safe, never destructive

Auto-backups before any delete. Scope discipline so massive sibling folders never get pulled into context. Selection warnings the moment a choice has a known cheaper or smarter alternative.

### Self-documenting

Every meaningful change writes a dated context log. The next AI session — yours, your teammate's, future-you's — starts oriented in seconds instead of re-exploring from scratch. That's tokens saved on every restart.

---

## Slogans

- **Pay less. Build more.**
- **Filler costs money. Caveman doesn't.**
- **One question, one answer, one round trip.**
- **Lazy on tokens. Sharp on code.**
- **Drop it in. Save 70% per session.**
- **Skills that pay rent.**
- **Every word costs. Spend wisely.**

---

## Skills

### Always on (no command needed)

| Rule | What it does | Token impact |
|---|---|---|
| **Caveman mode** | Drops articles, filler, pleasantries. Technical fragments only. | ~75% smaller responses |
| **Selection warnings** | One-line note when a choice has a smarter or cheaper alternative. | Saves wasted iteration |
| **Elaborate on demand** | No "why" by default. Only on `Why?` / `Explain`. | Skips unread paragraphs |
| **Context log** | Writes a dated handoff doc per project so the next session lands oriented. | Saves re-explore cost |
| **Task/progress file** | Reads/updates `Collaborated_Tasks.md` when present. | Keeps handoff + multi-AI work aligned |
| **Scope discipline** | Only loads folders pointed at active dev work. Asks if ambiguous. | Skips reading 10k irrelevant files |
| **Backup-before-delete** | Auto `cp` before any `rm`. Git? Trust git. No git? Dated backup folder. | Saves recovery cost |

### On demand

| Command | What it does |
|---|---|
| `/grill` | One batched multi-choice message before non-trivial work. Aligns intent in one round trip. |
| `/diagnose` | Feedback-loop-first debugging. Build the loop, then fix the bug. |
| `/zoom` | One-layer-up map of relevant modules + callers. Skip the deep dive. |
| `/graphify` | Reads `graphify-out/` when present, or recommends official Graphify for larger-than-small codebases. |
| `/tasks`, `collabgo` | Maintains `Collaborated_Tasks.md` and coordinates Lead/Follower work across Codex, Gemini, and Claude. |
| `/prototype` | Throwaway code that answers ONE question. Deleted or absorbed when done. |
| `/reboot-skills` | Re-asks the install questions, rewrites your defaults. |

---

## Install

1. Drop the `LazySkills/` folder anywhere — your project, a sibling folder, or your agent home (`~/.claude/`, `~/.codex/`, etc.).
2. In your project's instructions file (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, `.github/copilot-instructions.md`, etc.), add one line:

   ```
   Read LazySkills/Start.md before responding.
   ```

   Or for a global install, point at the absolute path.

3. First time you talk to your agent, it will run the install questionnaire (see `Skills/install.md`) and write your `defaults.md`. Takes ~30 seconds.

4. After defaults are captured, the agent asks once whether to move LazySkills to a global location so every future project picks it up automatically. Local always overrides global.

5. Use `/reboot-skills` any time you want to change defaults.

---

## What's in the box

```
LazySkills/
├── README.md            ← you're here
├── Start.md             ← entry point. Agent reads this first.
├── defaults.md          ← burnt-in answers. Edit by hand or /reboot-skills.
└── Skills/
    ├── always-on.md     ← the 7 rules applied every response
    ├── grill.md         ← /grill
    ├── diagnose.md      ← /diagnose
    ├── zoom-out.md      ← /zoom
    ├── graphify.md      ← /graphify
    ├── tasks-collab.md  ← /tasks + collabgo
    ├── prototype.md     ← /prototype
    ├── tests.md         ← test policy (read when relevant)
    ├── reboot.md        ← /reboot-skills
    └── install.md       ← first-run questionnaire
```

Total always-on payload: under 1000 tokens. Everything else loads on trigger only.

---

## Author

**PROMEXDOTME**

Yours to use, fork, adapt. No attribution required, but appreciated.
