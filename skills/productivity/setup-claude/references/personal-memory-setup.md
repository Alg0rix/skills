# Set up personal memory

Configure the target user's own memory store. Do not copy the author's private
preferences, project notes, git history, or remote URL.

## Install the workflow

Copy the bundled [personal-memory skill](../assets/personal-memory/SKILL.md) to
`~/.claude/skills/personal-memory/SKILL.md`, creating the directory if needed.
If already installed, inspect it first; keep an equivalent or newer workflow.
Back up before merging or replacing a different version. The bundled copy is
from this repository's `skills/productivity/personal-memory/SKILL.md`; refresh
it from that source when maintaining this setup skill.

Merge the personal-memory section of the global `CLAUDE.md` template with any
existing equivalent instructions. Avoid duplicate sections on repeated setup.

## Create or reuse the store

Use `~/.workspace` unless the user specified another location. Substitute that
location consistently in the installed instructions if changed.

- If it already exists, verify `git -C <store> rev-parse --show-toplevel` resolves
  to the store itself, not a parent repository. Inspect `git status --porcelain`,
  `README.md`, and `INDEX.md`. Preserve notes and follow the installed skill's
  clean/dirty and sync rules. Do not reinitialize an existing repo.
- If a supplied memory remote should be cloned, clone only into a missing or
  empty destination. Use the supplied URL, never the author's remote. Do not
  invent credentials or create an account/repository.
- Otherwise, initialize a local-only git repository in a missing or empty store.
  A nonempty directory that is not itself a memory git repo is a conflict:
  leave it intact and report it rather than initializing over existing data.

For a new local store, create `learnings/`, `decisions/`, `projects/`, and
`sessions/`. Add these initial files:

- `INDEX.md`: a `# Memory Index` heading and tables for Preferences, Learnings,
  Decisions, Projects, and Sessions. Give each file one row with its date,
  relative link, tags where useful, and concise summary. Initially link only
  `preferences.md`; add rows as actual notes are written.
- `preferences.md`: a heading and space for the target user's confirmed durable
  preferences. Do not populate it with the author's private notes or infer
  additional preferences from the act of installing this profile.
- `README.md`: describe the folders and INDEX-first recall, clean-tree
  `pull --ff-only` for an authorized remote, focused notes with source/date
  metadata, linked index updates, session entries, scoped staging/commits,
  authorized push, and dirty-store deferral. Point to the installed
  `~/.claude/skills/personal-memory/SKILL.md` for the full protocol.

Commit only the new bootstrap files using a plain commit message such as
`memory: initialize store`. If git identity is missing, leave files intact and
report the pending commit; do not invent identity. A local-only setup needs no
remote. If the user supplied a remote for this store, configure it as requested
and push on the first successful commit. Otherwise keep it local. For an
existing remote, follow the installed skill's synchronization and write rules.

## Verify

Confirm the store is its own git root, `INDEX.md` links resolve, and the installed
skill and global instructions name the same store. Report whether memory is
local-only or synced, and any pending commits or pushes. Do not manufacture a
sample personal fact just to test persistence. Setup is complete when the
workflow and store are available; runtime recall in a new Claude session remains
unverified until actually exercised.
