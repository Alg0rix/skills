---
name: setup-claude
description: Set up Claude Code with Alg0rix's global CLAUDE.md conventions, internal auto-memory, persistent personal memory at ~/.workspace, high-impact testing, Haiku implementation/search/test agents, and Opus reviews. Use when asked to configure Claude like this setup or apply these Claude preferences.
license: MIT
metadata:
  author: Marchel Fahrezi (Alg0rix)
---

# Set up Claude Code

Configure the target user's Claude Code installation using the bundled templates.
This is an opt-in configuration workflow, not instructions to apply the profile
to every task where this skill is discovered. Creating or inspecting the skill
does not authorize changing the current machine's Claude configuration.

The profile comes from `~/.claude/CLAUDE.md`, the Explore and test-runner agents,
and Claude's internal feedback memory. See [source notes](references/sources.md)
for scope and conflicting older memories. Personal memory uses a separate
Markdown/git repository at `~/.workspace`, alongside Claude's internal memory.

## Apply the profile

1. Resolve the target home directory from the setup request; default to the
   current user's home. Inspect existing `~/.claude/CLAUDE.md`, `settings.json`,
   and the two target agent files. Do not read credentials or copy another
   user's settings wholesale.
2. Back up each existing file that will change under a new timestamped directory
   in `~/.claude/backups/`. Preserve original content and permissions. Merge
   the [global instructions](assets/CLAUDE.md) into `~/.claude/CLAUDE.md`, keeping
   unrelated instructions and avoiding duplicate rules on repeated runs. The
   test cadence and Opus review exception must stay explicit. Surface conflicting
   target preferences rather than silently replacing them.
3. Merge the [settings fragment](assets/settings.json) into `settings.json` by
   nested key: preserve unrelated environment variables and settings. This
   selects Haiku for Agent subagents and removes default commit/PR attribution.
   If existing JSON cannot be parsed, stop editing that file and report the
   error. Do not change permissions, hooks, plugins, provider credentials,
   primary model, or security prompts.
4. Install or merge [Explore](assets/agents/Explore.md) and
   [test-runner](assets/agents/test-runner.md) into `~/.claude/agents/`.
   Preserve unrelated agents. Reviews must run inline in an Opus session or
   through an available delegate explicitly pinned to Opus: the global Haiku
   override also affects agents whose own frontmatter requests Opus. If Opus
   is unavailable, report that constraint; do not substitute a cheaper reviewer.
5. Configure internal auto-memory following the section below. Do not copy this
   author's project memory directories into the target installation.
6. Set up personal memory using [the personal-memory setup guide](references/personal-memory-setup.md).
   Install its bundled skill and initialize or reuse the target user's store.
7. Parse the resulting settings JSON, inspect the final diff, and confirm the
   installed files and model routing. Use a fresh Claude session to verify
   agent discovery when Claude is available and invocation is authorized;
   otherwise report runtime discovery as unverified. Tell the user to restart
   Claude or start a new session to load the changes. Report changed paths,
   backup location, conflicts, and anything not verified.

No dependency installation or remote account creation is necessary. Memory
commits and synchronization follow the personal-memory workflow; do not commit
or publish unrelated Claude configuration or project changes.

## Internal auto-memory

Use Claude's own project-scoped auto-memory directory. In a Claude session,
use the memory directory reported by that session or open `/memory` to find
it. Outside Claude, inspect existing `~/.claude/projects/*/memory/MEMORY.md`
and verify which project owns a directory before editing it. Do not guess the
encoded project path, choose an arbitrary project, or treat the home-directory
project's memory as globally loaded. If the project mapping is unavailable,
complete global setup and report memory initialization as pending the first
Claude session in the intended project.

Keep `MEMORY.md` a short index linking topic files. A feedback note should have
`name`, `description`, and `type: feedback` frontmatter, followed by the rule,
why it exists, and how to apply it. Store durable user corrections and reusable
project findings; exclude secrets, raw transcripts, temporary task state, and
unverified assumptions. Update existing notes instead of duplicating them.
Current user instructions take precedence over remembered feedback.

Global preferences belong in the global `CLAUDE.md`; internal memory holds
project context and feedback. The bundled global profile already includes the
reusable feedback from this setup, so do not seed duplicate memory notes just
to make the directory nonempty.

Personal memory holds cross-session preferences and reusable knowledge outside
Claude's project memory. Store each fact once and link to its canonical location
instead of maintaining competing copies in both stores.
