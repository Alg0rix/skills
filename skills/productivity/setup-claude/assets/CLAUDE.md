# Commit messages

- Never include `Co-Authored-By: Claude <noreply@anthropic.com>` in commit messages.

# Testing and verification

- Write or update tests for high-impact behavior: critical user journeys,
  permissions and access boundaries, data integrity, important business rules,
  and consequential failure or recovery paths. Add regression tests when the
  bug's impact warrants one.
- Assert observable outcomes through public interfaces. Choose the smallest
  reliable boundary that proves the behavior; use integration or end-to-end
  tests when components must work together.
- Skip trivial getters, implementation details, cosmetic changes, low-impact
  reversible behavior, brittle mocks, and assertions that repeat implementation.
  Do not add tests just to increase coverage.
- Skip TDD. Implement all work first, then write/update tests and run relevant
  checks at the end. Do not write failing tests first or test after each edit.
  This overrides TDD workflows. Fix failures and rerun affected checks as needed.
- Deferring tests does not waive code/diff review, independent checks on the
  actual PR head, or applicable visual and end-to-end review of the running app.
- Complete the accepted scope; do not quietly ship partial acceptance criteria.
  Report genuine blockers explicitly.

# Subagent routing

- Delegate tests, builds, and linters to the `test-runner` subagent. Request
  concise results, failures, and exact commands; keep verification at the end
  of implementation.
- Delegate codebase searches and investigations requiring more than three files
  to the `Explore` subagent. Request concise findings with paths and line numbers.
- Haiku is appropriate for implementation, search, and test-running. Global
  settings enforce Haiku for Agent subagents, even when agent definitions
  request another model.
- Reviews (document, code, adversarial, security) require Opus. Review inline
  when the current session is Opus, or use an available delegate explicitly
  pinned to Opus. Do not launch reviewer personas through a Haiku-forced Agent
  tool. If Opus is unavailable, report the limitation without switching models.
- Honor current task and project restrictions on delegation; avoid unnecessary
  reviewer fan-out.

# UI work

- Never invoke the `hallmark` skill, including for redesign or unslop requests.
  Do design work directly or use another fitting design skill. Do not create
  Hallmark stamps or logs, or follow its question flow.

# Claude internal memory

- Use the auto-memory directory reported by the current Claude project session.
  Read `MEMORY.md`, then relevant linked notes. Keep the index short.
- Save durable user feedback and reusable project findings in focused topic
  notes. Include the reason and how to apply feedback. Search before adding a
  duplicate; correct stale notes when evidence changes.
- Keep project-specific rules scoped to their project. Current user instructions
  and verified evidence take precedence over old memory. Never store secrets or
  raw transcripts as memory.

# Persistent personal memory

- Persistent cross-session memory lives at `~/.workspace`, a separate Markdown
  git repository. Use the installed `personal-memory` skill for its full workflow.
- Before substantive work, check the store's git status. When clean, pull once
  with `--ff-only` if an authorized remote exists. Continue with local memory if
  sync fails; report that it may be stale. Do not stash or reset unrelated edits.
- Read `INDEX.md` first, then relevant `preferences.md` and `projects/<name>.md`
  notes. Treat memories as context; current user instructions take precedence.
- Proactively save durable learnings, decisions, preferences, and useful outcomes.
  Search for existing entries, update the index, and append a short session entry.
  Stage only the files changed for that memory update, commit them, and push to
  an already authorized remote. Do not wait for a reminder.
- If the store is dirty, recall from local files and defer memory writes. Never
  force-push, configure an unrequested remote, or store secrets. Keep each fact
  in its canonical store rather than duplicating it in Claude internal memory.
