# Doppelgangers

Find duplicate issues and PRs through embedding visualization. Fetches issues/PRs from a GitHub repo, generates embeddings, and renders an interactive 2D/3D scatter plot where similar items cluster together.

## Install

```bash
npm install -g doppelgangers
```

Or run directly:

```bash
npx doppelgangers --repo owner/repo
```

## Usage

```bash
export OPENAI_API_KEY=...
doppelgangers --repo https://github.com/facebook/react
```

This will:
1. Fetch all open issues and PRs from the repo
2. Generate embeddings using OpenAI
3. Project them into 2D and 3D using UMAP
4. Output `triage.html` with an interactive viewer

## Options

```
--repo <url|owner/repo>   GitHub repository (required)
--state <state>           Item state: open, closed, or all (default: open)
--type <type>             Item type: pr, issue, or all (default: all)
--output <path>           Output path for items JSON (default: prs.json)
--embeddings <path>       Output path for embeddings (default: embeddings.jsonl)
--html <path>             Output path for HTML viewer (default: triage.html)
--model <model>           OpenAI embedding model (default: text-embedding-3-small)
--batch <n>               Batch size for embeddings (default: 100)
--max-chars <n>           Max chars for embedding input (default: 4000)
--body-chars <n>          Max chars for body snippet (default: 2000)
--neighbors <n>           UMAP neighbors (default: 15)
--min-dist <n>            UMAP min distance (default: 0.1)
--search                  Include embeddings for semantic search (increases file size)
```

## Viewer Features

**Filtering:**
- Toggle PRs and Issues visibility
- Toggle Open and Closed items
- Semantic search (requires `--search` flag, prompts for API key)

**Selection:**
- Shift+drag to select (replaces selection)
- Ctrl/Cmd+Shift+drag to select (adds to selection)
- Click empty space to deselect

**Sidebar Actions:**
- "Open All" opens all selected items in new tabs (allow popups in browser)
- "Copy" copies selection as formatted list to clipboard

**2D Mode:**
- Drag to pan
- Scroll to zoom
- Ctrl/Cmd+drag to select (adds to selection)

**3D Mode:**
- Drag to rotate
- Ctrl/Cmd+drag to pan
- Scroll to zoom

**Visual Encoding:**
- Circles = PRs, Diamonds = Issues
- Green = Open, Purple = Closed
- Orange = Selected

## Requirements

- Node.js 20+
- `gh` CLI (authenticated)
- `OPENAI_API_KEY` environment variable

## License

MIT
