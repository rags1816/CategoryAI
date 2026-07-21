# Category AI — Methodology

## Origin

Developed by Vijay L Narasimhan, 2025–26, drawing on 20+ years of category
management practice at BP (indirect category portfolios, $800m+), Shell
(global category strategies), and NESO (digital procurement platform,
Procurement Act 2023 compliance) — where category positioning was
traditionally done manually in workshops using static Kraljic-style
matrices.

## Problem this solves

Traditional category positioning (Kraljic matrix, Five Forces-style
supplier power analysis, purchasing chessboard exercises) is typically a
manual, workshop-driven process — slow to run, dependent on facilitator
expertise, and rarely revisited once done. This tool applies AI to speed up
and structure that positioning exercise, and to make it easier to revisit
as category conditions change, without needing a full workshop each time.

## Built on / credited frameworks

- **Framework: Kraljic Portfolio Matrix** (Peter Kraljic, 1983)
  - What it contributes: the core two-axis logic — supply risk vs. profit/
    business impact — used to classify categories into strategic quadrants
    (Strategic, Leverage, Bottleneck, Non-critical)
  - How this tool adapts it: replaces manual scoring with AI-assisted
    weighting of inputs (spend data, supplier market conditions, switching
    cost signals), so positioning can be generated and refreshed rapidly
    rather than fixed at a single workshop point in time

- **Framework: Porter's Five Forces** (Michael Porter, 1979)
  - What it contributes: structured lens on supplier market
    competitiveness/power — one of the inputs to the supply-risk axis above
  - How this tool adapts it: uses Five Forces as a background scoring input
    (not a separate output) to inform the AI's supply-risk weighting, rather
    than presenting it as a standalone analysis

- **Framework: Purchasing Chessboard concept** (conceptually related to
  A.T. Kearney's trademarked Purchasing Chessboard®)
  - What it contributes: a matrix-based approach to mapping category
    sourcing levers across supply/demand-side strategies
  - How this tool differs: Category AI implements its own original 64-cell
    board — no licensed A.T. Kearney dataset is included, and "Purchasing
    Chessboard" as a mark remains Kearney's. A licence would be required
    before wiring in official Kearney data. See
    `docs/THIRD-PARTY-NOTICES.md` for the full attribution note.

## Core framework (your original model)

The tool positions a category using two composite scores:
1. **Business Impact Score** — derived from spend volume, criticality to
   operations, and number of viable alternative categories
2. **Supply Risk Score** — derived from supplier concentration, switching
   cost, and Five-Forces-informed market power signals

These two scores place the category on a quadrant, and the AI layer then
suggests category strategy directions per quadrant (e.g. "Strategic" →
partnership/joint innovation approaches; "Leverage" → competitive
tendering). The purchasing chessboard's 64 cells provide a complementary,
more granular set of sourcing/negotiation lever suggestions once a category
has been quadrant-placed.

## Inputs → Process → Outputs

- **Inputs:** category name, spend data, supplier count, contract terms,
  market conditions
- **Process:** AI-assisted scoring against Business Impact and Supply Risk
  axes, informed by Kraljic and Five Forces logic; optional deeper
  chessboard-based lever selection
- **Outputs:** quadrant placement, suggested strategy direction, chessboard
  lever recommendations, AI-generated narrative explanation

## Why this approach (rationale)

Manual category positioning doesn't scale across a large category
portfolio and is rarely updated once market conditions shift. AI-assisted
scoring allows category managers to re-run positioning quickly as inputs
change, while keeping the underlying strategic logic (Kraljic, Five Forces,
and chessboard-style lever mapping) intact and recognisable to procurement
professionals — rather than replacing established frameworks with an opaque
black-box score.

## Version history

- v1.0–v1.2.0: initial AI-assisted Kraljic-style positioning model,
  Five-Forces-informed supply risk weighting (see `archive/` for these
  version snapshots)
- Current: adds the 64-cell purchasing chessboard tool, AI-assisted lever
  suggestions, and consolidated documentation (`docs/`, `archive/`)
