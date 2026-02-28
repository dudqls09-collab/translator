# Translate Task Template (Copy-paste into Codex)

Translate **all new files** in `/inbox` from English to Korean.

## Mandatory protocol
Follow `AGENTS.md` + `TRANSLATION_POLICY.md` + `glossary/GLOSSARY.md`.

You must execute a 4-pass pipeline for **each** input file:
1) Pass 0: create `out/_meta/<same-filename>.style.json`
2) Pass 1: create `out/_draft/<same-filename>.ko.draft`
3) Pass 2: create final `out/<same-filename>`
4) Pass 3: create `out/_meta/<same-filename>.qa.md` and fix if any hard gate fails (max 2 retries)

## Constraints
- Preserve Markdown structure, links, filenames, inline code, quoted identifiers.
- Do NOT translate code blocks (``` ... ```).
- Keep units, numbers, versions exactly as written.
- HTML: translate text nodes only; do NOT alter tags/attributes/scripts/styles.

## Deliverables
- `out/<same-filename-as-input>`
- `out/_draft/<same-filename>.ko.draft`
- `out/_meta/<same-filename>.style.json`
- `out/_meta/<same-filename>.qa.md`
- Update `STATUS.md` (newest entry at the top)
