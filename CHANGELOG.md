# CategoryAI — Changelog

## v2.39.1
### Fixed
- **Session export/import didn't carry Admin-panel customizations across
  devices** — confirmed via source: `categoryai_custom` (custom
  playbooks/archetypes), `categoryai_portfolio_library` (saved portfolio
  templates), and `categoryai_label_overrides` (custom terminology) each
  have their own separate localStorage key and load/save functions, and
  none were included in `sessionPayload()` or `importSession()`. A
  session file would restore all category/portfolio work perfectly, but
  any strategy referencing a custom playbook would land on a device
  where that playbook simply didn't exist.
- Fixed at the export/import boundary specifically, not by changing
  `sessionPayload()` itself — that function also backs frequent
  same-device autosave, and these three keys already persist
  independently there, so bundling them into every autosave would just
  be redundant duplication. Only the explicit cross-device export now
  bundles all three; the confirm-before-import dialog now says so
  explicitly when a file carries them.
- `App()` confirmed to have **zero** pre-existing brace/paren
  discrepancy (unlike `Step5`, which has a known harmless one) — checked
  both before and after this edit, genuinely balanced in both cases.

## v2.39.0
### Added
- **Five Forces and Supplier landscape charts now embed in the 2-page
  CEP export** — previously the CEP was text-only, no charts at all.
  Reuses the exact same chart-builder functions already used for the
  main strategy document (`buildForcesTraditionalChart`,
  `buildSupplierScatterChart`), not new chart-rendering code.
- **On-screen preview now shows the same real chart images the
  download will contain** — new `populateCepCharts()` helper shared by
  both the preview toggle and the download button, so what you see in
  preview genuinely matches what downloads. `renderCepPreview` extended
  to resolve `@@CHART:id@@` tokens into real `<img>` elements (falls
  back to a "[chart not yet available]" note if somehow called before
  population).
- **Disruptors now categorized** — Research Assistant's prompt extended
  to classify each disruption (Supply chain / Technology / Regulatory /
  Geopolitical / Economic / Market & competitive / Environmental &
  climate), and both the CEP export and the on-screen Research
  Assistant table now group findings by category instead of a flat
  list.
- **AI-drafted response suggestions for each disruptor** — the same
  Research Assistant prompt now also generates a one-sentence draft
  mitigation/response per disruption, clearly labeled "[AI draft —
  review before use]" everywhere it appears (CEP export and on-screen
  table), consistent with the app's confidence-flagging philosophy —
  never presented as a decision already made.

### Note
Category/response fields are generated once by Research Assistant and
reused everywhere downstream (CEP, on-screen table) — not regenerated
separately at CEP-download time, avoiding extra AI-call latency on a
simple document export action.
_Consolidated record. Earlier history (pre-v2.31) predates this
development cycle and isn't reconstructed here in full — this file
picks up from the point continuous, verified development began._

---

## v2.38.5 (frozen candidate)
SHA-256: `aada281cd6f3dc5d3de71c0fdbe52da3b4559a7a448fc101febe5c6baee18e1e`

### Fixed
- In-app documentation (Guide chat, Demo Tour, About tab) was stale
  relative to v2.35-v2.38's feature work — none of Find, My Categories,
  Collapsible sections, the phase banner, the CEP export, or chart
  embedding were mentioned anywhere a user or the AI guide could see
  them. All three surfaces brought current.

## v2.38.4
### Fixed
- API key masking gap closed on both remaining surfaces (Admin panel,
  first-open of either settings panel). Root cause: `saved` state
  always initialized `false` on mount regardless of whether a key was
  already persisted, so masking never engaged until an in-session Save
  happened. Fixed by initializing from actual persisted state.

## v2.38.3
### Fixed
- **Security**: API keys sat unmasked in the DOM continuously whenever
  an AI Settings panel was open — `type="password"` only masks visual
  rendering, not accessibility-tree snapshots used by automated testing
  tools. Found via 3 real exposure incidents in one session. Fixed with
  a masked-summary pattern (last 4 characters only, "Change" button to
  re-enter edit mode) — the real value only re-enters the DOM while
  actively being typed.
- Header "AI ready" status was stale relative to Test Connection
  results — could claim ready immediately after an explicit 401.

## v2.38.2
### Fixed
- The "My Categories" panel (both the header modal and a separate,
  earlier-built inline Step 1 widget) always showed "No named
  categories yet" despite real categories existing. Root cause: both
  checked `node.name` (a field only populated via Portfolio-linked
  flows) instead of `node.record.profile.name` (the field the normal
  Category Workbench flow actually populates).

## v2.38.1
### Fixed
- The header "My Categories" panel itself showed "No named categories
  yet" on first ship — same root cause as v2.38.2, caught one component
  earlier.

## v2.38.0
### Added
- **My Categories switcher** — fixed a real, confirmed gap: there was
  no safe way to run multiple independent standalone categories in one
  browser. Retyping a name on Step 1 silently renamed the active record
  in place, carrying over all its other data. New header panel: "+ New
  category" (genuinely blank, isolated), a list to switch between named
  categories, delete with confirm.
- **Collapsible sections** across most Category Workbench steps — AI-
  generated output/results collapse by default; input fields, active
  editing surfaces, and anything with actionable alerts stay visible.
  Applied to Steps 3, 4, 5, 8, 10, 11, 14, plus the Internal Data spend
  summary. Deliberately left uncollapsed where genuinely input-heavy:
  Suppliers scorecard, Chessboard, Execution Plan, Savings/Benefits
  tracking tables.

