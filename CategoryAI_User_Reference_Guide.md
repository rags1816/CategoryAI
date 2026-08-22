# CategoryAI — User Reference Guide
_v2.38.5 · Portfolio & Category Strategy Suite_

## 1. What CategoryAI is

A browser-based procurement strategy tool for category managers, built
around established frameworks: Kraljic matrix, Porter's Five Forces, the
A.T. Kearney-style Purchasing Chessboard, Huthwaite-style negotiation
planning, SWOT/PESTLE, supplier segmentation, should-cost analysis.

It's two independent workbenches, usable separately or linked together:

- **Category Workbench** — a 14-step wizard building one category's
  strategy, negotiation plan, and business case.
- **Portfolio Workbench** — a 3-phase tool (P1/P2/P3) for a
  cross-category portfolio strategy and board paper.

**Only the category name is a true requirement.** Everything else is
optional and, in almost every case, AI-fillable — you can build a
complete strategy from a bare category name plus AI generation, using
manual input only where you want to improve accuracy.

## 2. Getting started — AI provider setup

⚙ AI Settings, top right. Four modes:

| Mode | Needs | Works where |
|---|---|---|
| Claude · in-app | Nothing | Only inside claude.ai |
| Claude · API key | A real Anthropic key | Any browser |
| Gemini | A real Google key | Any browser |
| Sandbox | Nothing | Any browser (offline demo data) |

If you're using this outside claude.ai and AI features aren't working,
this is almost always why — switch to "Claude · API key" or "Gemini" and
use **Test connection** to confirm it's live.

## 3. Category Workbench — Steps 1 to 14

| Step | Purpose | AI-fillable? |
|---|---|---|
| 1 · Category profile | Name (required), sector/region, incumbent suppliers, pain points, specs & requirements (what you're buying), a Stakeholder map (Mendelow's grid) | Suppliers/pains/notes: yes; specs and stakeholders are manual — organisational fact, not AI-guessed |
| 2 · Spend profile | Internal spend data (CSV) — optional. Skipping keeps you in "generic mode" | No — real data or manual sliders |
| 3 · Market info hub | 9 external market variables + research assistant | Yes, one button scores all nine |
| 4 · SWOT & PESTLE | Buyer-perspective framing, grounded in Step 3 evidence | Yes, in full |
| 5–6 · Five Forces & Kraljic | Derived automatically | Fully derived |
| 7 · Suppliers & tiering | Segmentation, scorecards, SRM review history, and a Contract register (dates, value, notice period) | Yes — AI-assess (segmentation/scorecards); contracts are manual |
| 8 · Risk heatmap & ESG | 5×5 risk register + ESG opportunities | Yes, in full |
| 9 · Purchasing chessboard | Sourcing methods from the 64-method board | Yes — recommendations accumulate, you tick "Keep" |
| 10 · Cost drivers & levers | Should-cost weighting + levers | Yes — playbook default or full AI |
| 11 · Negotiation plan | Objectives, BATNAs, issues, trades, behaviours | Yes — grounded in Kraljic position and kept chessboard methods |
| 12 · Execution plan | Delivery plan | Partially AI-assisted |
| 13 · Commercial 7Ps (optional) | Sell-side canvas — only relevant if the category IS the business | Yes, throughout. Excluded from exports by default |
| 14 · Strategy & plan | Final synthesis, exports, business case, elevator pitch | Yes — one AI call |

### Accumulate, never overwrite
The Chessboard and Options steps **add** each new AI batch to what's
already there, rather than replacing it. You tick "Keep" on what you
want; only kept items flow into the final document. Regenerating never
silently discards a previous selection.

### The pre-flight check
Before generating Step 14, the app shows exactly what's missing (market
brief, research, SWOT, suppliers, etc.) and lets you continue anyway
(gaps get listed under "Data gaps to close") or go back and complete
them first.

### ⚠ If you download without generating first
Every export format (.docx, .pptx, .md) will now show a clear "⚠ DRAFT —
Generate Strategy has not been run" banner if you download before
generating — this is deliberate, not a bug: the document itself declares
its own incompleteness so it's never misleading, even if forwarded or
shared outside the app.

