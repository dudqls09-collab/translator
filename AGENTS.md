# Translation Agent Repo (Docs-only)

## Purpose
This repository defines a translation workflow for producing publication-quality Korean translations from English inputs.

- Input directory: `inbox/`
- Output directory: `out/`
- This repo is **docs-only**. Do not add application code. Enforce quality via workflow docs + templates.

## Source of truth (priority order)
1) `TRANSLATION_POLICY.md`
2) `glossary/GLOSSARY.md`
3) `prompts/*` (execution protocol)

## Mandatory execution protocol (4-pass, artifact-driven)
For **each** input file in `inbox/`, you must run the following passes and write artifacts:

### Pass 0 — Style Sheet (planning, saved)
- Write: `out/_meta/<same-filename>.style.json`
- This file is the binding contract for tone/register/POV and allowed style shifts.

### Pass 1 — Draft translation (meaning-first)
- Write: `out/_draft/<same-filename>.ko.draft`
- Focus on semantic fidelity. Allow awkward phrasing temporarily.

### Pass 2 — Rewrite (publishable Korean)
- Write final: `out/<same-filename>`
- Rewrite for natural Korean readability and rhetorical equivalence.
- Must follow the style sheet contract and HTML constraints.

### Pass 3 — QA Gate (hard gate + fix loop)
- Write: `out/_meta/<same-filename>.qa.md`
- If any hard gate fails: redo Pass 2 and re-run Pass 3 (max 2 iterations).
- Only after all hard gates pass, update `STATUS.md`.

## Non-negotiables
- Never invent facts.
- Preserve numbers, units, dates, versions, code blocks, identifiers.
- HTML: translate visible text only. Preserve structure, tags, attributes, scripts, styles.
- If context is missing, add minimal `[역주: ...]` only when essential.
