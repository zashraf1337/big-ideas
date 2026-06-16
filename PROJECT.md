# Big Ideas — Tech Breakthroughs Tracker

A weekly-updated tracker of major tech breakthroughs (2021 onwards) covering AI, bio, energy, space, quantum, and autonomy.

## Files in this folder

| File | What it is |
|---|---|
| `state.json` | **Base truth.** All breakthroughs, people, sub-ideas, frontier bullets, watch picks, sources, and the weekly_history log. The dashboard and PDF are both rendered from this file. |
| `dashboard.html` | Static dark-mode dashboard. Open directly in a browser. Self-contained (state.json data is embedded). |
| `dashboard_artifact.html` | Light-mode version published as a Cowork **Live Artifact** (`big-ideas-tech-breakthroughs`). Shows up in Claude Desktop's Live Artifacts section. |
| `tech_breakthroughs_report_YYYY-MM-DD.pdf` | Snapshot PDF report — date in filename matches `state.meta.as_of_date`. Old PDFs are not deleted on weekly runs (they accumulate as a history). |
| `weekly_highlights/` | One folder per weekly run. Each run drops `findings_YYYY-MM-DD.json` (the input to the merge) and `YYYY-MM-DD.md` (a human-readable digest). |
| `scripts/build_dashboard.py` | Regenerates `dashboard.html` from `state.json`. |
| `scripts/build_artifact.py` | Regenerates `dashboard_artifact.html` (light-mode for the Live Artifact). |
| `scripts/build_pdf.py` | Regenerates the dated PDF from `state.json`. |
| `scripts/weekly_update.py` | Merges a `findings_*.json` into `state.json` and appends a `weekly_history` entry. |
| `PROJECT.md` | This file. |

## The base run (2026-05-08)

Initial capture across **11 breakthroughs** — the 10 from the original spec plus self-driving cars/robotaxis as #11:

1. Transformers / LLMs / coding agents (incl. MCP, agentic AI)
2. RLHF + reasoning models (test-time compute scaling)
3. Diffusion models (image + video)
4. AlphaFold + computational protein design
5. mRNA vaccines + LNP delivery
6. GLP-1 agonists
7. CRISPR therapies (Casgevy + base/prime editing)
8. Quantum error correction (logical qubits below threshold)
9. Reusable rockets (Falcon 9 + Starship catch)
10. Renewables + battery cost collapse
11. Self-driving cars / robotaxis

For each: 5–6 named people (org-type tagged), 5 sub-ideas, 3–5 frontier bullets, 3–4 watch picks, impact + watch-for-next, flags. **150 unique source URLs.**

## Weekly run protocol

A scheduled Claude task should run every **Monday morning** and:

1. **Load context** — read `state.json` and note `meta.as_of_date` (start of the diff window).
2. **Research in parallel** — dispatch 3–4 research agents to scan the web for items dated in the past 7 days, split by domain (AI / bio / physical). Each agent returns candidate items as JSON with kind + payload.
3. **Assemble** — consolidate into `weekly_highlights/findings_YYYY-MM-DD.json` (schema in `scripts/weekly_update.py`).
4. **Merge** — `python3 scripts/weekly_update.py weekly_highlights/findings_YYYY-MM-DD.json`. This appends to `state.json`.
5. **Rebuild outputs**:
   - `python3 scripts/build_dashboard.py` → updates `dashboard.html`
   - `python3 scripts/build_artifact.py` → updates `dashboard_artifact.html`, then call `mcp__cowork__update_artifact` with id `big-ideas-tech-breakthroughs`
   - `python3 scripts/build_pdf.py` → writes a new dated PDF
6. **Digest** — drop a `weekly_highlights/YYYY-MM-DD.md` summary.
7. **Notify** — reply with the week's narrative, headlines per breakthrough, and updated file paths.

### What goes into a weekly entry

The merge supports six kinds of highlight (see `scripts/weekly_update.py` docstring):

- `NEW_BREAKTHROUGH` — a genuinely new top-level breakthrough (rare)
- `NEW_SUB_IDEA` — a new technique/method/component under an existing breakthrough (e.g. a new RL recipe → reasoning_models)
- `NEW_FRONTIER` — a new state-of-the-art result, paper, product, or benchmark
- `NEW_WATCH` — a rising lab / startup / individual to add to the watch list (with funding stage)
- `NEW_PERSON` — a foundational or currently-active person not yet in the people list
- `UPDATED_FACT` — a previously-recorded fact has changed (e.g. battery $/kWh)

### Quality bar

- Every highlight must cite a real, resolving URL. No fabrication.
- Prefer primary sources (arxiv, Nature, Science, FDA, BloombergNEF, company engineering blogs).
- 5–15 highlights per week is the right size; do not pad.
- Dropping breakthroughs / overwriting old data is not allowed — the weekly task only appends. Edits to existing entries should be done explicitly by the user.

## Updating the project instructions in Cowork

Replace the current project_instructions in Cowork settings with the contents of `cowork_project_instructions.md` in this folder.
