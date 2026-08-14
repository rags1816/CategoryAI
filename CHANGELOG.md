# Changelog

## v2.31.0
### Changed
- **Replaced all 33 native `window.confirm()`/`window.alert()` calls with
  an in-app async modal.** Native dialogs live outside the DOM, making
  every one of them invisible to browser-automation tools — this fully
  blocked automated regression testing at 4+ confirmed points this
  session (Excel upload, Exit deep-dive, Generate Strategy's completeness
  check, portfolio switching), each requiring a full page reload to
  recover from, discarding whatever was in flight. Real users were never
  affected by the freeze itself, but the native dialogs were visually
  inconsistent with the rest of the UI regardless.
- New `confirmAsync()`/`alertAsync()` (module-level, callable from any
  component without prop-drilling) plus a single `<ConfirmModalHost/>`
  mounted at the app root. Same call/response shape as the native
  versions (`await confirmAsync(msg)` → true/false), Escape/Enter
  keyboard support, click-outside-to-cancel on confirms.
- One functional chain (`ensureChartTokens` → `reportMarkdownForExport`
  → `downloadPortfolioReport`) had to become async together, since the
  return value was consumed synchronously — everything else converts
  1:1 with no behavioral change beyond the dialog itself.

### Note
This is the largest single-session change so far by call-site count and
has NOT been runtime-tested — every edit was applied via exact-match
string replacement (each individually verified to exist before
replacing) and the 3 most structurally complex conversions were manually
re-inspected for correct brace/statement closure, but no JS parser or
live browser was available in this environment to confirm the file
actually runs. A full live pass — ideally re-running the same Portfolio
regression prompt plus the pre-flight/negotiation-plan/Excel-upload
checkpoints specifically — is required before this is trusted, let alone
shipped further.

## v2.30.3
### Fixed
- **P2 Strategic Options generation** (Portfolio Workbench) had no `maxTokens`
  set at all — silently defaulting to 1500, same bug class as v2.30.0/v2.30.1.
  This call's schema is the largest found yet (up to 5 options × 22+ scored
  fields each), reproducibly failing 3/3. Now capped at 8000.
