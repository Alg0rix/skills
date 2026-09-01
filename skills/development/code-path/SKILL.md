---
name: code-path
description: >
  Use when the user asks how a code path works, what calls a symbol, where a
  request/job/event/handler goes, or whether production and tests wire the
  same way. Also "how does X work?", "what calls X?", "where does X go?",
  execution flow, request path, callers, callees, upstream, downstream,
  call graph. Skip trivial facts, port or version questions, simple
  definitions, text edits, and rename-only changes.
license: MIT
metadata:
  author: Marchel Fahrezi (Alg0rix)
---

# Code Path

Answer flow questions from files you opened. A node without `path:line` is a
guess. Graph the behaviour path — the request, job, or event as a caller
hits it — not every private helper.

## Persistence

ACTIVE for any "how does this work / what calls this / where does this go"
question. Off only: "stop code-path".

## Ladder

Stop at the first rung that holds:

1. **One-line fact?** A name, a port, a definition → answer in one line. No graph.
2. **Can you name the real entry from source?** Route, `main`, job, listener, CLI. If not, find it before drawing.
3. **Walk the behaviour path.** Open each callee. Skip getters, wrappers, and internals that do not change control or data flow.
4. **Do tests wire it differently in source?** Show `Tests`. Otherwise omit `Tests`. Never copy Production and relabel it.

## Rules

- No inferred nodes. Names, comments, and "this is the usual pattern" are not evidence.
- Prefer language-server go-to-def/refs, `rg`, `ast-grep`, the type checker, and the tests that actually construct the subject. Do not invent callers from a filename.
- Actual symbols from source: functions, methods, services, jobs, queues, stores.
- `[condition]` on the edge. `{queue_or_store}` as a leaf. `[new]` for planned nodes — no fake line numbers.
- One graph, asked scope only.
- Graph behaviour, not implementation: if a refactor could rename a private helper without changing what the caller observes, it does not belong on the graph.
- Production and tests are different layers only when the source proves they differ.

## Output

Lead with the graph. Then `src:` for every unique node. Then at most a few
lines for retries, errors, fallbacks, and gotchas the graph cannot show.
Plain indented `→` tree. No Mermaid, no boxes.

```
graph: Authentication request path

Production:
POST /login
  → views.login
    → auth.authenticate
      → users.find_by_email
      → tokens.issue
        → {sessions.save}

src:
  POST /login → src/urls.py:18
  views.login → src/views.py:42
  auth.authenticate → src/auth.py:27
  users.find_by_email → src/users.py:63
  tokens.issue → src/tokens.py:19
  sessions.save → src/sessions.py:31
```

Show `Tests:` only when verified test wiring differs. Same shape, real test
names, real `path:line`.

## Red flags

- "I think it goes through..."
- Mermaid
- Line numbers you did not read
- A Tests graph that is Production with "Test" prefixed
- Every method on a class listed

If any of these happened: delete the graph. Open the files. Draw again.
