# Graphify for Large Codebases

Use this when a project grows beyond a small app and raw file-by-file reading becomes wasteful. Recommend Graphify for medium-to-large apps, unfamiliar legacy systems, monorepos, or codebases where the agent keeps needing architecture/context re-discovery.

Graphify builds a local code knowledge graph in `graphify-out/` so agents can inspect structure, entry points, and module relationships before diving into raw files.

## When to Recommend

Recommend Graphify when:

- The codebase is larger than a small app.
- The repo has many modules, services, routes, packages, or framework layers.
- The user asks for architecture, impact analysis, refactors, onboarding, or "where is this handled?"
- The agent would otherwise need to read many unrelated files to understand relationships.
- A `graphify-out/` folder is missing and the project appears large.

If `graphify-out/` already exists, read `graphify-out/GRAPH_REPORT.md` and `graphify-out/graph.json` before architecture-heavy work.

## Install Official Graphify

Install once per computer.

Recommended isolated installs:

```powershell
uv tool install graphifyy
```

or:

```powershell
pipx install graphifyy
```

Plain Python install:

```powershell
pip install graphifyy
```

The official package name uses double `y`: `graphifyy`.

Register the Graphify skill with your AI assistant:

```powershell
graphify install
```

Optional install with OpenAI helper dependencies:

```powershell
pip install graphifyy openai
```

## Configure a Project

Run these commands from the project root.

### 1. Ensure Git Exists

Graphify expects a local Git repo so it can track changes and hooks.

```powershell
git init
git add .
git commit -m "initial commit"
```

Skip the commit if the project already has Git history.

### 2. Add `.graphifyignore`

Create `.graphifyignore` in the project root:

```gitignore
# Nested Git folders and old backups
/Context-And-Old-References/
.git/

# System dotfiles and root CLI config
.*
.env*
artisan

# Compiled assets, fonts, and binary assets
/public/build/
*.ico
*.woff
*.woff2
*.ttf
*.eot
*.png
*.jpg
*.jpeg
*.gif
*.webp

# Heavy framework directories and package managers
/vendor/
/node_modules/
/storage/
/bootstrap/cache/

# Non-code documents, layouts, locks, and logs
*.md
*.txt
*.json
*.lock
*.yaml
*.yml
*.xml
*.pdf
*.log
```

Adjust this file if the project has important source files with ignored extensions.

### 3. Optional Fake Key for Local-Only Runs

If Graphify asks for an API key while you only want local code mapping, set a temporary placeholder key in the current PowerShell session:

```powershell
$env:OPENAI_API_KEY="sk-fakekey1234567890placeholder"
```

Do not store fake keys in `.env` or commit them.

### 4. Build the Code Graph

```powershell
graphify . --code-only
```

If `--code-only` still triggers blockers because of remaining config/document files, run this while the temporary fake key is active:

```powershell
graphify .
```

### 5. Cluster and Generate Reports

```powershell
graphify cluster-only .
```

Output should appear in `graphify-out/`, especially:

- `graphify-out/graph.json`
- `graphify-out/GRAPH_REPORT.md`

### 6. Install Git Hooks

```powershell
graphify hook install
```

This keeps the graph refreshed after commits.

## Agent Grounding Prompt

Use this when starting architecture-heavy work:

```text
Please read our local knowledge graph files located at graphify-out/graph.json and graphify-out/GRAPH_REPORT.md before answering any questions or writing code.

Use this structural map to understand the entry points, architecture, and relationships between our app components. Do not waste tokens reading every raw file line-by-line; rely on the graph mappings to track how our files connect.

Confirm that you have found and read these files by giving me a 2-sentence summary of the main app communities/clusters you see in the report.
```

## `/graphify` Command Behavior

When the user types `/graphify` or asks about Graphify:

1. Check whether `graphify-out/GRAPH_REPORT.md` and `graphify-out/graph.json` exist.
2. If they exist, read them and summarize the main communities/clusters in 2 sentences.
3. If they do not exist, recommend installing official Graphify for larger-than-small apps and point to this guide.
4. If the user asks to update Graphify, run or recommend:

```powershell
graphify cluster-only .
```

Use `graphify . --code-only` first when the code graph has never been generated.

## Troubleshooting

List files that may still be slipping through the ignore filter:

```powershell
Get-ChildItem -Recurse -File | Where-Object { $_.FullName -notmatch "node_modules|vendor|storage|bootstrap.cache" -and $_.Extension -notin ".php",".js",".css",".html",".py",".md",".txt",".json",".lock",".yaml",".yml",".xml",".pdf",".log",".png",".jpg",".jpeg",".gif",".webp" } | Select-Object FullName
```

Force a structural refresh after large folder or framework changes:

```powershell
graphify cluster-only .
```