- **"Start fresh"** only cleared `categoryai_session`, leaving 6 other
  localStorage keys untouched (`categoryai_portfolio_strategies`,
  `categoryai_portfolio_library`, `categoryai_custom`,
  `categoryai_label_overrides`, `categoryai_tour_xy`,
  `categoryai_tour_xy_min`). Stale data in the untouched keys — e.g. from
  a prior Demo Tour run — was read straight back in on the very next load,
  producing what looked like an un-clearable phantom demo session and a
  wrong Portfolio Matrix. Now clears all session-derived keys (deliberately
  still preserves `categoryai_keys`, the saved AI provider/API key —
  that's a setting, not session data).
- **`duplicateLevel1CategoryAsChild`** only received the composition
  line's name string, not the row itself — when no matching tree node
  existed yet (the common case for a line just typed into P1), it built a
  synthetic blank parent with no notes/playbook/channel/etc. to copy from,
  so the new child's descriptive context was silently empty regardless of
  what the real composition row contained. Now receives and copies from
  the actual row.

### Changed
- Route-to-market: added a one-click "use this →" link next to each
  line's ranked channel suggestion. Previously, accepting the top
  suggestion required a separate, easy-to-miss dropdown interaction —
  the ranking text looked like a decision had already been made when it
  hadn't, so a chosen channel could silently never reach the board-paper
  report (§3) even though the underlying report logic was correct all
  along.

### Investigated, not a bug
- Route-to-market recommendations "not flowing into the .docx" (flagged
  in this session's QA report) — confirmed the report-builder logic is
  correct and correctly gated; the real gap was the UX issue fixed above,
  not a data-flow defect.

## v2.30.2
### Changed
- Renamed "Archetype" → "Playbook" everywhere it's user-facing (Admin tab,
  cost driver screen, P1 composition table, guide/help text, tour stops,
  Excel export column, tooltips) — "Playbook" is the standard procurement
  term for a pre-built sector template of cost drivers/levers/KPIs, where
  "Archetype" was borrowed design/psychology terminology. Internal code
  identifiers (`matchArchetype`, `ARCHETYPE_EXTRAS`, the `archetype` data
  field on category objects) are unchanged — renaming those would need a
  migration path for existing saved sessions and is a separate, lower-
  priority piece of work with no user-visible benefit on its own.
  Left alone: the unrelated "four offline archetypes" (independent /
  integrated / hybrid / capability-based) in the P2 sourcing-options
  screen — a different concept, not a category playbook.

## v2.30.1
### Fixed
- **Elevator Pitch generation** (Step 14, "AI-write the 2-minute pitch + 10
  FAQs") was using the default 1500-token cap like the other calls fixed in
  v2.30.0 — this specific call site was missed because it's a separate
  function/button from the main Step 14 strategy generation, even though
  both live on the same screen. Combined pitch (180-230 words) + 10
  sourced FAQ items reliably exceeds 1500 tokens. Now capped at 5000.
  Found via live regression testing on the deployed v2.30.0 build (4/4
  reproducible failures on Claude; passed on Gemini, which has no cap).

## v2.30.0
### Fixed
- **Critical:** `max_tokens` was hardcoded to 1500 on every direct Claude
  API call (both in-app and API-key modes), silently truncating JSON on
  the app's largest prompts — Generate Strategy, Negotiation Plan, and
  the Research Assistant — causing parse failures and blocking the core
  strategy/export/business-case pipeline. Now sized per call: 6000 tokens
  for strategy generation, 4096 for negotiation plan and research
  assistant. Gemini path unaffected (no output cap was ever set there).
- Negotiation Plan prompt now includes kept chessboard method names — the
  `chess` data was already available to the component but was never
  being passed into the prompt.
- Header banner and version references were still reading v2.25.0/v1.2.0
  in several places (export footers, AI guide context string) despite
  the app having shipped through v2.29.0 internally — all six user-facing
  version strings now consistently read v2.30.0.
 
## v2.29.0 (Phase B — category hierarchy)
Categories can now have children: **➕ Duplicate as child** on any node (any level) copies its descriptive context (notes, archetype, channel, specialization, coverage, supplier count, volume) — never its scores; the child always starts unassessed, exactly like any new category. New **📊 Portfolio Matrix** tab on P3 plots every node in the portfolio on one Value×Risk chart, filterable by level or all levels at once (tangled, with parent-child connecting lines), children under the same top-level category grouped by a ring color; click a bubble to open it in the Category track. New **rollup engine**: a parent with children shows a position computed from its assessed children (spend-weighted average by default, falling back to a simple average when spend data's missing, or an alternate worst-case/highest-risk-child mode) — unassessed children are excluded outright, never blended in as a default guess, with a visible "rollup incomplete" indicator when only some children have been assessed. Spend on a line with children is now derived (summed from them) rather than independently editable. Optional **UNSPSC/CPV** classification code fields on every category node — manual entry only, no lookup or validation yet.

## v2.28.0 (Phase A — category tree foundation)
Replaced the single flat "currently active category" model with a real tree: every category is a node with a stable id, and the wizard (Steps 1–14) reads from and writes to its active node's own record live, as you edit — deep-dive a category, switch to another, come back, and each one's data is genuinely its own (previously, re-opening an already-deep-dived category silently carried over most of another category's data). Added an explicit Portfolio entity as the real container above the category tree. Existing sessions migrate automatically, once, with no data loss.

## v2.27.0
AI-draft-and-review workflow for unassessed Kraljic variables: new `ai_draft` confidence state ("AI Draft — unconfirmed") with its own badge styling; "AI-draft the missing scores" reuses the Step2.assess() scoring pattern but requires explicit accept (or an edit to a different value) before a drafted score counts — re-clicking the same value is a no-op, not silent acceptance. Confidence vocabulary synced everywhere it's described: Module Review export label, About tab tooltip, and three portfolio/export narrative strings that still said "User / AI-inferred / Assumed" now include AI Draft.

## v2.26.0
FIX: generic-mode Kraljic quadrant bug — business impact was hard-pinned to the midpoint whenever internal data was skipped, making Bottleneck/Non-critical mathematically unreachable; now always derived from the actual internal variables. FIX: a saved/imported session missing a variable (schema drift) threw and white-screened the app with no recovery — added a normalizeVars() merge-on-load and a React error boundary as a safety net. Added a visible "not yet assessed" state (banner, dashed/hollow marker, "(assumed)" axis labels) so an unscored category no longer looks like a real Strategic placement. Step2's AI market assessment now names which variables it didn't return a usable score for, instead of silently leaving them unchanged.

## v2.25.0 (Route-to-market engine)
New rule-based route-to-market recommendation panel beneath P1 Composition:
ranks the 4 default channels (MSP/VMS, Niche/Specialist Consultancy,
Contingent/Temp Labour, RFx) per line. Kraljic quadrant is the primary
signal; specialization, volume/frequency, existing panel coverage, and
credible-supplier-count are modifiers on top of a base score per
quadrant×channel. Pure and rule-based by design — an optional AI
narrative layer can sit on top later without changing the underlying
contract. Recommendations are ranked suggestions, never locked; the
category manager always makes the final channel choice. Channel library
is Admin-extensible.

## v2.24.0
About tab rebuilt as a numbered, paginated deck (8 sections, one page at
a time) with clickable page dots and Prev/Next, instead of one long
scroll. Resets to page 1 each time About is reopened.

## v2.23.0 (+ v2.23.2 fix)
Tour card made freely draggable (drag the header anywhere; position
clamped to the viewport and remembered per browser), with a sensible
default position (top on mobile so it never covers the bottom action
buttons; bottom-right on desktop) until the user drags it themselves.
v2.23.2 fix: dragging then releasing was immediately followed by a
browser-generated "click" on the same element — the drag-vs-click guard
was clearing itself synchronously on release, so it read as already gone
by the time the spurious click fired, causing every drag to also
re-expand the minimised tour card right after moving it. Fixed by
clearing the guard one tick later instead of synchronously.

 ## v2.22 — no trace found in code comments or commit history; likely a
version-number skip, or content that left no recoverable detail.

## v2.21.2 (frozen)
FIX: demo tour blanked when crossing from the category stops to the portfolio stops — a stray comma in the tour array (introduced v2.12) created a JavaScript array hole, so the 17th stop was `undefined`; legal syntax, invisible to static checks, found by driving the full tour in a real headless Chrome (now a regression harness). Tour is now explicitly two-part: "Part 1 · CATEGORY tour (stops 1–16)" then "Part 2 · PORTFOLIO tour", with the handover announced at the Part-1 completion stop.

## v2.21.1 (frozen)
Minimum-path strip rendered above all routes (portfolio strip was below the fold).
## v2.21.0
Collapsible + clickable workbench headers; persistent per-workbench minimum-path strips (portfolio chips / category pills 1–14) with current-highlight and done-ticks; Deepen chip after Composition.
## v2.20.0
P2: four titled stages with From/Feeds lineage (Stage 2 finally titled); P1 banner titles match chips; chips clickable; two-workbench nav; guides synced.
## v2.19.0
Flow audit: 🚦 guided start, P1 minimum path, Step-14 Outputs divider, OUTPUT nav order (strategy before optional 7Ps), ➕ add-as-new-line (standalone category joins portfolio).
## v2.18.0
Workspace identity (👤 name, stamped exports), handoff-aware import confirm, About "Data & devices".
## v2.17.x
Chart-token regex fix (digits — literal `@@CHART:catforces5@@` bug); ATK wording honesty ("similar to"); VM business case primary; PowerPoint matched to Word (pitch-first, chart images); 🗂 My template language (51 renameable labels, both accepted on upload); guides/About/tour synced; to-do box honest statuses.
## v2.16.0
Business case in both formats: Value Management template (stakeholders → opportunity → benefits delivery plan L1/L2/L3 → project economics Capex/Opex → risks & alternatives incl. do-nothing) and Five Case Model — assembled from session data, `[To complete]` for named accountability; tested full+empty.
## v2.15.0
🧾 Document composer; pre-generation preflight; traditional Five Forces + chessboard selection funnel; 💡 Options & opportunities engine (Portfolio/Category levels); 2× chart resolution; pitch first, FAQ last.
## v2.14.0
Standalone↔portfolio loop (view-existing reminder, end-of-flow update with stamp); 7Ps honesty; five category charts + table upgrades; research wired into SWOT/PESTLE (sequence fix).
## v2.13.0
Portfolio frozen at v2.12.0; category audit vs management documents (decision-first reorder); duplicate-work guard.
## v2.12.0 (portfolio freeze)
Word input template round-trip (blank/prefilled, mammoth parse); professional .docx styling; P3 numbered download flow; sticky deep-dive reminders.
## v2.0–v2.11 (portfolio build)
Charter/fact base/plans/composition; strategic questions; options+matrix+risk heat; roll-up engine; library; Excel round-trip & doc ingestion; declarations; 12-section board paper with canvas charts; exec summary; edit-&-confirm single source.
## v1.2.1 (baseline, frozen)
Category track 1–14, demo tour, module reviews, PPT deck, ConfCell confidence flags.
