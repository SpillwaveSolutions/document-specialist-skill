# Voice and style

TOKEN_BUDGET: 280
TIER: 1
LOAD_TRIGGER: Every document this skill writes
DEPENDENCIES: SKILL.md

## One pack only

| Pack | Default | Use when |
|------|---------|----------|
| STE100 | Yes | All docs unless the user names Google style |
| google-docs-style | No | User says Google style / Google developer docs |

Do not mix packs in one document.

## Hard bans (both packs)

1. No em dash (`\u2014`). No `--` used as an em dash. Use a period or a comma.
2. No sentence that starts with So, That, Thus, or Hence.
3. Rewrite "So the service retries" to "The service retries".
4. Rewrite "That means the lock is held" to "The lock is held".

## STE100 defaults

- Procedure sentence: 20 words or fewer.
- Description sentence: 25 words or fewer.
- One instruction per numbered step.
- Active voice. Imperative in procedures.
- No contractions. Write "do not", not "don't".
- No Latin short forms (`e.g.`, `i.e.`, `etc.`).
- No should / could / might / may in steps.
- One meaning, one word.

Invoke the `ste100` skill loop on the finished draft. Stay local. Do not call a network STE checker.

## Google style (opt-in)

- Address the reader as you.
- Present tense. Active voice. Serial comma.
- One H1. Sentence-case headings.
- Bold UI labels. Code font for commands and paths.
- Run the google-docs-style formatter when that skill is installed.

## Diagrams stay outside the voice pack

Voice rules apply to prose, headings, list items, and captions. They do not rewrite fenced `mermaid` or `puml` code.
