# Changelog

## [1.1.0] — 2026-07-14 (frozen)

Rebrand release: **ProcureAI Strategic Category Suite** is now **CategoryAI Strategic Category Suite**.
Four features selectively ported from the CategoryAI v2.0 comparison build (Vite/TS), following a
feature-parity audit which confirmed v1.0 as the product of record. Sandbox offline mode, originally
scoped as a fifth port, was found already present (and superior) in v1.0 — no change was needed.

### Changed — rebrand (patch 1)
- All branding renamed CategoryAI: title bar, header, version badge, Word document header,
  PowerPoint deck footer, chessboard open-board attributions, in-app guide context
  (guide identifies itself as "formerly ProcureAI v1.0").
- localStorage keys renamed (`categoryai_session` / `categoryai_keys` / `categoryai_custom`)
  with a one-time, non-destructive migration from the old `procureai_*` keys. A v1.0 build
  opened later still finds its data.
- Session files now stamped `categoryai-session-v1`; the importer accepts both old and new
  formats, so v1.0 session JSON files load cleanly.

### Added — SRM post-contract review (patch 2, fix 2b)
- New SRM review panel on step 7: date-stamped supplier performance reviews on the five
  scorecard dimensions, radial gauge, four-tier grading (Executive leader ≥90 / Preferred
  partner ≥70 / Transactional ≥50 / Improvement plan <50).
- Reviews accumulate as history and never overwrite the strategic scorecard.
- Persisted in autosave and session JSON; exported to the strategy document as an
  "SRM review history" table.
- **Fix (2b):** gauge circles were invisible — SVG presentation attributes reject CSS
  `var()`; replaced with concrete palette hex values and hardened the label overlay.

### Added — savings ledger upgrade (patch 3)
- Status funnel bar on step 13, weighted by planned % (Idea → Validated → In delivery → Delivered).
- Complexity (Low/Medium/High) and Owner columns on pipeline rows; AI generation and sandbox
  data supply complexity; pre-existing rows default to Medium/blank.
- Approximate annual spend fallback: indicative £/$ value columns without a spend CSV,
  clearly flagged as an assumed baseline in-app and in the Word export. An uploaded CSV
  always takes precedence.
- Complexity and Owner added to the strategy document and Module Review exports.

### Added — staged maturity checklist (patch 4)
- 12-practice, 4-stage checklist (Foundational / Developing / Established / Leading practice)
  in the style of CIPS/Hackett maturity models, on step 13 alongside the existing 1–5
  self-assessment. Stage is awarded only on complete, consecutive stages — no skipping.
- Progress strip with stage label, completion bar and n/12 count; persisted; exported to the
  strategy document once at least one practice is ticked.

### Changed — navigation & tour polish (patch 5)
- Nav rail phases are collapsible with per-phase completion counts (e.g. "STRATEGY 3/5 ✓");
  only the active phase opens by default, and it cannot be collapsed.
- One-line hover help on every step button, combined with completion status.
- Demo tour card gains a minimise button (– / floating "Tour n/16 — show" pill), keeping the
  user's place — primarily for mobile. New controls carry aria-labels.
- Step buttons slightly more compact.

### Checksums (SHA-256)
```
a250920a354386dc6645be9bdc9188fd64a2a74c483c8665de3699fa64873d5c  categoryai-strategic-category-suite-v1_1_0.html
```

### Upgrade notes
- No breaking changes. v1.0 sessions (localStorage or exported JSON) load without action.
- Old `procureai_*` localStorage keys are copied, not deleted, on first launch.

## [1.0.1] — 2026-07-12 (frozen, as ProcureAI)
- Demo tour crash at stop 4 and three sibling bugs fixed (SWOT/PESTLE data normalised to
  per-key `{text, conf}` shape).

## [1.0.0] — 2026-07 (as ProcureAI)
- Initial frozen release: 15-step sourcing workflow, sandbox mode, exports, demo tour, admin panel.
