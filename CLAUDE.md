# CLAUDE.md

Persistent context for Claude Code sessions in this repo. Read this before
starting work.

## Who this repo belongs to

Owned by Vijay L Narasimhan (GitHub: rags1816). Part of a wider portfolio
of applied tools — see the hub page at https://rags1816.github.io for the
full list. Each repo is independent but follows the same conventions below
for consistency across the portfolio.

## Repo structure convention

- **Root** — only the live app file(s) (e.g. `index.html`), `README.md`,
  `METHODOLOGY.md`, `LICENSE`, `.gitignore`. Keep root clean; nothing else
  belongs there.
- **`docs/`** — user guides, admin guides, reference guides, and any
  supporting documentation not needed to run the app.
- **`archive/`** — superseded versions, old HTML/app snapshots, deprecated
  scripts. Kept for history, not deleted, unless confirmed genuinely
  redundant (e.g. a byte-identical duplicate).
- **`tools/`** — utility/build scripts still actively used, if any (keep
  separate from `archive/`, which is for scripts no longer used).

## Documentation files — what each one is for

- **`README.md`** — what the app does, current status, tech stack, how to
  run it. Must end with a **Development note** section (see below) and a
  **Related** section pointing to METHODOLOGY.md.
- **`METHODOLOGY.md`** — the original framework/methodology behind the
  tool. This is the IP-protection document — states origin, credits any
  established frameworks the tool builds on (with clear attribution, e.g.
  Kraljic, Porter's Five Forces), and describes the original contribution
  clearly separated from the credited frameworks.
- **`LICENSE`** — explicit "All Rights Reserved" copyright, present in
  every repo individually (do not rely on inherited/default licensing —
  confirmed unreliable across this portfolio; always add the file
  directly). Exception: Raaga, which is deliberately MIT-licensed.

## Standard "Development note" section for README.md

Every README ends with this section, verbatim, before "Related":

```markdown
## Development note

Development assisted by Claude Code (Anthropic) under my direction. The
methodology, product design, and domain expertise reflected in this tool
are my own — see `METHODOLOGY.md` for the original framework.
```

## Workflow rules — always follow these

1. **Never commit without showing a diff first and waiting for explicit
   confirmation.** A stop-hook nudge about uncommitted changes is not
   confirmation — only an explicit go-ahead from Vijay counts.
2. **Never force-push** without explicit, separate confirmation — treat
   this as a distinct, higher-caution action from a normal push.
3. **Before any file reorg**, check whether files referenced by the live
   app (script tags, asset paths, sound files, etc.) would be affected.
   Search the app file for references before moving anything that could
   plausibly be a runtime dependency. Report findings before moving, don't
   assume.
4. **Work happens on a feature branch, then via PR into `main`.** Direct
   pushes to `main` should be avoided — branch protection may not be
   enabled on all repos yet, but the convention is PR-first regardless.
5. **After a PR merges, the remote feature branch is not auto-deleted.**
   Flag it and offer to delete it — if deletion 403s (a known permission
   gap with the current GitHub App install), tell Vijay to delete it
   manually via the repo's Branches page rather than retrying.
6. **Never hardcode API keys, passwords, or secrets into any file.** Keys
   are supplied at runtime (env vars, UI input, or session input) — this
   is a firm project-wide rule, not a per-repo preference.
7. **Flag, don't silently fix, anything that looks like real personal
   data, credentials, or PII** in any file being touched — stop and ask
   before proceeding, even if it seems like test data.

## Known environment quirks

- The GitHub App integration can push and merge but **cannot delete
  branches** (consistent 403) — this is expected, not a bug to keep
  retrying.
- Commit signing may show as unverifiable in local hooks even when the
  actual signature is present and GitHub verifies it server-side after
  push — don't treat a local signing-check failure as blocking on its own.

## When in doubt

Report findings and ask, rather than assuming — this repo (and the wider
portfolio) prioritises careful, reviewed changes over speed.

---

# CategoryAI — Project-Specific Notes (addendum to root CLAUDE.md)

Read this alongside the standard portfolio-wide CLAUDE.md conventions.
These are lessons learned the hard way during the Phase A/B integrity
overhaul — treat them as binding, not optional.

## Commit discipline — non-negotiable

**Commit locally the moment a step passes its own tests and has been
reviewed in chat — even if explicit "proceed" hasn't been given yet.**

This project lost a full completed, tested step (Phase A Step 1) to a
container reset because it was held uncommitted across a turn boundary
while waiting for review. Local commits are cheap and reversible; leaving
tested, working code uncommitted is not durable in this environment.

- Commit locally as soon as tests pass and the diff has been shown.
- Do NOT push, open a PR, or merge without explicit confirmation — that
  gate still applies.
- If asked to hold before committing (e.g. "show me the design first"),
  still commit the moment testing confirms the design works — "hold" means
  don't push/merge, not "leave it uncommitted."

## Core trust principle — never blend unassessed data into a real result

This app's entire value proposition is that a placement, score, or rollup
means what it says. Multiple bugs fixed in this project were all the same
underlying mistake in different forms:

- A default value must never be indistinguishable from a real assessment.
- An AI-drafted value must never count until explicitly reviewed and
  accepted — re-selecting an already-chosen value does not count as review.
- An unassessed child must never be blended into a parent rollup as a
  default-midpoint guess — exclude it, and show a visible "X of Y not yet
  assessed" indicator instead.

Any new feature touching scoring, confidence states, or rollups must be
tested against this principle explicitly, the same way the AI-draft
review gate and the rollup exclusion logic were.

## Data model — current shape (post Phase A/B)

- Categories are a tree, up to 4 levels deep (Category → Sub-category →
  Sub-sub-category → Item/commodity), under a Portfolio entity.
- Every node has a stable id. Do not reintroduce name-keyed lookups —
  this was a real, confirmed bug source (duplicate-named children became
  unreachable) before ids existed everywhere.
- A node with children never carries its own manual score — its displayed
  position is always the rollup of its children, even if it was
  individually scored before children were added. A stale individual
  score is more misleading than an honest "incomplete" state.
- `treeToLegacyStrategiesBlob` and related export/report logic are
  currently Level-1-only — sub-category assessments do not yet feed the
  exported strategy report. This is confirmed, current scope, not a bug.
  Check this file's own comments before assuming it's been fixed.

## Testing convention for this repo

- Use Playwright against a locally-served copy with local UMD copies of
  CDN dependencies (this sandbox blocks cdnjs.cloudflare.com) — don't
  assume network access to real CDNs during testing.
- Test realistic user paths, not just isolated unit checks — most real
  bugs found in this project (the exit-deep-dive race condition, the
  cross-category field leak, the duplicate-naming collision) were only
  caught by walking an actual multi-step user journey, not by testing
  functions in isolation.
- `page.reload()` re-runs `addInitScript` and silently reseeds
  localStorage with the pristine test seed — a known test-harness gotcha,
  not an app bug. Use in-app navigation instead of reload when testing
  persistence.
- Autosave is debounced ~600ms — wait for it before reading localStorage
  in a test, or you'll read a stale pre-save snapshot.

## Known, confirmed scope boundaries (do not silently "fix" without asking)

- Only one live Portfolio is supported today. The Portfolio entity exists
  in the data model to support more in future; switching/comparing
  multiple live Portfolios is explicitly not built.
- UNSPSC/CPV codes are manual-entry only — no lookup, no validation, no
  AI suggestion, and not copied when duplicating a node as a child
  (deliberate — a copied code is more likely wrong than helpful).
- Sub-category detail doesn't feed the exported report (see above).

If any of the above changes, update this file and the in-app About tab /
STEP_GUIDE chat context together — do not let the app's own documentation
and its in-app AI assistant's knowledge drift apart again (this happened
once already and required a dedicated consistency-pass step to fix).