### Module Review — a per-step Word export
Every step has its own "📊 Module review" card: a Complete/Pending badge,
an on-screen chart where the module produces one (Five Forces, Kraljic,
Suppliers, Risk, Chessboard, Cost drivers), and a "⬇ Module report
(Word)" button — a single-module document with that same chart actually
embedded (not just the on-screen preview), useful for circulating one
piece of the analysis without the full 14-step document.

### Collapsible sections, across most of the workbench
AI-generated output collapses by default on Steps 3, 4, 5, 8, 10, 11,
and 14 (Research findings, SWOT/PESTLE, Five Forces breakdown, Risk
register, ESG opportunities, savings/KPI grids, negotiation issues
matrix, trading board, behaviours roadmap, and every Step 14 section
except Executive Summary, which stays visible as the orientation
anchor). Deliberately left uncollapsed everywhere it's an active
editing surface rather than passive review content — Suppliers
scorecard, Contract register, Chessboard, Execution Plan's Gantt/RACI,
and Step 13's tracking tables all stay visible, since collapsing an
active input surface would hurt usability, not help it.

### 📁 My Categories — multiple independent categories, one browser
Click "📁 My Categories" in the header (or use the inline widget on
Step 1 itself) to create and switch between genuinely separate,
independent categories in the same browser. "+ New category" creates a
real blank record — unlike simply retyping a name into the Category
name field, which renames the *currently active* record in place and
carries over every other field (suppliers, risks, chessboard picks)
under the new name. Delete removes a category's entire record
permanently, with a confirm first.

### Category phase banner
A chevron strip at the top of every Category Workbench screen shows the
current phase — Define → Understand → Strategise → Source → Contract &
Manage → Output — with completed phases marked. Note: Five Forces (Step
5) shows under Understand, not Strategise, by design — it's grouped with
SWOT/PESTLE as a market-understanding tool, not a strategy-selection
one. The sidebar's own per-phase counters can look ahead of the banner
in places (e.g. showing a later phase already partly "done") — that's
because a couple of steps share completion logic with an earlier one
(Kraljic mirrors Five Forces' readiness), not a banner error.

### 🔎 Find — jump to any screen
Click "🔎 Find" in the header to search every screen's name and one-line
description, across both workbenches. Type to filter live, click a
result to jump straight there. Escape closes it; Enter jumps to the
current top result (Enter doesn't trigger the search itself — that
happens as you type).

## 4. Portfolio Workbench — P1 to P3

| Phase | Purpose |
|---|---|
| P1 · Charter & composition | 19-field parent charter + your list of categories/service lines (name, spend, risk, Kraljic, Playbook). Route-to-market channel suggestions per line — click "use this →" to actually accept a suggestion, not just view it |
| P2 · Strategic options | 3–5 distinct portfolio-level options, scored |
| P3 · Roll-up, matrix & report | Per-line strategy drafting, the Portfolio Matrix, the consolidated 12-section board-paper report |

### Category hierarchy
Any line can be split into sub-categories at any depth via "➕ Duplicate
as child." Descriptive context (notes, playbook, channel, specialization,
supplier count, volume) copies down; **scores never do** — every child
starts fully unassessed, exactly like a brand-new category.

### The rollup engine
A parent with assessed children shows a **rolled-up** position, not its
own individual score: spend-weighted average by default (falls back to
simple average if no child has spend entered), or a worst-case/
highest-risk-child alternate mode. Unassessed children are always
excluded — never blended in as a guess — with a visible "rollup
incomplete" indicator whenever it's partial.

### Linking to a Category
From P3, "Deep-dive" on any line opens the Category Workbench with the
parent charter's relevant fields (objectives, governance, risk appetite,
sustainability, AI strategy, benefits framework) already inherited;
line-local fields (market, suppliers, KPIs) start blank for your own
assessment. A standalone category can also be attached back into a
portfolio at the end of its own Step 14.

**Known limit:** child-level (sub-category) assessments don't yet feed
the exported board-paper report — the roll-up and report currently
reflect level-1 lines only. This is a documented scope boundary, not a
bug.

## 5. Prefer to prepare offline? The Category input template

