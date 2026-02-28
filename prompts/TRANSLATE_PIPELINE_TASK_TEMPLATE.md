# Translate Pipeline Task Template (File-list driven, strict)

## Files (fill these)
- inbox/<FILL_ME>

For each file, do:

### Pass 0 — Style Sheet
Write `out/_meta/<same-filename>.style.json` following the required fields in `TRANSLATION_POLICY.md`.

### Pass 1 — Draft
Write `out/_draft/<same-filename>.ko.draft` (meaning-first).

### Pass 2 — Rewrite
Write final `out/<same-filename>` (publishable Korean).
- Must comply with the style sheet and HTML constraints.

### Pass 3 — QA Gate + Fix Loop
Write `out/_meta/<same-filename>.qa.md` including:
- Hard gate PASS/FAIL + evidence snippets
- Soft score (0–100) by rubric
- Top 3 fixes
If any hard gate FAIL: redo Pass 2, then redo Pass 3 (max 2 loops).

Finally update `STATUS.md` (newest entry at top) with:
- date, direction, input/output paths
- style summary
- QA summary (hard gates + soft score)
- [역주] count
