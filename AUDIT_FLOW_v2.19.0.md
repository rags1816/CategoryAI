# CATEGORYAI — honest flow audit (v2.19.0)

**Build:** sha256 `ad067baa14a9a51276466ac76b33d5d18a96def72d262c33063270d6fd69a1b5` · portfolio code frozen at v2.12.0 · full 14-suite battery green

## The question asked
Do the portfolio and category tracks work independently AND dependently (category as part of a portfolio) with a logical flow — and has the app become too complex to operate?

## Verdict, honestly
**The logic is sound; the *entry and orientation* were not.** The app had grown three coherent journeys but never told the user which one they were on, gave no visible minimum path through the richest screen (P1), and had one genuinely missing link (a standalone category couldn't *join* a portfolio, only update an existing line). Those are fixed in this build. The remaining density is **capability, not confusion** — a practitioner suite covering two management levels cannot be a five-button app, and hollowing it out would be the wrong fix. Progressive disclosure (collapsed banners, composer, preflight) is the right mechanism and stays.

## The three journeys — audited
**A · Portfolio only (independent).** P1 charter/fact-base/composition → P2 questions/options/matrix/risk → P3 roll-up → board paper. Self-contained; never requires a category build. ✔ Sound.
**B · Category only (independent).** Steps 1–14 → strategy document + business case. Self-contained; never requires a portfolio. ✔ Sound. Dependencies inside the track verified: research→SWOT/PESTLE (wired v2.14), drivers/levers→opportunities→generation prompt→document, kept chess plays→funnel/doc/prompt, preflight before generation.
**C · Category as part of a portfolio.** Three connection points, each explicit and user-confirmed: (1) *entry* — the Step-1 reminder when the name matches a line, with view-existing-strategy; (2) *during* — deep-dive from P3 with sticky banner + sidebar chip + charter inheritance + live sync; (3) *exit* — the Step-14 card: update the matching line (stamped), or **new in this build: add as a new line** when no match exists. Standalone remains a valid end state — connection is always opt-in. ✔ Sound, now complete.

## What was genuinely wrong — and is now fixed
1. **No guided entry.** Fresh sessions landed on category Step 1 with a 20-item nav and no explanation. → 🚦 Start-here banner: three cards (Portfolio / Category / demo tour), one click routes, dismiss persists.
2. **P1 had no visible minimum path** (~14 collapsed banners of equal apparent weight). → "Minimum path" chip strip with live done-ticks: 1 Charter → 2 Composition → 3 Options (P2) → 4 Report (P3), everything else explicitly labelled "deepens the report — optional, any order."
3. **Step-14 button sprawl** — generate and six output buttons in one undifferentiated row. → An "Outputs — one strategy, several formats" divider now separates making the strategy from downloading it.
4. **Nav implied 7Ps precedes the strategy document** (OUTPUT listed it first). → Order swapped; strategy is "14 · Strategy, business case & outputs", 7Ps is "(optional add-on)".
5. **Missing link:** a standalone category with *no* matching line had no route into the portfolio. → "➕ Make this category part of your portfolio?" adds a composition row (spend from internal data where present, Kraljic from the derivation) and stores the strategy as the line's deep-dive — confirmed, stamped, declared.

## Accepted complexity — deliberate, not accidental
- **Two "options" concepts** (P2 strategic options vs Step-14 options & opportunities) are different management levels sharing a word; renaming either would break practitioner vocabulary. The Step-14 panel says "from should-cost, drivers & levers" to disambiguate.
- **Deep-dive vs standalone-then-update** have different semantics (live sync + charter inheritance vs one-shot update, no inheritance) — both banners state this; it's a real choice, not duplication.
- **The nav is long** because the method has 14 steps plus a portfolio track; the grouped, collapsible rail with progress dots is the mitigation, and the start banner now explains which half matters to you.

## Browser checklist for this build
Fresh profile (or clear storage) → see the start banner, take each card once · P1 → watch the chip strip tick as you fill charter/composition · name a category that matches a line → Step-14 shows *update*; name one that doesn't → shows *add as new line*, then check P1 composition and P3 · Step 14 → confirm the Outputs divider reads clearly.
