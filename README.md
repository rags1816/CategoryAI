# ProcureAI · Strategic Category Suite v1.0

A **single-file, no-install application** that walks a procurement category manager through building a complete, defensible category strategy — from external market data to a boardroom-ready Word document and PowerPoint deck — in 15 guided steps.

> **Try it in 60 seconds:** open `procureai-category-suite-v1.0.html` in any modern browser and click **▶ Demo tour** in the header. A full simulated *Cloud Services* category loads instantly (offline, no API key) and a 16-stop narrated tour walks you through every module.

---

## What it does

**Five phases, 15 modules:**

| Phase | Modules |
|---|---|
| **Intake** | Category profile · Spend profile (internal, optional) · Market info hub (9 external variables) |
| **Assessment** | SWOT & PESTLE · Five Forces (derived + radar) |
| **Strategy** | Kraljic matrix · Supplier segmentation, Gold/Silver/Bronze tiering & preferencing · Risk heatmap & ESG · Purchasing Chessboard (literal 8×8 board) · Cost drivers & levers |
| **Bargaining** | Negotiation plan (Huthwaite-style) |
| **Execution & Output** | Execution plan (Gantt + RACI) · Savings & value (planned vs delivered) · Commercial 7Ps (optional) · Strategy document, elevator pitch + 10 FAQs, downloads |

**Principles that make it different:**

- **External-data-first** — a full strategy can be built from market knowledge alone; internal spend data sharpens, never blocks (generic mode).
- **Confidence transparency** — every value is flagged **User / AI-inferred / Assumed**; the assumption register in the output shows reviewers exactly what has and hasn't been validated.
- **Grounded libraries** — 9 market variables, 16 cost drivers, 21 levers, 22 curated category archetypes, a 64-method chessboard, 4 master templates.
- **Progress you can see** — green/amber module dots, an X/13 progress bar, and a Module review card on every screen with a chart and a per-module Word report.

## Getting started

1. Download `procureai-category-suite-v1.0.html` and open it in Chrome, Edge, Firefox or Safari.
2. Open **⚙ AI settings** in the header and pick a provider:

| Provider | Key needed | Notes |
|---|---|---|
| Claude — in-app | None | When the file runs inside Claude.ai |
| Claude — API key | `sk-ant-…` | Enables the live web-search research module |
| Google Gemini | `AIza…` | gemini-2.5-flash default, automatic fallback |
| 🏖 Sandbox | None | Offline simulated demo data, clearly labelled |

3. Fill the **Category profile** and work left to right. Every screen has ⓘ tooltips and a 📚 Guide bubble that answers questions about that exact screen.
4. Download the result: a real **Word .docx**, a widescreen **PowerPoint deck**, Markdown, four pre-filled master templates, and per-module reports.

## Documentation

| Document | Audience |
|---|---|
| [`docs/ProcureAI-v1.0-User-Guide.docx`](docs/ProcureAI-v1.0-User-Guide.docx) | Category managers — the full walkthrough |
| [`docs/ProcureAI-v1.0-Reference-Guide.docx`](docs/ProcureAI-v1.0-Reference-Guide.docx) | Frameworks, formulas and master data behind every screen |
| [`docs/ProcureAI-v1.0-Admin-Guide.docx`](docs/ProcureAI-v1.0-Admin-Guide.docx) | Deployment, CDN whitelist, customisation, governance |

## Network & privacy

- Requires **cdnjs.cloudflare.com** at open time (React, Babel, PapaParse); the Word (`docx`) and PowerPoint (`pptxgenjs`) libraries load on demand with unpkg/jsDelivr fallbacks.
- API keys stay in the browser (memory, or localStorage if you click Save) and are sent **only** to the chosen AI vendor. In Sandbox mode nothing leaves the machine.
- All working data lives in the browser; sessions can be exported/imported as `.json` files.

## Customisation (Admin panel 🛠)

Custom document templates · custom category archetypes (JSON) · licensed A.T. Kearney chessboard plug-in (the built-in board is ProcureAI's open version) · local user register · provider pre-configuration.

## Versioning

This is the **v1.0 release candidate** — frozen after testing. See [CHANGELOG.md](CHANGELOG.md). Development continues on a copy toward v1.1.
