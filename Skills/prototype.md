# /prototype

Throwaway code that answers ONE question. Deleted or absorbed when the answer is found.

---

## Trigger

User says `/prototype`, "prototype this", "let me play with it", "try a few designs", "sanity-check this state machine".

---

## Pick the branch

What's the question?

- **"Does this logic / state model feel right?"** → tiny terminal app or unit-test-style harness that pushes the state machine through hard cases.
- **"What should this look like?"** → 2-4 radically different UI variations on a single route, switchable via URL param + a floating bottom bar.

If ambiguous and user unreachable: pick by surrounding code (backend module → logic; page/component → UI). State the assumption at top of the prototype file.

---

## Rules (both branches)

1. **Throwaway from day one.** Name so a casual reader sees it's a prototype. Locate near the real code it's prototyping for. Don't invent new top-level structure — follow the project's existing routing / module convention.
2. **One command to run.** Use whatever the project's task runner supports.
3. **No persistence.** State in memory unless persistence IS the question being tested. If DB is needed, use a scratch DB or local file with a clear "PROTOTYPE — wipe me" name.
4. **No tests, no error handling, no abstractions.** Skip the polish. Point is to learn fast and delete.
5. **Surface the state.** After every action (logic) or on every variant switch (UI), print or render the full relevant state.
6. **Delete or absorb when done.** When the prototype has answered its question, either delete it or fold the validated decision into the real code. Don't leave it rotting.

---

## When done

The ANSWER is the only thing worth keeping. Capture it durably:

- Commit message
- ADR
- Context log (`<project>_YYYY-MM-DD_Context.md`) under "Behavior decisions"
- `NOTES.md` next to the prototype if no other home fits

Then delete the prototype.

If user is around, that capture is a quick conversation. If not, leave a placeholder so they (or you, next session) can fill in the verdict before deleting.
