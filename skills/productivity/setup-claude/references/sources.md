# Profile sources

Derived on 2026-11-06 from the author's Claude installation. The templates are
portable; these original paths are provenance, not runtime dependencies.

- `~/.claude/CLAUDE.md`: no Claude commit trailer; high-impact tests through
  public interfaces; implement before testing; retain review; delegate
  verification to test-runner and investigations beyond three files to Explore.
- `~/.claude/agents/{Explore,test-runner}.md`: bundled agent definitions.
- `~/.claude/settings.json`: confirmed
  `env.CLAUDE_CODE_SUBAGENT_MODEL=haiku`. The empty attribution settings are a
  setup mechanism for suppressing attribution, not a copy of existing settings.
- `~/.claude/projects/-home-dev-serv/memory/never-use-hallmark.md`: never invoke
  Hallmark for UI/redesign/unslop work (2026-10-28).
- `~/.claude/projects/-home-dev-serv-Project-py-proj-semesta-one/memory/reviewers-on-opus.md`:
  Haiku implementation/search/test runs are allowed, reviews require Opus
  (2026-11-05). This refines the older blanket Haiku routing in global instructions.
- The same project's `never-cut-scope.md`: complete all accepted criteria and
  independently verify work; do not present partial implementation as finished.

Older ai-platform memories prohibit subagent fan-out and request inline,
sequential reviews. Tomo and Semesta memories contain historical task-specific
provider and model assignments. Do not promote those assignments into a global
default. Honor any restrictions still applicable to the target project.

The original global file also points to a separate `~/.workspace` memory repo.
The user subsequently requested personal-memory setup as well. The bundled
workflow comes from this repository's `skills/productivity/personal-memory/SKILL.md`.
It uses clean-tree fast-forward sync and scoped commits rather than the older
global instruction's rebase/autostash and broad staging procedures.

No credentials, permission bypasses, hooks, plugin catalog, deployment endpoints,
project history, personal notes, or author-specific memory remote are bundled.
