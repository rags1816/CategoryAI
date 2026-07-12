# Changelog

All notable changes to ProcureAI Strategic Category Suite.

## [1.0.1] — 2026-07-12 · FROZEN (hotfix)
### Fixed
- **Demo tour crash at stop 4** — the demo loader stored SWOT/PESTLE as raw arrays/strings instead of the app's per-key `{text, conf}` shape, blanking the SWOT & PESTLE screen; also corrected the demo `pitch` to `{text, faqs, conf}` and added the missing top-level confidence flag on the demo negotiation and execution plans. Shape-regression tests added so demo state is now asserted against the exact render shapes.

## [1.0.0] — 2026-07-12 · superseded by 1.0.1

### Guided experience
- **▶ Demo tour** — 16-stop narrated walkthrough of all modules on a full simulated *Cloud Services* dataset, generated offline by the Sandbox engine from the archetype library; loads instantly, no key, confirms before replacing current work
- **Progress tracking** — green/amber completion dot per module in the rail, driven by real module state, with an "X / 13 core modules complete" progress bar; optional modules (internal data, 7Ps) never block
- **📊 Module review card** on every screen — Complete/Pending badge, SVG output chart where chartable (market bars, five-forces bars, supplier scatter, risk severity bars, driver weights, planned-vs-delivered savings, workstream timeline) and a one-click per-module Word report

### Output & reporting
- **Real .docx export** — strategy document and all four master templates generate genuine Word files (docx library via CDN, three fallback URLs) with automatic legacy `.doc` fallback offline
- **PowerPoint deck export** — 14-slide widescreen board deck with native charts (market bars, five forces, cost-driver pie, planned-vs-delivered grouped bars), SWOT boxes, supplier/risk/roadmap/benefits tables and the 2-minute pitch (pptxgenjs via CDN)
- **Elevator pitch + 10 FAQs** — built from a source-tagged fact list (no invented numbers); the ten questions a sceptical CFO would ask, each answered with its source step

### AI & providers
- **🏖 Sandbox mode** — fourth AI provider: fully offline simulated answers for all 23 prompt signatures, synthesised from the archetype library; every output labelled `[Sandbox — simulated]` and flagged AI-inferred
- Providers: Claude in-app · Claude API key · Gemini (2.5-flash default, automatic model fallback) · Sandbox

### Frameworks & modules
- **Purchasing Chessboard rebuilt** — literal 8×8 board (strategy = 4×4 quadrant, approach = 2×2 block, cell = method); accumulate-and-select recommendations (append up to 15, never overwrite; AI told what's already shown), High/Medium fit ranking, **Keep checkboxes** (only ticked methods flow downstream), click-to-add manual picks marked User
- **Savings pipeline** — Planned % vs **Delivered %** with status gating (Delivered editable only at status Delivered, resets on regression); dual totals; carried into all exports
- **Contract tier calculator** — value (50%) / risk (30%) / complexity (20%) weighted score → suggested tier under the chosen scheme; **Gold/Silver/Bronze retained** as the recognised public-procurement (GCF) naming
- **Supplier preferencing** declared explicitly as a subjective judgement with sharpening guidance
- Porter Five Forces radar alongside the force diagram

### Foundation (carried forward and hardened)
- 15-step external-data-first workflow with generic mode; universal User / AI-inferred / Assumed confidence flags with assumption register; 9+5 variable registry; 16 cost drivers; 21 levers; 22 curated archetypes; 4 master templates; derived Five Forces & Kraljic; risk heatmap & ESG; Huthwaite negotiation planner; Gantt + RACI; KPI & maturity tracking; five-type benefits register; Commercial 7Ps; live research assistant (Claude); per-screen Guide bubble with master-library knowledge; session save/load; Admin panel (templates, archetypes, chessboard plug-in, users, keys)

### Documentation
- User Guide, Reference Guide and Admin & Deployment Guide shipped as Word documents in `docs/`

## Earlier development (unversioned)
Consolidation of the Vite/TypeScript pilot and strategy-studio into the single-file suite; iterative usability, explainability and framework rounds; feature ports from the GA comparison build.
