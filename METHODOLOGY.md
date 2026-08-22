# Development Methodology

The workflow this repo's development has followed, and why — for
anyone continuing this work, human or AI.

## The core cycle

**Patch → verify structurally → live-test → freeze → checksum → changelog**

No step gets skipped, and no step happens out of order. A patch that
hasn't been live-tested is not "done" — it's a candidate.

## 1. Patch

One scoped change at a time where reasonably possible. When a fix
touches multiple files/functions for a single coherent reason (e.g.
the same field-naming bug appearing in two separate components), fix
all instances together rather than partially.

## 2. Verify structurally

Before any version bump, confirm the edited function's braces and
parentheses are genuinely balanced. **The naive method — counting `{`
and `}` across a whole file — produces false positives**, because
string literals (JSON schema examples inside AI prompts, emoji-adjacent
text) contain unmatched brace/paren characters as plain text, not code
structure.

The reliable method: walk brace depth starting from the actual function
body's opening `{` — found by locating the `{` immediately after the
parameter list's closing `)`, not just the first `{` in the source
(which is often the destructured-parameters brace, giving a trivially
small and meaningless span) — through to where depth returns to zero.

```python
start = content.index('function NAME(')
paren_close = content.index(')', start)
body_start = content.index('{', paren_close)
depth = 0
j = body_start
while j < len(content):
    if content[j] == '{': depth += 1
    elif content[j] == '}':
        depth -= 1
        if depth == 0: break
    j += 1
# content[start:j+1] is the real function; check brace/paren counts there
```

**When a discrepancy shows up, check it against the pre-edit baseline
before assuming it's new.** More than once this session, a "failing"
check turned out to be an artifact already present in the last known-
good, already-shipped file — proving the edit didn't introduce it. Only
trust a discrepancy as real once you've confirmed the baseline was
clean on that exact same check.

## 3. Live-test — with evidence, not impressions

A fix is not confirmed by "it looks right" or "the button responded."
The standard used throughout this repo's history:

- **Quote exact values observed** — an exact total, an exact score, an
  exact error message — not a paraphrase
- **For visual/rendering claims, extract and inspect the actual asset**
  (pull the embedded chart image out of the .docx and look at it) —
  don't infer correctness from "a chart appeared"
- **For UI state claims, use the DOM/accessibility tree directly**
  (`document.elementFromPoint`, computed styles, `getBoundingClientRect`)
  rather than a visual screenshot alone — several real bugs in this
  history (state logic masquerading as a "mobile touch" issue) would
  have been misdiagnosed by relying on appearance alone
- **Re-test the specific thing that failed**, not just "does the app
  still load," after every fix. Several fixes in this history needed a
  second round because the first attempt addressed a symptom convincingly
  without addressing the actual mechanism — confirmed only by testing
  the exact original failure case again, not a broader smoke test

## 4. Don't declare done on a single pass

A pattern worth naming explicitly, because it recurred: fixing one bug
sometimes reveals a second, previously-masked one in the same area
(e.g. fixing a crash on a screen surfaces a completely unrelated,
pre-existing broken button that testing happened to exercise while
verifying the fix). Finding something unrelated to what you were
checking is a reason to fix it, not a distraction from the actual task.

## 5. Freeze

A "freeze" is a specific, checkable claim: *this exact file, identified
by its hash, is what's live.* Not "I think this is what's deployed" —
a SHA-256 comparison between the file about to be recorded and the
actual file fetched from the live URL.

```cmd
certutil -hashfile index.html SHA256
```

If the hash doesn't match, the freeze record is wrong and needs
correcting before trusting it — this caught at least one real upload
mismatch in this repo's history (an intermediate build got uploaded
instead of the intended one).

## 6. Changelog

Every freeze gets a changelog entry recording: what changed, why (the
actual bug/gap, not just the fix), and the verified checksum. Entries
distinguish real fixes from confirmed-non-bugs (a report that turned
out to be correct existing behavior, once investigated) — both are
valuable to record; conflating them isn't.

## Why this much process for a single HTML file

Because "it's just one file" is exactly the condition under which
sloppy verification is most tempting and most costly — there's no
compiler, no type system, no test suite to catch a syntax slip before
it reaches production. The structural-balance check and the live-
evidence standard exist specifically to substitute for the safety net
a build step would normally provide.
