# Changelog


## v2.33.5
### Fixed — item 21, and my own earlier mistake
- **Item 21 doesn't need a new feature — it already exists.** The
  "⚡ AI-build pipeline, KPIs & maturity" button already generates
  AI-suggested savings pipeline, KPI targets, AND maturity self-assessment
  scores in one call, all editable afterward. A separate
  "⚡ AI-build benefits register" button also already exists. Both were
  incorrectly documented as absent in a guide-text edit I made earlier
  this session — I trusted your quoted paraphrase of an older chat
  response instead of re-verifying against the actual `gen()`/
  `genBenefits()` functions. Corrected, and both claims now verified
  directly against code (confirmed zero `askClaude` calls in SRM and the
  staged checklist specifically — those two claims were accurate).

### Note
This should have been caught the first time — worth flagging plainly
rather than quietly fixing it. Going forward, any guide-text claim about
what a screen can or can't do gets checked against the actual function,
not inferred from what a person remembers being told.

## v2.33.4
### Fixed — item 11 (final item, closes the full report)
- The Supplier Preferencing table had no visible confidence indicator at
  all, despite the banner right above it explicitly claiming scores are
  "flagged AI-inferred." The underlying data always had the flag — it
  just wasn't rendered in this specific table. Added a lightweight badge
  next to each supplier's name (not a full editable ConfCell, since
  `conf` is shared with the main segmentation table above — editing
  belongs there, not duplicated here).

### Note
Caught and fixed a real syntax bug introduced by this exact edit before
shipping it — the structural balance check (used throughout this
session, not just today) is not just process theatre; it found a
genuinely missing closing brace this time, not another string-literal
false positive.

## v2.33.3
### Fixed — item 6
- The "Continue to SWOT & PESTLE" button previously sat at the bottom of
  Step2's own content (the 9 market variables), rendered ABOVE Research
  Assistant on the same screen — meaning a user could click through and
  move on without ever discovering Research Assistant existed. Moved the
  button to after Research Assistant instead, so it's now the single,
  true end-of-screen action.

### Fixed — item 12 (remainder)
- SRM review's scorecard sliders showed only a bare 1-5 number, no
  indication of which end meant what. Added "Poor" / "Excellent" labels
  at each end. Checked the main strategic supplier scorecard for the
  same gap — it's a labeled table with numeric inputs, not a slider,
  so no fix needed there.

## v2.33.2
### Changed — item 22
- Category maturity self-assessment scale labels changed from
  "Ad hoc" / "Leading practice" to "Disagree" / "Agree." Kept the same
  1=worst/5=best direction as before, so nothing downstream (scoring,
  rollups) needed to change — only the wording. The separate staged
  maturity CHECKLIST's own stage name "Leading practice" is a different
  feature (categorical stage titles, not this continuous scale) and was
  correctly left untouched. Guide text updated to match.

## v2.33.1
### Fixed — Research Assistant, properly this time (item 7)
- Replaced the confirm-before-overwrite guard with genuine accumulate
  behavior, matching Chessboard's pattern: the AI is told what's already
  found and asked for different findings, new results merge into the
  existing lists rather than replacing them. Nothing is ever lost, so
  the confirm dialog is gone too — it's no longer needed. Added a
  "🗑 Clear all findings" button for a genuine reset when wanted.

### Added — persistent demo-data banner (items 3, 4)
- A shared warning now shows on every Category Workbench step whenever
  the profile name still carries the Demo Tour's "(Demo)" marker — one
  fix covering both the general request and the Market Info Hub-specific
  one, rather than duplicating logic per screen.

### Fixed — 3 more guide-text gaps
- Market Intelligence: previously said nothing about Research Assistant
  at all, despite it living on that screen — the direct cause of "is it
  only PESTLE?" confusion. Now fully explains scope, source, and the new
  accumulate behavior.
- Negotiation Plan: added explicit single-source-call transparency
  (issues matrix, trading board, and behaviours all come from the one
  call) and regenerate behavior.
- Execution Plan: added source (strategy roadmap + levers), the new
  editability, and regenerate behavior.

### Not addressed this round
- Item 22 (maturity chart wording) — your note was unclear to me, need
  clarification before implementing
