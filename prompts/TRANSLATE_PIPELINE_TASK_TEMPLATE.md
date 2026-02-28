# Translate Pipeline Task Template (Strict, file-list driven)

## Goal
Translate the following files from `/inbox` to `/out` with the mandatory 4-pass pipeline.

## Files
- inbox/<FILL_ME>

## Execution steps (must not skip)
For each file:

### Pass 0 — Style Sheet
Write `out/_meta/<same-filename>.style.json` with:
- genre
- stance (monologue / addressing reader / neutral report)
- default_register (한다체 / 합니다체 / 해요체)
- pov_base (나는/저는/우리는)
- reader_address (none / 여러분 / 당신 / 독자)
- permitted_shifts (quote-only / emphasis blocks / reader-address blocks)
- html_mode (true/false)
- forbidden (list): “noun-only sentences”, “random register mixing”, “tag/attr changes (HTML)”
- notes (short): intended tone + any tricky sections

### Pass 1 — Draft (meaning-first)
Write `out/_draft/<same-filename>.ko.draft`.
- Keep meaning and constraints intact.
- Allow awkwardness temporarily.
- No random style drift.

### Pass 2 — Rewrite (publishable Korean)
Write final `out/<same-filename>`.
- Make it read like original Korean writing.
- Apply rhetorical equivalence (avoid literal metaphors when awkward).
- Keep the selected style sheet consistent; allow shifts only within permitted ranges.

### Pass 3 — QA Gate + Fix Loop
Write `out/_meta/<same-filename>.qa.md` containing:
- Hard gate checks (pass/fail) and evidence snippets
- Soft score (0–100) using rubric in TRANSLATION_POLICY.md
- If any hard gate fails: redo Pass 2 and re-run Pass 3 (max 2 loops)

Finally update `STATUS.md` (newest entry at top) with:
- date, direction, inputs/outputs
- style sheet summary (register/pov/reader)
- QA: hard gates pass?, soft score
- [역주] count
