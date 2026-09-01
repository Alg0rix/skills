---
name: cleanup-skills
description: >
  Use when the user asks to clean up, trim, deslop, tighten, or fix existing
  agent skills; when SKILL.md files have duplicated rules, no-op guardrails,
  stale paths, leftover category names, README/plugin drift, or unused
  supporting files. Also /cleanup-skills. Do not use for writing a brand-new
  skill from scratch, or for cleaning application code.
license: MIT
metadata:
  author: Marchel Fahrezi (Alg0rix)
---

# Cleanup Skills

Delete until each remaining sentence changes what an agent does. Do not
rewrite a skill into a different skill. Do not add categories, examples, or
sections "for completeness."

## Persistence

ACTIVE when the user asks to clean, trim, deslop, or tighten skills, or
points at skill sprawl. Off only: "stop cleanup-skills".

## Scope

- Named skill → that folder only.
- "these skills" / no name → every `SKILL.md` under `skills/` except `drafts/`
  and `deprecated/`.
- Application code, tests, and unrelated docs are out of scope.

## Ladder

Stop at the first rung that holds:

1. **Dead?** Unused, superseded, or the user said remove it → `deprecated/` or
   delete if they said delete. Do not keep a stub.
2. **Catalog lie?** Folder name, `name:` frontmatter, README link, and
   `.claude-plugin/plugin.json` path must match. Fix the catalog to match
   disk, not the other way around.
3. **Duplicate fact?** Same rule in two places → keep one home, delete the
   rest. Description must not summarize the workflow; it only says when to
   use the skill.
4. **No-op?** Sentence that does not change behaviour, or "don't X" after
   "do Y" already landed → delete it.
5. **Orphan file?** Script, reference, or example nothing points at → delete
   it.
6. **Still too long?** Cut until a later agent can follow it without the
   cut sentence. Prefer fewer bullets over a new heading.

## Rules

- Deletion first. No new skills, no new folders, no new examples while
  cleaning.
- Do not change purpose, triggers, or output contract unless they are wrong
  or duplicated.
- `name:` is kebab-case and equals the folder name.
- One pass per skill. Do not "improve" voice, add rationalization tables, or
  port in another skill's structure.
- After edits, grep the repo for the old name, old path, and broken
  relative links.

## Output

Edits first. Then at most three lines:

`[skill] → removed: [X]. kept: [Y].`

No tour of skills you did not touch.
