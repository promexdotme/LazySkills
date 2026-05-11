# /grill

Pre-implementation alignment. ONE message of batched multi-choice questions.

---

## Trigger

- User types `/grill`, "grill me", "stress-test this plan", "ask me questions before you build."
- Optionally: agent uses `/grill` spontaneously when about to make a non-trivial decision and user direction is genuinely ambiguous.

## Format

For each unresolved decision, present:

```
Q<n>: <one clear question>
1. <Recommended option>     — <one-line description>
2. <Alternative>             — <one-line description>
[3. <Other alternative>      — <one-line description>]
[Other (free text)]
```

Rules for option count:
- 1 option = yes/no implied. Don't pad.
- 2 options = most common. Use these.
- 3 options = only when there's a genuinely-third path.
- "Other (free text)" = always allow it, but only when freeform input is realistic.

Mark recommended option `(Recommended)`. Always required answers — no optionals.

## Process

1. List ALL questions in ONE message. Numbered.
2. Recommend the answer you would pick for each.
3. Wait for user reply.
4. Resolve dependencies — next round can ask deeper questions only after first round answered.
5. Stop when shared understanding reached. Don't grill for the sake of grilling.

## Code-first heuristic

If a question can be answered by reading the codebase, READ instead of asking. Never burn a user round trip on something the repo already shows you.

## Example output

```
Pre-implementation grill. 3 questions before I touch code.

Q1: Where should the saved-list state live?
1. SavedVariables / accountDB (Recommended)  — survives reload, account-wide
2. CharDB                                     — per-character only
3. In-memory                                  — lost on reload

Q2: Default item status on import?
1. want (Recommended)  — matches tracker conventions
2. unmarked            — user marks each by hand

Q3: On import to existing list — overwrite or merge?
1. overwrite (Recommended)  — clean, predictable
2. merge by item id         — keeps user's existing marks
Other (free text)

Reply with numbers. Example: "1, 1, 2".
```
