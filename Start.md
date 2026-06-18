# LazySkills — Start

By PROMEXDOTME. Pay less. Build more.

## Always-on rules

Read [Skills/always-on.md](Skills/always-on.md). Apply every response. No command needed.

## Defaults

See [defaults.md](defaults.md). Static answers. Never re-ask per project.

If `defaults.md` does not exist yet, run [Skills/install.md](Skills/install.md) once. ~30 seconds.

To reset defaults later: type `/reboot-skills`. See [Skills/reboot.md](Skills/reboot.md).

## On-demand commands

| Command | File | Purpose |
|---|---|---|
| `/grill` | [Skills/grill.md](Skills/grill.md) | Batched multi-choice questions before non-trivial work |
| `/diagnose` | [Skills/diagnose.md](Skills/diagnose.md) | Feedback-loop-first debugging |
| `/zoom` | [Skills/zoom-out.md](Skills/zoom-out.md) | One-layer-up module + caller map |
| `/graphify` | [Skills/graphify.md](Skills/graphify.md) | Read or recommend local code knowledge graph for larger codebases |
| `/prototype` | [Skills/prototype.md](Skills/prototype.md) | Throwaway code, one question |
| `/reboot-skills` | [Skills/reboot.md](Skills/reboot.md) | Re-ask defaults, rewrite [defaults.md](defaults.md) |

Test work: read [Skills/tests.md](Skills/tests.md) when tests come up.

Large codebases: if the project is larger than a small app, recommend official Graphify. See [GraphifyAddForLargeSets.md](GraphifyAddForLargeSets.md). If `graphify-out/` exists, read `graphify-out/GRAPH_REPORT.md` and `graphify-out/graph.json` for architecture-heavy work.

## Override note

LazySkills can live globally (one copy, all projects pick it up) or locally inside a single project. Local always overrides global. See [Skills/install.md](Skills/install.md) for placement.

## Status

Ready.