## v2.37.2
### Fixed
- The "Start here" onboarding banner: 2 of 3 buttons, plus the Dismiss
  link, never actually dismissed the banner. Root cause: banner
  visibility was computed fresh on every render from a live storage
  read, with no dedicated state — it only disappeared as an incidental
  side effect of some unrelated re-render happening to fire. Fixed with
  proper dedicated `startDismissed` state.

## v2.37.1
### Fixed
- Currency-symbol parsing in the Spend template sheet: `$1,234,567`
  silently landed as `234,567` — off by exactly $1,000,000, corrupting
  total spend, concentration share, and the downstream AI-inferred
  score. Fixed by preferring the cell's raw numeric value (when SheetJS
  already parsed it as a number) over string-based regex stripping.

## v2.37.0
### Added
- Spend folded into the Category input template as its own sheet
  (previously a separate .csv upload only) — same total/top-10/
  concentration derivation formula reused exactly, not reimplemented.

## v2.36.1
### Fixed
- Supplier scatter chart: identical capability/alignment scores
  overlapped illegibly — same chart used in the main strategy document,
  not just the new Module Review export, so this was a pre-existing bug
  surfaced by more thorough testing.
- Chessboard quadrant chart: caption text and the "Demand power" axis
  label collided (6px apart).
- Step 12's "Continue" button routed into Portfolio P3 instead of
  Step 13 — a pre-existing bug, unrelated to this session's edits,
  found only because testing happened to exercise that button.
- Inline SVG favicon added, eliminating a 404.

## v2.36.0
### Added
- 🔎 Find — header keyword search across every screen.
- On-screen CEP preview before downloading (Step 14), mirroring
  Portfolio's existing Report Preview precedent.
- Category phase progress banner (Define→Understand→Strategise→
  Source→Contract & Manage→Output).
- Chart images now actually embed in Module Review's per-module Word
  exports (previously the on-screen chart never made it into the
  download — only the data table did). New should-cost breakdown chart
  type, which didn't exist anywhere in the app before.

## v2.35.0
### Added
- 2-page Category Execution Plan export — a dense, at-a-glance summary
  distinct from the full strategy document, built from real-world
  category-management template structures (fully genericized, no
  external branding or content). Structure: spend/scope header, spend
  profile, demand & strategy, Five Forces, supplier landscape, 3-year
  plan, near-term actions, a Disruptors table sourced from Research
  Assistant findings.

## v2.34.1
### Fixed
- Category input template's scoring criteria were unexplained — every
  1-5 field just said "Score (1-5)" with no indication of what either
  end meant. Added a Read Me sheet plus inline criteria in every
  relevant column header.

## v2.34.0
### Added
- Category input template expanded to cover Contracts, Demand Forecast,
  Stakeholders (Mendelow grid), Specs & Requirements, and Supplier
  Performance (feeds the existing SRM Review history rather than
  duplicating it as a new concept).

## v2.33.0 – v2.33.6
### Fixed
Genuine, sourced fixes across a real user-submitted QA report (26
items): regeneration data-loss risk on 5 screens (now confirm-before-
overwrite or genuine accumulate, depending on the screen), Research
Assistant's missing confidence flag and narrow scope, 3 empty/incomplete
guide-chat knowledge-base entries (one was a fully empty string), Five
Forces enrichment (3 collected-but-unused variables wired in), a demo-
data persistent warning banner, a misplaced Continue button relative to
Research Assistant, an SRM bar chart missing axis labels, and a
maturity-scale wording change (Ad hoc/Leading practice → Disagree/Agree).

## v2.32.0 – v2.32.4
### Added / Fixed
- Category input template (first version): Profile, Variables,
  Suppliers, Risks — downloadable/uploadable offline round-trip.
- Fixed 3 real bugs found via live verification within a day of
  shipping: a scorecard-crash on imported suppliers missing required
  fields, malformed segmentation charts from the same root cause, and a
  genuinely pre-existing broken "+ Add supplier" button unrelated to
  this feature.
- Fixed both Excel template downloads saving with a UUID filename and
  no extension instead of a proper `.xlsx` name.

## v2.31.3 – v2.31.5
### Fixed
- The original, session-opening finding: hardcoded `max_tokens:1500`
  truncating AI responses across every call site, tuned per-endpoint
  instead. JSON-parse-failure auto-retry. All 33 native browser
  dialogs replaced with an in-app async confirm/alert system. Excel
  Composition import fixed from position-based to header-name-based,
  then hardened further to refuse rather than guess on unrecognized
  headers. Export-format unification: 4 sections that existed in
  Word/Markdown but had no PowerPoint equivalent at all, added.

---

## Freeze record

| Version | SHA-256 |
|---|---|
| v2.32.4 | `9bffcf2c9f4f8bed3d11b8aa0d0cf2d137dd0eac41289084205757cc4ef0e02f` |
| v2.34.1 | `78b86e2adcc7732052937f82093a47f79e96ecd47a58f889d08cc92cdc855880` |
| v2.36.1 | `324e0585642a5d84f4525bbdcb53e83740b484405b1ca04436aa73c3f54d4e47` |
| v2.37.2 | `d7768df5fd227622e55ef373a284b61fd4402c401c4171cc16b22f7167fbe578` |
| v2.38.4 | `8ce3caa9a51f5180abaf2f35c55fce827430356c7615194995afae96cbbe3e73` |
| v2.38.5 | `aada281cd6f3dc5d3de71c0fdbe52da3b4559a7a448fc101febe5c6baee18e1e` |

Every freeze was independently verified by hashing the actual live
GitHub file and comparing against the value recorded here — not just
trusting the local build.
