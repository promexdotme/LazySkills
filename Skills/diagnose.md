# /diagnose

Hard bug or perf regression. Don't guess. Build a feedback loop first.

---

## Trigger

User says `/diagnose`, "debug this", "diagnose this bug", reports something broken/throwing/failing, or describes a perf regression.

---

## Phase 1 — Build the loop (this is 90% of the value)

Goal: a fast, deterministic, agent-runnable pass/fail signal for the bug.

Try in roughly this order:

1. **Failing test** at the right seam (unit, integration, e2e).
2. **curl / HTTP script** against running dev server.
3. **CLI invocation** with fixture input, diff stdout vs known-good snapshot.
4. **Headless browser script** (Playwright / Puppeteer).
5. **Replay captured trace** — saved request, payload, or event log.
6. **Throwaway harness** — minimal subset of system, single function call.
7. **Fuzz / property loop** for "sometimes wrong" bugs.
8. **Bisection harness** if regression is between two known states.
9. **HITL bash script** — last resort. Human clicks, structured output feeds back.

If you cannot build a loop, STOP. Tell user. List what you tried. Ask for: environment access, captured artifact (HAR, log dump, screen recording with timestamps), or permission to add temporary instrumentation.

Do NOT proceed to hypothesis without a loop you trust.

### Iterate on the loop

Once you have *a* loop, ask:
- Faster? (cache setup, narrow test scope)
- Sharper signal? (assert specific symptom, not "didn't crash")
- More deterministic? (pin time, seed RNG, freeze network)

A 30-second flaky loop is barely better than no loop. A 2-second deterministic loop is a superpower.

### Non-deterministic bugs

Goal is not a clean repro. Goal is a HIGH reproduction rate. Loop trigger 100×, parallelise, add stress. 50%-flake is debuggable. 1% is not.

---

## Phase 2 — Reproduce

Run the loop. Confirm:
- Loop produces the SAME failure user described, not a nearby one.
- Reproducible across multiple runs (or, for non-deterministic, at high enough rate).
- Symptom captured exactly (error message, wrong output, slow timing).

Do not proceed until reproduced.

---

## Phase 3 — Hypothesise

List **3-5 ranked falsifiable hypotheses** before testing any. Single-hypothesis thinking anchors on the first plausible idea.

Format each: "If `<X>` is the cause, then `<changing Y>` will make bug disappear / `<changing Z>` will make it worse."

If you cannot state the prediction, the hypothesis is a vibe. Sharpen or discard.

**Show ranked list to user before testing.** They often re-rank instantly with domain knowledge ("we just deployed #3 yesterday"). Cheap checkpoint, big time saver.

---

## Phase 4 — Instrument

One probe per hypothesis. Change ONE variable at a time.

Tool preference:
1. Debugger / REPL inspection if env supports it. One breakpoint beats ten logs.
2. Targeted logs at boundaries that distinguish hypotheses.
3. Never "log everything and grep".

Tag every debug log with a unique prefix:
```
[DBG-a4f2] auth middleware token expiry: <value>
```

Cleanup at end = single grep. Untagged logs survive. Tagged logs die.

**Perf branch:** logs are usually wrong for perf. Use timing harness, `performance.now()`, profiler, query plan. Measure first, fix second.

---

## Phase 5 — Fix + regression test

Write the regression test FIRST, but only if a correct seam exists.

A correct seam = test exercises the real bug pattern as it occurs at the call site. If only a too-shallow seam is available (unit test that can't replicate the chain that triggered the bug), a regression test there gives FALSE confidence.

If no correct seam exists, that itself is the finding. Note it. Architecture is preventing the bug from being locked down. Flag for follow-up.

If correct seam exists:
1. Failing test at that seam.
2. Watch it fail.
3. Apply the fix.
4. Watch it pass.
5. Re-run the Phase 1 loop against original (un-minimised) scenario.

---

## Phase 6 — Cleanup

Required before declaring done:

- [ ] Original repro no longer reproduces (re-run Phase 1 loop).
- [ ] Regression test passes (or absence of seam documented).
- [ ] All `[DBG-*]` instrumentation removed (`grep` the prefix).
- [ ] Throwaway harness deleted (or marked clearly).
- [ ] **Update context log:** hypothesis confirmed, fix summary, file paths touched.

Commit / PR message states which hypothesis was correct. Future debuggers learn.
