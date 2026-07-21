# CATEGORYAI — Strategic Category & Portfolio Suite

A **single-file, self-contained HTML application** for procurement practitioners: build complete category strategies and portfolio strategies — from market analysis to board-ready documents — entirely in the browser. No install, no server, no account; your data never leaves your machine.

**Current frozen release: v2.21.1** · baseline v1.2.1 · portfolio track frozen at v2.12.0

## Two standalone workbenches

**💼 Portfolio Workbench (P1 → P2 → P3)** — charter (20 fields, 4 groups), Stage-3 fact base (21 one-line positions), composition (service lines), portfolio library, input routes (online / Excel round-trip / Word template round-trip with custom label language / document ingestion). P2 runs four titled stages: strategic questions → 2–5 generated options (incl. capability-based) → weighted assessment matrix (editable weights, advisory leader) → 10-dimension risk heat. P3 rolls up per-line strategies (AI draft or manual deep-dive), with executive summary, edit-&-confirm sign-off, portfolio risk register, and a 12-section board-paper .docx with embedded charts.

**📦 Category Workbench (Steps 1–14)** — profile, spend, market info hub with research assistant, SWOT/PESTLE (grounded in research findings), Five Forces (radar + traditional diagram), Kraljic, supplier segmentation/scorecards/preferencing/tiering, 5×5 risk register, 64-cell purchasing chessboard (own board, *similar to* the A.T. Kearney model; licensed data pluggable), cost drivers & levers, options & opportunities engine (Portfolio-vs-Category level), Huthwaite-style negotiation plan, execution Gantt/RACI, savings pipeline & benefits, decision-first strategy document (pitch → summary → strategy → evidence → FAQ → assumption register), **business case in two formats** (Value Management template · Five Case Model), matching PowerPoint deck.

Each workbench **works alone**; they connect only by user choice — deep-dive a portfolio line through Steps 1–14 (charter inherited, live sync), or update/add a line from a standalone category build (stamped, declared).

## Principles
- **External data first** — a strategy is buildable from market data alone; internal spend refines, never gates.
- **Accumulate, never overwrite** — AI suggestions append; the manager selects what to keep.
- **Every input declares its source** — User / AI-inferred / Assumed confidence flags flow into the assumption register and bibliography.
- **Honest gaps** — empty sections are omitted or marked, never padded; business cases emit `[To complete]` for what needs named accountability.

## Quick start
1. Download `index.html`, open it in Chrome/Edge (double-click). 2. Pick a workbench on the 🚦 start screen, or run the ▶ Demo tour (offline, simulated, labelled). 3. Configure an AI provider in ⚙ (Claude/Gemini key) or use Sandbox mode. See `USER_GUIDE.md` and `DEPLOYMENT.md`.

## Data & devices
One person · one device · one browser profile = one private workspace (localStorage). No sync — hand off between devices via ⬇/⬆ session .json (stamped with workspace name & time). Shared PCs: use separate browser profiles. Details in-app under About → 💾 Data & devices.

## Licence
MIT — see `LICENSE`. The chessboard is CategoryAI's own 64-cell board, similar in concept to the A.T. Kearney Purchasing Chessboard®; the licensed ATK dataset is **not** included (plug-in slot in Admin).