- Item 6 (SWOT/PESTLE button position vs Research) — not yet investigated
- Item 11 (visible confidence badge on Preferencing chart specifically)
- Item 12 (SRM bar chart low/high axis labels)
- Items 1, 2, 21 — genuinely new scope, still deferred
- Item 15 — confirmed the button exists in code; can't resolve what you
  specifically saw without more detail from your own testing

## v2.33.0
### Fixed — regeneration data loss (5 screens)
- Risk Heatmap, ESG opportunities, Negotiation Plan, Execution Plan, and
  Research Assistant all previously wiped existing data silently on
  regenerate — no confirmation, no merge, unlike Chessboard's
  accumulate-and-tick-to-keep pattern. All five now confirm first,
  quoting exactly what will be lost, before proceeding.

### Fixed — Execution Plan had zero editable fields
- Confirmed via direct inspection (`onChange` count: 0) — the Gantt/RACI
  plan was 100% AI-regenerate-only with no way to adjust a single value.
  Added full inline editing for both the Gantt table (workstream,
  start/end quarter, owner) and the RACI matrix, matching the edit
  pattern already used on Suppliers/Risks elsewhere in the app.

### Fixed — Research Assistant
- Was missing its `conf:"ai"` flag entirely, despite the on-screen text
  explicitly claiming "findings are flagged AI-inferred in the
  document" — added the flag and wired it into the export header.
- Expanded the prompt to use `profile.notes` and `profile.pains`, not
  just category name/sector/region — more targeted research.

### Fixed — three empty or incomplete guide-chat entries
- Cost Drivers & Levers: guide text was a **completely empty string**.
  Rewrote covering playbook-vs-AI-generate, cost driver vs. lever
  distinction, and the source of savings/KPI/demand-driver/risk fields.
- Suppliers/SRM: rewrote with AI-assess source transparency, explicit
  primary (segment+spend) vs. secondary (tier calculator, contract-level)
  basis, and clarified SRM review is entirely manual/non-AI — a real
  distinction that existed in behavior but was undocumented anywhere.
- Maturity checklist: added the CIPS/Hackett-style attribution that
  already existed in code comments and the About tab, but was missing
  from this specific screen's own guide text — the actual source of the
  user's confusion.

### Changed — Five Forces enrichment
- Found 3 market variables collected on-screen but never used in any of
  the 5 Porter's Forces calculations: `geoRisk`, `priceVolatility`,
  `regulatoryIntensity`. Wired each into a directionally appropriate
  force (geoRisk → Supplier power, regulatoryIntensity → Threat of new
  entrants as a classic barrier-to-entry factor, priceVolatility →
  Competitive rivalry) and kept the guide text's dynamic source list in
  sync.

### Added
- PowerPoint Supplier segmentation slide now includes the chart image
  (previously table-only, unlike every other module slide).

### Verified, no fix needed
- Kraljic's "not yet assessed" warning banner already exists and is
  well-built (dynamic, explains exactly which axis is unconfirmed) —
  confirmed real rather than assumed broken.
- Chessboard's "AI-recommend" button exists and is correctly labelled.

### Deferred — genuinely new scope, not this sweep
- Expanding the input template to cover contract register, demand
  forecast, specs, supplier performance, stakeholder map
- A "what are we buying / capability" input feeding archetype matching
- An in-app AI-assist button for the Maturity/KPI screen (currently
  manual-only by design)
- Minor remaining copy/UX items (SWOT-above-Research ordering, floating
  guide visibility, a visible confidence badge specifically on the
  Supplier Preferencing chart)

### Note
This sweep was done via careful source verification and static
structural checks (all edited functions individually confirmed
balanced), without a live Claude Code test round, per explicit
instruction to conserve cost this time. **This means v2.33.0 has NOT
been tested live** — recommend at least a light verification pass
before treating it as stable, given the volume of real logic changes
(5 confirm guards, new Execution Plan edit UI, a scoring formula
change) in this release.

## v2.32.4 (frozen)
SHA-256: 19a0ca5b284355478ed3e25137bb426a0621b966c30245e9ae1c1662b8557f5c
Supersedes v2.32.3's freeze — fixed both Excel template downloads
saving with a UUID filename/no extension instead of a proper .xlsx
name (XLSX.writeFile()'s built-in browser-download path wasn't
reliably honoring the filename; replaced with an explicit Blob +
anchor download). Verified: both templates confirmed opening directly
in Excel with correct filenames, valid zip/XLSX structure checked
directly, no rename needed.

