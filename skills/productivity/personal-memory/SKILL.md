---
name: personal-memory
description: Persistent cross-agent memory at ~/.workspace (Markdown + git). Use when asked to remember or recall something, when starting work that may have prior context, or when a run produces a learning, decision, or preference worth keeping.
---

# Memory

Store: `~/.workspace` — a git repo of Markdown only, synced to `origin` (github.com:Alg0rix/memory). Full protocol: `~/.workspace/README.md`.

## Sync

Keep the store current so memory written by other agents and machines is visible:

- **Before reading**: `git -C ~/.workspace pull -q --rebase --autostash` — picks up memory written elsewhere.
- **After writing**: commit + push (below).
- Once per run is enough — don't pull on every read.
- Pull failures (offline, diverged history) must not block work — continue with local state and note it.

## Recall

- Scan `~/.workspace/INDEX.md` first — it indexes every memory file by date, tags, and summary.
- Search: `grep -ril "keyword" ~/.workspace --include="*.md"`, or `ls -t ~/.workspace/learnings/ | head` for recent.
- For project work, also check `~/.workspace/projects/<name>.md` and `~/.workspace/preferences.md`.
- Read only the files the index points to; don't bulk-read the store.

## Remember

When the user says "remember this", or a run produces a durable learning, decision, or preference:

1. Pull first if you haven't this run — avoids clobbering concurrent writes.
2. Write the file per README conventions:
   - `learnings/YYYY-MM-DD-slug.md` — insights, gotchas, how things work
   - `decisions/YYYY-MM-DD-slug.md` — decisions + rationale
   - `projects/<name>.md` — running project context (update in place)
   - `preferences.md` — standing user preferences (edit in place)
   - `sessions/YYYY-MM-DD.md` — append one line on what was done
3. Add or update the matching row in `~/.workspace/INDEX.md` — it is the entry point, never skip it.
4. Commit and push: `cd ~/.workspace && git add -A && git commit -m "memory: <summary>" && git push`.

## Rules

- One idea per file; date-prefixed kebab-case names; YAML frontmatter with `date`, `tags`, `project`.
- Never write secrets, tokens, passwords, or credentials.
- Correct stale memory by adding a new dated note that links the old file — don't rewrite history.
- Batch related writes into one commit; don't commit when nothing changed.
