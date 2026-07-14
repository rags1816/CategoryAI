# CategoryAI Strategic Category Suite

**A complete procurement category strategy tool in a single HTML file.** Open it in a browser and build an end-to-end category strategy — market analysis, positioning, supplier strategy, negotiation plan, execution tracking and a board-ready document — with AI assistance at every step and full transparency about where every input came from.

> **Formerly ProcureAI Strategic Category Suite.** v1.1.0 renames the product to CategoryAI; sessions and files from v1.0 load without any migration steps.

## Try it in 60 seconds

Open `categoryai-strategic-category-suite-v1_1_0.html`, choose **🏖 Sandbox** as the provider (header ⚙ — no API key, nothing leaves your machine), and click **Guided demo tour**. Sixteen stops walk the full workflow on a simulated Cloud Services category, from profile to finished strategy document.

## What's inside

| Phase | Modules |
|---|---|
| **Intake** | Category profile · Spend profile (optional CSV upload) · Market info hub with live research assistant |
| **Assessment** | SWOT & PESTLE · Porter's Five Forces with radar chart · Kraljic matrix with quadrant strategy advice |
| **Strategy** | Supplier segmentation, scorecard, preferencing & Gold/Silver/Bronze tiering · **SRM post-contract reviews with dated history and grading** *(new)* · 5×5 risk heatmap with ESG opportunities · Purchasing chessboard (open 64-method board; licensed ATK board pluggable) · Cost drivers & levers across 20+ category archetypes |
| **Bargaining** | Huthwaite-style negotiation plan: objectives, BATNAs, issues matrix, trading board |
| **Execution** | 3-year Gantt · RACI · Savings pipeline with **status funnel, complexity, owners and value view** *(upgraded)* · Benefits register across five benefit types · Maturity self-assessment **plus staged CIPS/Hackett-style practice checklist** *(new)* |
| **Output** | Optional commercial 7Ps · Strategy document with elevator pitch and defend-your-strategy FAQs · Word (.docx) export · PowerPoint board deck · Four fillable master templates · Per-module Word reports |

## Design principles

- **External data first.** A full strategy can be built from market data alone; internal spend upload is an optional refinement, never a prerequisite. New in 1.1.0: enter an approximate annual spend to unlock indicative £/$ values — clearly flagged as an assumed baseline.
- **Confidence transparency.** Every AI-generated input carries a User / AI-inferred / Assumed flag with one-click confirmation. Every AI section explains its sources.
- **Accumulate, never overwrite.** Regenerating chessboard methods appends recommendations for you to keep or discard; SRM reviews build dated history rather than replacing scores.
- **Visible progress.** Module dots, per-phase completion counts in the collapsible navigation, and a Module Review with per-module export.

## Getting started

1. Download the HTML file and open it in any modern browser (internet needed for CDN libraries; Sandbox mode needs no AI network access).
2. Pick an AI provider in the header ⚙:

| Provider | Needs | Notes |
|---|---|---|
| 🏖 Sandbox | Nothing | Simulated demo data, honestly tagged; fully offline-safe |
| Claude (in-app) | Running inside Claude.ai | No key required |
| Claude (API key) | Anthropic key | Stored locally only, at your choice |
| Gemini 2.5 Flash/Pro | Google key | Automatic model fallback |

3. Name your category on step 1 — every other module unlocks from there.
4. Work saves automatically in your browser; export a session `.json` any time for backup or hand-over (v1.0 `procureai-session` files import cleanly).

## Documentation

`docs/` contains the User Guide, Reference Guide and Admin Guide (v1.0 editions — they carry the former ProcureAI name; content remains accurate for the workflow, with 1.1.0 additions covered in `CHANGELOG.md`).

## Privacy & network

Keys are stored on your device only, and only if you choose to save them. Session data lives in your browser and in files you export. In Sandbox mode nothing is sent anywhere. CDN access is required for React, Babel, PapaParse, pptxgenjs and docx libraries.

## Customisation

The Admin panel manages API keys, a local user register, custom document templates, custom category archetypes, and the licensed A.T. Kearney chessboard plug-in (board data not included — see LICENSE).

## Version

**v1.1.0 — frozen 2026-07-14.** See `CHANGELOG.md` for the full release history and SHA-256 checksums. Development continues on a copy toward v1.2.