## v2.32.4
### Fixed
- **Both Excel template downloads (Portfolio and Category input
  templates) could save with a UUID filename and no extension instead
  of a proper .xlsx name** — found by the user directly, not by prior
  testing, which checked file contents thoroughly but never specifically
  confirmed the filename shown in the browser's download list. Root
  cause: `XLSX.writeFile()`'s built-in browser-download mechanism wasn't
  reliably honoring the filename in this environment. Replaced with an
  explicit download (manually build the Blob, set the anchor's
  `download` attribute directly) in both places, giving full control
  instead of trusting that black box.

### Note
This means your frozen v2.32.3 checksum
(90524adec1ff117e3410d3db163046e4ab3c179c3270c7d682b86261a88fb7d0) is
now superseded — v2.32.4 is the new frozen candidate, pending
verification.

## v2.32.3
### Changed
- **In-app guide text synced with the new Category input template
  feature** — the Step 1 Reference Library context and the master
  AI-wide context string both previously described Excel round-trip as
  Portfolio-only (P1). Both now mention the Category track's own
  download/upload template, so a user asking the Reference Library
  "does the category side have an offline input option?" gets an
  accurate answer instead of a stale one. Text-only, no logic changes.
- Confirmed no other stale claims: the Demo Tour (Sandbox pre-loaded
  data, doesn't touch the upload flow), Elevator Pitch guide text, and
  Admin panel tooltips were all already accurate and needed no changes.

## v2.32.2
### Fixed
- **Segmentation/preferencing charts rendered malformed (invalid SVG
  `<circle r="NaN">`) for Excel-imported suppliers.** Same class of bug
  as v2.32.1's crash — a field every other supplier-creation path
  provides (`share`, the spend-share used to size chart markers) was
  never set by the new Category input template import. Fixed at the
  source (import now sets `share:0`, matching the manual-add convention)
  and defensively at both chart render sites (`(s.share||0)`), so a
  future path with the same gap degrades to a small marker instead of a
  broken one.
- **Manual "+ Add supplier" button was completely broken — pre-existing,
  not something this session introduced.** `StepSuppliers` never
  received `setProfile` as a prop, but both its Enter-key handler and
  its "+Add" button called it anyway, throwing `ReferenceError` on every
  use with a silent no-op (typed name stayed in the box, nothing was
  added). Found only because this session's verification happened to
  exercise that specific button while checking something else. Fixed by
  threading `setProfile` through from `App()`.

### Note
Both found via the same verification discipline as the last two
patches — real, reproducible evidence, not assumption. The manual-add
bug in particular is a good example of why re-testing adjacent
functionality (not just the thing you changed) matters: it was sitting
there before any of this session's work touched that screen.

## v2.32.1
### Fixed
- **Category input template's Suppliers sheet crashed the Supplier
  segmentation screen** — found immediately in verification of the new
  v2.32.0 feature, 100% reproducible. Root cause: Excel-imported
  suppliers only carried Capability/Alignment/Notes, but the screen
  unconditionally reads `s.scorecard[dd]` (quality/delivery/cost/
  innovation/ESG) for every supplier — `TypeError: Cannot read
  properties of undefined`. Fixed at three levels: (1) Excel-imported
  suppliers now get the same default scorecard
  (`Object.fromEntries(SCORECARD_DIMS.map(d=>[d,3]))`) every other
  supplier-creation path already provides; (2) the actual crash site now
  guards against a missing scorecard regardless of cause — found in the
  process that the AI-assess path spreads the AI's raw JSON response
  without guaranteeing a scorecard field either, so this protects that
  path too, current and future; (3) the two document-generation
  dereferences (Module Review export, main Supplier segmentation table
  in `buildMd()`) got the same guard, since a document-export crash from
  the identical root cause would be at least as bad as a screen crash.

### Note
Caught within the same session the feature shipped, via the
comprehensive verification prompt rather than a separate later report —
this is what that verification standard is for.

Comprehensive verification on CategoryAI v2.32.0 at
https://rags1816.github.io/CategoryAI/ (confirm header version). Use
Claude · API key from C:\Users\DELL8\OneDrive\Desktop\Procurement
Category Management\.env. Never print/log the key.

This is the FINAL check for this session — covers everything patched
since the last full verification, in one pass. Don't re-test anything
outside this list; it's already confirmed solid.

1. NEW: Category input template (Step 1)
   Fill a category partially (name, sector, 2-3 variables, 1 supplier,
   1 risk). Click "⬇ Download input template" — confirm a real .xlsx
   downloads with 4 sheets (Profile, Variables, Suppliers, Risks) and
   your entered data appears correctly in it. Edit the file: add 3 more
   variable scores, add 2 more suppliers, add 1 more risk, change the
   sector. Upload it back via "⬆ Upload filled template" — confirm the
   pre-apply dialog shows correct counts, and after applying, all the
   new data is genuinely reflected in the wizard (check Step 1 fields,
   the Variables step, Suppliers step, Risks step).
   Then: delete the header row entirely from the Variables sheet in a
   fresh copy, upload it. CHECK: does it correctly refuse to import that
   sheet with a clear warning (matching the Excel corruption fix from
   earlier this session), rather than silently misreading scores?

2. NEW: PowerPoint export completeness (4 previously-missing slides)
   Build a category with PESTLE generated, Research Assistant run, ESG
   opportunities generated, and a full assumption register (several
   variables scored). Generate Strategy, download PowerPoint. CHECK: all
   4 slides now present — "PESTLE", "Research findings", "ESG & social
   value opportunities", "Assumption register — core variables" — each
   with real content, not empty tables.

3. RE-CONFIRM: Excel corruption fix still holds (Portfolio)
   Quick re-check only, not the full adversarial suite from before:
   delete a column from the Portfolio Composition template, upload it,
   confirm it's still refused (not silently misimported).

4. RE-CONFIRM: Duplicate-as-child still holds (Portfolio)
   Quick re-check: duplicate a line with real notes/playbook as a child,
   open the child, confirm real inherited text still appears (not
   placeholder content).

Report as: Confirmed Working (with concrete evidence — exact values
observed, not just "looks right") or Issue Found (exact repro + exact
problem). This should be the last verification round needed before this
version is considered stable.

## v2.31.4
### Fixed
- **Excel import: the v2.31.3 warning informed but didn't prevent the
  corruption it warned about.** When column headers couldn't be
  recognized, the importer still fell back to guessed positions — a
  deleted "Service line name" column shifted every field left, landing a
  spend number as literal text in the name field. Spend/Risk/Kraljic
  happened to survive because they fail type/enum validation and fall
  back safely; the free-text name field had no such guard. Now: if
  headers can't be recognized, **nothing is imported from that sheet at
  all** (same as "no sheet found") rather than guessing — the warning is
  now actually protective, not just informational.
- **Duplicate-as-child: real notes/playbook weren't appearing on the
  child's Category profile — a different bug than the one fixed in
  v2.30.3, not a regression of it.** The v2.30.3 fix correctly stores
  notes/archetype/channel on the tree node when duplicating. But
  `customizeCategoryInWizard` (the "Deep-dive" function) built the
  child's profile from `portfolioDetails.categories` — a list children
  deliberately never appear in, by the app's own Phase B design — so
  that lookup was always empty for a child, silently falling through to
  generic placeholder defaults instead of reading the real data sitting
  on the tree node two lines above it. Now pulls `existing.notes` and
  `existing.archetype` (the tree node's own fields) first, folding the
  inherited playbook into the notes text alongside the other inherited
  context (objectives, governance, etc.) — no dedicated "Playbook" field
  exists on the profile screen to put it in directly, so this matches
  the pattern already used for everything else inherited there.

### Note
Both fixes came directly from the exception-based verification report,
which caught these with concrete evidence (network traces, exact
corrupted values, exact missing content) rather than vague suspicion —
worth continuing that standard for future verification passes rather
than accepting a "PASS" without evidence behind it.

## v2.31.3
### Fixed
- **Excel Composition sheet import mapped columns by fixed position, not
  header name** (the Charter sheet already did this correctly — this
  brings Composition in line with it). A deleted or reordered column
  previously shifted every field silently: names showed as raw spend
  numbers, spend silently zeroed, risk/Kraljic fell back to arbitrary
  defaults — with zero warning anywhere in the import flow. Now matches
  columns by their actual header text (accepting both "Playbook" and the
  pre-rename "Archetype" for backward compatibility with older
  downloaded templates); if the header row can't be recognized at all,
  a clear warning is now shown before import rather than silent
  corruption.
- **Incomplete strategy exports gave no self-declaring indication of
  their own incompleteness.** A .docx/.pptx/.md downloaded without a
  completed Generate Strategy run looked structurally clean and
  complete — real headings, real content, real charts — with the only
  trace being a small "GENERIC MODE" tag and text buried in a table.
  The in-app warning dialog only protects the person downloading; once
  shared or forwarded, nothing in the file itself told a reader they
  were looking at a partial export. All three export formats now open
  with a bold, explicit "⚠ DRAFT — Generate Strategy has not been run"
  notice listing exactly what's missing, whenever `strategy` is empty.

### Note
Both were found via the impact-assessment pass, not routine testing —
worth keeping that kind of deliberate "what happens if this data is
adversarial or incomplete" check as a standard part of pre-rollout review
going forward, not just happy-path regression.

## v2.31.2
### Fixed
- **Intermittent JSON parse failures on AI generation** — root-cause was
  distinct from the max_tokens truncation bug fixed in v2.30.x, despite
  producing an identical-looking error message. Confirmed by the failure
  position: it occurred at ~2400 tokens against a 10000-token ceiling —
  far too early to be truncation. This is the model occasionally emitting
  a stray character that breaks `JSON.parse()` on an otherwise-complete
  response — a known class of issue with prompted (not schema-enforced)
  JSON generation. `askAI()` now retries once, automatically, specifically
  when the failure looks like a JSON parse error (not on network/auth
  errors, where a retry can't help). This mirrors what already happened
  organically in testing: the two attempts immediately following a
  failure both succeeded cleanly on fresh generation.
- **Overclaiming "References & Bibliography" text** — the About tab and
  AI Settings panel both stated "each strategy report closes with a
  References & Bibliography," but this section only exists in the
  Portfolio Workbench's board-paper report (§12) — it was never built for
  the Category Workbench's Step-14 document. Text corrected to say
  "Portfolio strategy report" specifically. Also fixes a mistake I
  introduced in v2.31.1's own warning banner, which incorrectly listed
  "References" as a category-doc section that could go missing — it was
  never a real section there to begin with.

### Note
The retry fix should meaningfully reduce (not necessarily eliminate) the
intermittent failure rate — it's a mitigation for a known LLM-JSON-
reliability pattern, not a guarantee. A future, more robust fix would be
moving from prompted JSON to Claude's tool-use/schema-enforced structured
output, which guarantees valid JSON — a bigger architecture change, out
of scope for this patch.

## v2.31.1
### Fixed
- **Generate Strategy still truncating at 6000 tokens** in generic mode
  (external-data-only) with rich upstream context — traced to a real,
  confirmed cause: generic mode's prompt adds an explicit extra
  instruction ("be explicit where internal data would change the answer")
  that inflates output across nearly every section, on top of everything
  else. Not present in the traceable 3/3 reproducible failure without
  it. Raised to 10000 tokens.
- **PowerPoint export was missing the Commercial 7Ps slide entirely** —
  not a conditional bug, a pure omission; `sevenPs` was never referenced
  anywhere in `downloadPpt()`, even though the .docx builder correctly
  includes/excludes it via the composer toggle. Added, using the exact
  same gating condition (`hasSevenPs && inc("sevenps")`) the .docx
  already uses, so both formats now agree.

### Changed
- Added a visible warning banner + a confirm-before-download step when
  downloading the Word document without a completed strategy synthesis.
  Previously, a failed/never-run Generate Strategy silently produced an
  incomplete .docx (missing ~5 sections — Chessboard, Cost drivers,
  Supplier segmentation, Risk register, References) with no indication
  anything was wrong, while .pptx and .md happened to render complete
  because they pull that content from raw module data independently
  rather than through the same synthesized object. This doesn't unify
  how the three formats source their data (a bigger, separate piece of
  work) — it makes the existing gap visible instead of silent.

### Investigated, not fixed this pass
- The three export formats (.docx, .pptx, .md) source some sections
  from the AI-synthesized `strategy` object and others from raw module
  data, inconsistently across formats — this is why they can diverge in
  completeness when synthesis fails. A deeper fix (making all three pull
  from the same source consistently) is a real, valuable piece of work
  but bigger in scope than this session's fixes; flagging for a future
  dedicated pass rather than rushing it here.

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
