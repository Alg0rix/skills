---
name: cleanup-tests
description: >
  Use when the user asks to clean up, trim, deslop, or delete existing tests;
  when a suite is bloated, flaky, over-mocked, coverage-padded, or coupled to
  implementation. Also /cleanup-tests, "clean up the tests", "too many tests".
  Do not use for writing new tests (use high-impact-testing) or for cleaning
  skills or application code.
license: MIT
metadata:
  author: Marchel Fahrezi (Alg0rix)
---

# Cleanup Tests

Delete tests that cannot catch a real bug. Do not add tests while cleaning.
Do not change product behaviour to make a leftover test pass.

The keep/delete bar is **high-impact-testing**. This skill is the pass over
an existing suite.

## Persistence

ACTIVE when the user asks to clean, trim, or deslop tests, or points at a
bloated/flaky/over-mocked suite. Off only: "stop cleanup-tests".

## Scope

- Named file, folder, or test → that only.
- "the tests" / no name → the tests for the code already under discussion.
  Do not roam the whole repo.

## Ladder

For each test, stop at the first rung that holds — then delete or keep:

1. **Would nobody notice if the code it "protects" broke?** Delete.
2. **Does the type system already guarantee it?** Delete.
3. **Does it mock the thing it claims to verify?** Delete. Do not replace it
   in this pass.
4. **Does it poke internals, private fields, call order, or side channels?**
   Delete. Behaviour is what the interface returns, not how.
5. **Is the same behaviour already covered at a real seam (route, CLI, DB)?**
   Delete the extra unit test.
6. **Was it written to move a coverage number?** Delete.
7. **Keep** only if it would have caught a real bug: auth/authz, money or
   date math, migrations, a seam that broke in prod, or the user named it.

Mark a keep that looks skippable with `// high-impact-testing: <why>`.

## Rules

- Deletion first. No new tests, no new framework, no filling coverage gaps.
- Do not rewrite a test into a different test. If it is the wrong shape,
  delete it. A replacement belongs to high-impact-testing, and only if the
  user asked.
- Do not edit product code in this pass unless a deleted test was the only
  thing forcing extra complexity — then shrink the product, don't add tests.
- After deletes, run the remaining tests in scope. If something fails that
  you did not intend to touch, stop and say so.
- 80:20. The long tail of "just in case" tests goes.

## Output

Deletes first. Then at most three lines:

`[test] → removed: [X], because [Y]. kept: [Z].`

No essay defending every omitted unit test.
