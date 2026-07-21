# Category AI

An AI-assisted end-to-end category management suite — applying portfolio
and competitive positioning frameworks (Kraljic-style tiering, Porter's
Five Forces, and an original 64-cell purchasing chessboard) to procurement
category strategy, with AI-assisted scoring throughout.

## What it does

- Takes category/spend inputs and guides the user through a structured
  positioning exercise (see `METHODOLOGY.md` for the underlying model)
- Produces a visual quadrant/matrix placement for a category, in the spirit
  of a Kraljic-style portfolio view, adapted with AI-assisted scoring
- Includes an original 64-cell purchasing chessboard tool — conceptually
  related to, but independent of, A.T. Kearney's trademarked Purchasing
  Chessboard® (see `METHODOLOGY.md` and `docs/THIRD-PARTY-NOTICES.md` for
  the full attribution/trademark note)
- Surfaces suggested category strategy directions based on quadrant
  placement
- Exports and reporting support via CDN-loaded libraries (docx, pptxgenjs,
  PapaParse, pdf.js, JSZip, mammoth) — see `docs/THIRD-PARTY-NOTICES.md`

## Status

Live. Actively developed — see `archive/` for prior version snapshots
(`v1.1.0`, `v1.2.0`, frozen releases) kept for reference.

## Tech stack

Single `index.html` front end (React via CDN, Babel Standalone), no build
step required. AI-assisted scoring via Claude/Gemini. Hosted via GitHub
Pages.

## How to run locally

Download and open `index.html` directly in a browser — no install or
server required.

## Development note

Development assisted by Claude Code (Anthropic) under my direction. The
methodology, product design, and domain expertise reflected in this tool
are my own — see `METHODOLOGY.md` for the original framework.

## Related

- [`METHODOLOGY.md`](./METHODOLOGY.md) — the strategic frameworks this tool
  applies (Kraljic, Five Forces, purchasing chessboard) and how the AI
  layer adapts them
- [`docs/`](./docs) — user, admin, and reference guides, plus third-party
  notices
- [`archive/`](./archive) — prior version snapshots
