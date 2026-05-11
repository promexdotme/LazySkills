# Tests — Viber Policy

Default: don't write tests unless asked. Suggest tests when stakes are real.

This is a policy, not a workflow. Read it when test work comes up. Don't quote it back at the user.

---

## When to suggest tests

**Real stakes — suggest tests:**
- Auth, session handling, permissions
- Payments, billing, money math
- Database migrations or schema changes
- Data-loss paths (delete, overwrite, archive, hard-reset)
- Anything user explicitly says "must not break"
- Anything that runs in production and can't easily be rolled back

**No real stakes — skip tests, just ship:**
- UI tweaks, copy changes, styling
- Throwaway prototypes
- One-off scripts
- Glue code that crashes loudly when wrong
- Personal projects where user wants speed over rigor

When in doubt, ASK in one line:
> Risky path. Write a test for `<specific behavior>` first?

---

## How to write them when needed

- **Test BEHAVIOR, not implementation.** Test through public interfaces.
- **Good test:** "user can checkout with valid cart" — describes a capability.
- **Bad test:** "calls `fooHandler` exactly once" — describes internal mechanics.
- Tests should survive refactors. If renaming an internal function breaks the test, the test was wrong.
- One test → one piece of implementation. NOT "write 5 tests, then write 5 implementations."

---

## When user asks for "TDD" / red-green-refactor

Vertical slices, not horizontal:

```
RED:   Write ONE failing test for ONE behavior.  Watch it fail.
GREEN: Write minimum code to pass.                Watch it pass.
       Repeat for next behavior.
REFACTOR: Only while green. Never while red.
```

Anti-pattern: writing all tests first, then all implementation. Produces tests that test the imagined SHAPE of things instead of actual behavior. Don't do this.

---

## Mocks

- Mock external services (third-party APIs, email, payment gateways).
- Don't mock the database in integration tests. Use a real test DB or a fast in-memory equivalent.
- Don't mock the unit you're testing.
- Don't mock internal collaborators just to make a unit test possible — that's a sign the seam is wrong.
