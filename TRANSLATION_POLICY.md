# Translation Policy

## Default direction
- Source: English
- Target: Korean

## Priority (strict)
1) Natural Korean readability and flow (highest)
2) Technical meaning fidelity (preserve intent, not literal form)
3) Terminology consistency (use glossary first)

### Interpretation rule
- Translate for how a professional Korean translator would naturally write, not how a machine would map words one-to-one.
- You may restructure sentence order, split/merge sentences, and localize expressions when needed for fluency.
- Preserve the source intent, constraints, and key facts, but avoid awkward literal phrasing.

## Target reader / tone
- Reader: non-expert who still wants precise technical meaning
- Korean honorifics (존댓말)
- Professional, publication-quality Korean (자연스럽고 매끄러운 문장)
- Prefer clear, idiomatic Korean over literal translation style
- Avoid mechanical translation artifacts (직역투, 어색한 연결어, 반복적 문장 패턴)

## Formatting / structure
- Preserve Markdown structure, headings, lists, tables
- Preserve links, filenames, inline code, and any quoted identifiers
- Do not translate code blocks (``` ... ```)
- Keep units, numbers, versions exactly as written

## Notes / translator’s notes
- If context is missing, add minimal note in-line:
  - [역주: ...]
- Never add new facts.
- Do not drop essential constraints or facts, but non-essential wording may be adapted for natural Korean.
