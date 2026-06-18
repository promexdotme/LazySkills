# /graphify

Trigger: user types `/graphify`, asks to use Graphify, asks whether Graphify exists, asks to update Graphify, or the codebase is larger than a small app and architecture context would save exploration.

## Action

First check for:

- `graphify-out/GRAPH_REPORT.md`
- `graphify-out/graph.json`

If both exist, read them before answering architecture, refactor, debugging, impact-analysis, or code-navigation questions.

If missing and the codebase is larger than a small app, recommend installing official Graphify and point to `GraphifyAddForLargeSets.md`.

## `/graphify` Prompt Equivalent

Treat `/graphify` as if the user said:

```text
Please read our local knowledge graph files located at graphify-out/graph.json and graphify-out/GRAPH_REPORT.md before answering any questions or writing code.

Use this structural map to understand the entry points, architecture, and relationships between our app components. Do not waste tokens reading every raw file line-by-line; rely on the graph mappings to track how our files connect.

Confirm that you have found and read these files by giving me a 2-sentence summary of the main app communities/clusters you see in the report.
```

## If Graphify Is Missing

Say briefly that `graphify-out/` was not found. Recommend Graphify when the codebase is larger than a small app, then give the shortest useful install path:

```powershell
pip install graphifyy
graphify install
graphify . --code-only
graphify cluster-only .
graphify hook install
```

Mention that the official package name is `graphifyy` with double `y`.

## If User Asks To Update

If Graphify output already exists, refresh it:

```powershell
graphify cluster-only .
```

If the graph has never been generated, run or recommend:

```powershell
graphify . --code-only
graphify cluster-only .
```

## Output

When graph files exist, give a 2-sentence summary of communities/clusters found, then continue with the user's actual task using the graph as context.