On Step 1, "⬇ Download input template" gives a 10-sheet spreadsheet — a
**Read me** cover sheet (what each sheet is for and how it feeds the
app, plus a full scoring-criteria reference — every 1-5 field's "1
means.../5 means..." in one place) plus 9 real data sheets:

- **Profile** — name, sector, region, notes, specs & requirements,
  suppliers, pains
- **Variables** — all 9 market + internal variables — the most tedious
  one-by-one task in the wizard, so the highest-value sheet to fill
  offline
- **Spend** — supplier + amount. Folds in what used to be a separate
  .csv upload on Step 2 — one file now covers both. Auto-strips
  currency symbols and commas (`$1,234,567` parses correctly), auto-
  infers the total, top-10 suppliers, and the supplier-concentration
  score exactly like the standalone upload always did — same formula,
  not a simplified version. The Step 2 CSV upload still exists
  separately too, if you'd rather refresh spend alone without
  re-touching the whole template.
- **Suppliers**, **Risks** — as in-app
- **Contracts** — name, supplier, dates, value, notice period, status —
  feeds negotiation timing
- **Demand forecast** — period, amount, trend
- **Stakeholders** — Mendelow's power-interest grid: influence × interest
- **Supplier performance** — feeds the existing SRM Review history,
  adds to it, doesn't replace

Every column header carries its own scoring criteria inline (e.g.
"Capability (1=Limited/unproven, 5=Best-in-class)"), so the ambiguity
of a bare "Score (1-5)" column is gone — you don't need to cross-
reference the Read Me sheet just to know what a number means, though
it's there for the fuller picture.

Fill it — alone, or with a colleague — then "⬆ Upload filled template"
applies it back. You'll see exactly how many fields/scores/rows will
change before confirming. If a column header can't be recognized (e.g.
a column got deleted or renamed), that sheet is **not imported at all**,
with a clear warning — never a silent guess that could scramble data.

This is separate from the Portfolio Workbench's own Excel round-trip
(P1's composition template) — each track has its own.

## 6. Exports

| Format | Contents |
|---|---|
| .docx (Word) | pitch → executive summary → objectives → levers → options → negotiation approach → roadmap → risks → data gaps → evidence charts → FAQ → assumption register. Real embedded charts |
| .pptx (PowerPoint) | Mirrors the .docx order, one slide per module, same charts — including PESTLE, Research findings, ESG opportunities and a condensed Assumption register (the fully exhaustive audit trail is in the Word doc) |
| Business case — VM template | Recommended, procurement-linked: stakeholders → opportunity → benefits delivery plan → project economics → risks & alternatives |
| Business case — Five Case Model | Same session data, HM Treasury-style structure |
| .md (Markdown) | Plain-text equivalent, for wikis |
| 2-page Category Execution Plan (.docx) | New v2.35. A dense, at-a-glance summary distinct from the full strategy document: spend/scope header, spend profile, demand & strategy, Five Forces, supplier landscape, 3-year plan, near-term actions, and a Disruptors table (from Research Assistant findings). On-screen preview available before downloading. Does NOT include PESTLE — it's deliberately compact, not a second full document. |

7Ps is excluded from every export by default (toggle it on in the
Document Composer if the category genuinely IS the business being sold),
and is never included in either business case format regardless of the
toggle — it's a strategy-document concern only.

## 7. Guide chat, Demo Tour & Excel round-trip

**Guide chat** (📚 "Guide — this screen") — an AI chat bubble on every
screen, grounded in
that screen's specific mechanics plus a master library covering cost
drivers, levers, and playbooks. No live web search — it answers from its
own knowledge base plus standard category-management reasoning.

**Demo Tour** (▶ Demo tour, header) — 19 stops: Category Workbench (16
stops) then Portfolio Workbench (3 stops), on a full simulated Cloud
Services dataset. **Confirms before starting** since it replaces
whatever's currently in your session.

**Excel round-trip** — download a pre-filled template from P1, edit
offline, upload back. Columns are matched by their actual header text
(not position), so reordering columns is safe; if a required column is
deleted or truly unrecognizable, you'll get a clear warning before
anything imports, rather than silent data corruption.

## 8. Data & device model

Everything lives in this browser's local storage — one device, one
private workspace. Nothing syncs automatically. Moving between devices
needs a manual session export/import (⬇ Backup session as .json).
Two people sharing a browser profile will overwrite each other's work.

## 9. Required-Input Reference

| Field | Required? |
|---|---|
| Category name | **Required** |
| Everything else (sector, suppliers, market data, SWOT, cost drivers, negotiation plan, 7Ps) | Optional, AI-fillable |
| Internal spend data | Optional — the one input that meaningfully upgrades a generic sector-typical playbook into a data-backed strategy |
