# Changelog

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
