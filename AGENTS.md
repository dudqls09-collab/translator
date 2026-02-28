# Codex Project Guidance (Translation Repo)

## What this repo is
This is a translation workspace.
- Inputs: `/inbox`
- Outputs: `/out`
- This repo is **docs-only**. No build/test is required.

## Source of truth
Always follow, in this order:
1) `TRANSLATION_POLICY.md`
2) `glossary/GLOSSARY.md`
3) `prompts/*` templates (task execution protocol)

## Translation execution protocol (mandatory)
Every translation job must run as a **4-pass pipeline** and produce artifacts.

### Pass 0 — Style Sheet (internal planning, saved as file)
- Create a style sheet for each input file.
- Save to: `out/_meta/<same-filename>.style.json`

### Pass 1 — Draft translation (meaning-first)
- Produce a faithful draft translation.
- Save to: `out/_draft/<same-filename>.ko.draft`

### Pass 2 — Rewrite (publishable Korean)
- Rewrite the draft into natural, publication-quality Korean.
- Save final to: `out/<same-filename>`

### Pass 3 — QA Gate (hard gate + fixes)
- Run QA checks described in `TRANSLATION_POLICY.md`.
- Save QA log to: `out/_meta/<same-filename>.qa.md`
- If any hard gate fails: revise (redo Pass 2) and re-run QA (up to 2 iterations).

## Output contract (must follow every task)
For each translated file:
- `out/<same-filename>` (final)
- `out/_draft/<same-filename>.ko.draft` (draft)
- `out/_meta/<same-filename>.style.json` (style sheet)
- `out/_meta/<same-filename>.qa.md` (QA log)
- Update `STATUS.md` (newest entry at the top)

## Non-negotiables
- Never invent facts.
- Preserve: numbers, units, dates, versions, code blocks, identifiers.
- For HTML: preserve tags/attributes/scripts/styles. Translate text nodes only.
- If context is missing, add minimal `[역주: ...]` only when essential.
