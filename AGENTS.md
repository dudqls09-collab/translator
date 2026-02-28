# Codex Project Guidance (Translation Repo)

## What this repo is
This repo is a translation workspace. Inputs go to /inbox. Outputs must be written to /out.

## Default translation behavior
- Default direction: EN -> KO.
- Highest priority: natural, fluent Korean based on source intent (avoid literal translation tone).
- Tone: polite, professional Korean; natural flow over rigid sentence mirroring.

## Formatting rules
- Preserve Markdown structure (headings, lists, tables).
- Preserve links and inline code exactly.
- Do NOT translate code blocks (``` ... ```).
- Keep product names, API names, CLI commands as-is unless a standard Korean term exists.

## Output contract (must follow every task)
When translating:
1) Read TRANSLATION_POLICY.md and glossary/GLOSSARY.md first.
2) Translate each input file from /inbox to a matching output file in /out.
3) Append a log entry to STATUS.md with:
   - date
   - source filename(s)
   - target language
   - any [역주] notes count
4) Never invent facts. Keep core intent and constraints, but adapt wording/sentence structure for natural Korean. If context is missing, add only minimal [역주: ...].

## Suggested commands (optional)
No build/test required. This is a docs-only repo.
