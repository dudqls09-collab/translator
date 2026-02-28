# Translate Task Template (Strict)

Translate **all new files** in `inbox/` from English to Korean.

## Mandatory protocol (must not skip)
Follow `AGENTS.md` + `TRANSLATION_POLICY.md` + `glossary/GLOSSARY.md`.

For **each** input file, you must execute the 4-pass pipeline and write artifacts:
1) Pass 0: `out/_meta/<same-filename>.style.json`
2) Pass 1: `out/_draft/<same-filename>.ko.draft`
3) Pass 2: `out/<same-filename>` (final)
4) Pass 3: `out/_meta/<same-filename>.qa.md`
- If any hard gate fails: redo Pass 2 and re-run Pass 3 (max 2 retries).
- Only after PASS, update `STATUS.md` (newest entry at top).

## HTML constraints (hard)
- Translate visible text in `article` only (p/h1/h2/h3/li/blockquote).
- Do NOT translate or change: head/title/meta/script/style/pre/code, tags/attrs/classes/data-*, URLs, `.sf-hidden`, nav/footer/form.

## Deliverables
- `out/<same-filename>`
- `out/_draft/<same-filename>.ko.draft`
- `out/_meta/<same-filename>.style.json`
- `out/_meta/<same-filename>.qa.md`
- `STATUS.md` updated (newest entry at the top)
