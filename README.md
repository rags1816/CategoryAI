# CategoryAI

**Portfolio & Category Strategy Suite** — a browser-based procurement
category management workbench, built as a single HTML file with no
build step, no server, and no installation.

**Live**: [rags1816.github.io/CategoryAI](https://rags1816.github.io/CategoryAI/)

## What it does

Guides a category manager through building a complete sourcing
strategy — from market analysis through negotiation planning to a
finished business case — using established frameworks: Kraljic matrix,
Porter's Five Forces, SWOT/PESTLE, supplier segmentation, a purchasing
chessboard (similar to the A.T. Kearney model), should-cost analysis,
and Huthwaite-style negotiation planning.

Two independent tracks, usable separately or linked together:

- **Category Workbench** (Steps 1-14) — one category's full strategy,
  external market data alone or enriched with internal spend
- **Portfolio Workbench** (P1-P3) — a cross-category charter, strategic
  options, and a consolidated board-paper report

Only the category name is a genuine requirement. Everything else is
optional and, in almost every case, AI-fillable.

## Running it

There's nothing to install. Two ways to use it:

1. **Inside claude.ai** — open the file directly; the built-in Claude
   provider works with no API key.
2. **As a standalone site** (this repo's actual deployment) — open
   `index.html` in any browser, or host it anywhere static files are
   served (GitHub Pages, as it is now). You'll need to add your own
   Claude or Gemini API key in ⚙ AI Settings, or use 🏖 Sandbox mode for
   offline simulated demo data with no key at all.

No `npm install`, no build command. Every dependency (React,
Babel-standalone, PapaParse, pptxgenjs, SheetJS, docx) loads from a CDN
at runtime.

## Key features

- **AI-assisted, always transparent** — every AI-generated or -inferred
  value carries a visible confidence flag (User / AI-inferred / Assumed),
  one click to confirm ownership
- **Accumulate, never silently overwrite** — regenerating the Chessboard
  or Research Assistant adds to what's there; other AI-generated
  sections confirm before replacing
- **Offline-first data prep** — a 10-sheet downloadable/uploadable Excel
  template covers profile, spend, market variables, suppliers, risks,
  contracts, demand forecast, stakeholders, and supplier performance,
  for anyone who'd rather fill it in before sitting at the app
- **Real exports** — genuine `.docx`/`.pptx` with embedded charts, two
  business-case formats, a compact 2-page Category Execution Plan, and
  per-module Word reports from any single screen
- **🔎 Find** and **📁 My Categories** — jump to any screen by keyword;
  run multiple independent categories in one browser
- **One device, one workspace** — everything lives in that browser's
  local storage; nothing syncs automatically. Move between devices with
  an explicit session export/import (⬇ Backup session as `.json`)

## Documentation

| File | For |
|---|---|
| [`CLAUDE.md`](./CLAUDE.md) | AI agents (Claude Code) picking up development work |
| [`METHODOLOGY.md`](./METHODOLOGY.md) | The patch→verify→freeze workflow used on this repo |
| [`CategoryAI_Developer_Guide.md`](./CategoryAI_Developer_Guide.md) | Architecture, known quirks, patch discipline |
| [`CategoryAI_Admin_Guide.md`](./CategoryAI_Admin_Guide.md) | AI provider setup, deployment checklist |
| [`CategoryAI_User_Reference_Guide.md`](./CategoryAI_User_Reference_Guide.md) / `.docx` | Full user-facing feature reference |
| [`CategoryAI_Testing_Guide.md`](./CategoryAI_Testing_Guide.md) | Reusable test prompt templates |
| [`CategoryAI_EndToEnd_Test_Script.md`](./CategoryAI_EndToEnd_Test_Script.md) | Full-lifecycle regression script |
| [`CategoryAI_PreLaunch_Checklist.md`](./CategoryAI_PreLaunch_Checklist.md) | Quick pre-release sign-off checklist |
| [`CHANGELOG.md`](./CHANGELOG.md) | Version history with freeze checksums |

## Attribution & honest limitations

- The Purchasing Chessboard is CategoryAI's own 64-cell board, described
  as "similar to" the A.T. Kearney model — not a licensed reproduction.
  A plug-in slot exists (🛠 Admin) for organizations with a genuine
  A.T. Kearney license to load the official data.
- The staged maturity checklist is the tool's own construct, built in
  the style of CIPS/Hackett maturity models — not a licensed copy of
  either.
- No real accounts, no live multi-device sync, no multi-user approval
  routing — by design. A single static HTML file in a browser can't
  provide these honestly; pretending otherwise would risk exactly the
  data mix-ups this design avoids. These belong to a future server
  phase, not this one.

## Data & privacy

Everything (sessions, categories, portfolios, API keys) lives in your
browser's local storage. Nothing is sent anywhere except directly to
whichever AI provider you've configured, for that provider's own API
calls. Two people sharing one browser profile will see and can overwrite
each other's work — use separate OS logins or browser profiles for
genuinely separate workspaces.
