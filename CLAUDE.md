# CLAUDE.md

Context for Claude Code (or any AI agent) picking up work on this repo.
Read this before touching `index.html`.

## What this is

CategoryAI: a single-file (`index.html`, ~10,650 lines), browser-based
procurement category management application. React + Babel-standalone
+ PapaParse + pptxgenjs + SheetJS (xlsx) + docx, all loaded via CDN —
**no build step, no bundler, no package.json**. Deployed as a static
file on GitHub Pages: `https://rags1816.github.io/CategoryAI/`.

Two independent workbenches: **Category Workbench** (Steps 1-14, one
category's full strategy) and **Portfolio Workbench** (P1-P3, a
cross-category charter/roll-up/board paper). They connect only by user
choice (deep-dive, duplicate-as-child).

## Architecture essentials

- **State model**: every category is a node in `categoryTree`
  (`newCategoryNode()` shape), each holding a `record` (`defaultRecord()`
  shape — profile, vars, suppliers, risks, chess, nego, exec, value,
  strategy, etc.). The active category is `activeNodeId`; `activeRecord`
  derives from it. All field bindings go through `bindField(key)` —
  `const risks=activeRecord.risks, setRisks=bindField("risks")`.
- **A name lives in two different places** — this has caused two real
  bugs already (v2.38.0-v2.38.2). `node.name` (top-level) is ONLY
  populated via Portfolio-linked flows (deep-dive, duplicate-as-child).
  The name a user types on Step 1 lands in `node.record.profile.name`.
  Any code reading "the category's name" needs to check both, preferring
  the record-level one — see `nameOf()` in `CategorySwitcher` for the
  reference implementation.
- **AI calls**: `askAI()`/`askClaude()` centralize provider routing
  (Claude in-app / Claude API key / Gemini / Sandbox). Every AI call
  site has its own tuned `max_tokens` — this was a real, serious
  historical bug (hardcoded 1500 truncating everything); check the
  changelog before ever touching this again.
- **Excel round-trip**: `findCol(...)` matches by header TEXT, not
  position. **If headers can't be recognized, refuse the import
  entirely — never fall back to guessed positions.** An earlier version
  guessed positions and silently corrupted data (a deleted column
  shifted every field left). This is now the established, non-
  negotiable pattern for every sheet in both the Category and Portfolio
  templates.
- **Chart embedding in exports**: `@@CHART:id@@` tokens in markdown get
  resolved into real images by `mdToDocxChildren` (see `downloadAsWord`),
  reading from `window.__docxCharts[id]`. Chart builders (`build*Chart`
  functions, top-level, data-parameterized, not closure-bound) populate
  this registry. To add a chart to any export: build/reuse a
  `build*Chart(data)` function, register it into `window.__docxCharts`
  before the download call, and add the matching token to the markdown.
- **Confirm/alert**: no native `window.confirm`/`window.alert` anywhere
  — use `confirmAsync(message)` / `alertAsync(message)`, the async
  in-app modal system (`ConfirmModalHost`, mounted once at App root).

## Non-negotiable patterns, learned the hard way this cycle

1. **Regeneration must never silently discard data.** Either genuinely
   accumulate (Chessboard, Research Assistant — new results merge with
   old) or confirm-before-overwrite (Negotiation Plan, Execution Plan,
   Risk, ESG). A wholesale silent replace was a real, serious bug found
   in 5 places at once.
2. **Collapse output, never collapse input.** If you add a new step
   section, decide honestly which category it's in before wrapping it
   in `<Collapsible>`. Active editing surfaces (scorecards, Gantt/RACI,
   anything with "+Add" buttons) and anything with actionable alerts/
   warnings must stay visible by default. Only AI-generated review
   content collapses.
3. **Secrets never sit in the DOM longer than necessary.**
   `type="password"` only masks *visual rendering* — it does NOT stop
   accessibility-tree snapshots (used by browser automation tools) from
   reading the raw value. Once a credential is saved, show a masked
   summary (`KeyField` component) and only let the real value re-enter
   the DOM during active editing. This was a real, repeated (5+ times
   in one session) exposure pattern before the fix — do not reintroduce
   a plain bound `<input value={secret}>` anywhere.
4. **Verify structural balance after every edit** — but not with a
   naive whole-file brace/paren count. String literals (JSON schema
   examples in AI prompts, emoji-adjacent text) throw off raw counts
   and produce false positives. The reliable method: walk brace depth
   from a specific function's actual body-opening `{` (found via the
   character *after* the parameter list's closing `)`) to where depth
   returns to 0. See any `python3 -c "..."` block in the changelog
   history for the exact technique. When in doubt, compare against the
   previous known-good baseline file — an identical discrepancy in both
   versions means it's a pre-existing artifact, not something you
   introduced.
5. **Live-test claims before writing them into guide text.** This
   session's Developer/Guide-chat text had at least 3 confirmed false
   claims ("no AI button exists" when one did; "PESTLE is on page 2 of
   the CEP" when it never was) — all from trusting a remembered
   description instead of re-checking the actual function. Grep the
   real code before describing what a screen does.

## Where things are

- Step→title mapping, in order, both workbenches: `STEPS` array
- Per-step AI chat knowledge base: `STEP_GUIDE` object (`kb:` field —
  check this isn't an empty string if a screen's guide answers seem
  vague; it has been, at least once)
- Master cross-cutting AI context: the `APP-WIDE CONTEXT (v...)` string
  inside the guide-chat prompt builder — has a numbered "NEW in this
  build" list; add a new numbered item for any release-worthy feature,
  don't let it go stale (it did, for 3 minor versions, before v2.38.5)
- Demo Tour stops: `TOUR` array
- About tab content: `AboutScreen` function

## Testing discipline

Every fix in this codebase's history that shipped without a live check
turned out to have at least one issue found on the next real test. The
established minimum bar:
- Structural balance check (above) before any version bump
- A live re-check with **quoted evidence** (exact values observed, not
  "looks right") for anything touching calculation, data parsing, or
  navigation
- Re-test the SPECIFIC thing that failed, not just "did the app load,"
  after any fix — several "fixed" claims in this history needed a
  second round because the first fix addressed a symptom, not the root
  cause

See `CategoryAI_Testing_Guide.md` and `CategoryAI_EndToEnd_Test_Script.md`
for reusable test templates. See `METHODOLOGY.md` for the full patch→
verify→freeze→checksum workflow.

## Don't

- Don't add a new native `window.confirm`/`alert`/`prompt` call
- Don't bind a secret's raw value directly to an always-rendered input
- Don't guess a fallback column position when Excel headers don't match
- Don't claim a screen "can't do X" or "has no button for Y" without
  grepping the actual function first
- Don't trust a whole-file brace/paren count as evidence of a real bug
  without checking it against the pre-edit baseline first
