---
name: avoid-overengineering
description: Use for every implementation, debugging, refactoring, review, configuration, or repository task; especially when scope, design, testing, or process could expand beyond what the accepted requirement justifies.
metadata:
  author: Marchel Fahrezi (Alg0rix)
---

# Avoid Overengineering

## Purpose

Complete the current task with the minimal sufficient solution.
Prohibit over-engineering.
Planning can be aggressive, but execution must be lightweight.
Designs that cannot prove necessity are not done by default.
Tests that cannot prove necessity are not added by default.

## Workflow

1. Understand the requirements first, then take action. Do not modify code first and guess the intent afterward.
2. Use stronger reasoning during planning. During execution, default to medium-low reasoning or a lighter model when available.
3. Do not keep the highest reasoning mode on throughout.
4. Do not default to spinning up multiple agents in parallel. Complete one task in a single thread first, then decide whether to split it.
5. Enable only the skills necessary to complete the task. Do not install heavy-process skills.
6. Produce a minimal plan first. The plan must clearly state:
   - Goals
   - Non-goals
   - Acceptance criteria
   - Scope not to be changed

## Failure Modes

1. Failing to truly understand the intent and only fixing surface issues.
2. When a clean root-cause fix could have been done once, instead piling on historical patches, compatibility layers, dual tracks, duplicates, and branches to bloat the code.
3. Over-designing for rare cases, increasing daily maintenance costs.
4. Using the wrong judgment basis: even if reasoning is complete, the conclusion is wrong.
5. Instead of directly reading the code to locate the issue, substituting search or guesswork.
6. Using “add tests” as an excuse to keep adding abstraction, expanding scope, and making things seem complete.

## Action Boundaries

Before taking action, restate:

- What the user truly wants
- The scope of this time
- Things explicitly not to do
- What counts as completion

For any irreversible operation, wait for a user reply with the confirmation codeword before executing. The user must specify the confirmation codeword. Without the codeword, with the wrong codeword, or with any other reply, refuse execution outright.

The following operations are not considered irreversible by default and can be executed:

- Git rollback, revert, or branch switch
- Moving files to the backup directory of the current repository
- Running tests, viewing diffs, generating plans, or read-only analysis

If the target or scope of a destructive operation is unclear, stop and ask the user.

## Testing

Tests only serve to verify the current changes.
Tests are not responsible for filling historical coverage gaps or designing future test systems.

1. Prioritize running existing tests related to this change.
2. If existing tests can prove the change is correct, do not add new tests.
3. Add new tests only when:
   - The change modified behavior, but existing tests do not cover it
   - The user explicitly requires adding tests
4. New tests cover at most one main path of the actual change this time and, if necessary, one key failure path.
5. Do not expand test scope for completeness.
6. Do not use the opportunity to fill tests for unrelated modules.
7. Do not introduce new test frameworks, tools, or infrastructure.
8. Do not write large snapshots, parameterized matrices, or end-to-end suites.
9. Do not write tests for boundaries not required by the current needs.
10. Do not modify tests first and then force product behavior to become more complex.
11. Do not use green tests as a reason to continue adding abstraction.

Before adding any test, answer:

- Which accepted requirement is this test verifying?
- If removed, can existing tests no longer detect this regression?
- Is it more complex than the implementation itself?

If test code is longer or more convoluted than the implementation code, default to considering it over-engineering; delete the test or shrink the implementation.

## Model Division of Labor

- Requirement clarification and solution review: use stronger models.
- Writing code, modifying code, and running tests: use medium-low-spec models or lighter execution models.
- When the execution model starts stacking architecture, adding compatibility, expanding scope, or adding large test suites: stop immediately and rewrite the minimal plan.

## Pre-Completion Checklist

- Intent and acceptance criteria have been restated.
- The solution is minimal, not maximal.
- Non-goals have been marked.
- Relevant code was read directly before forming conclusions.
- Only the minimal set of files needed to complete the task was modified.
- Related existing tests were run.
- No tests were added for unrequired scenarios.
- If tests were added, they only lock the current behavior and are very small.
- Tests did not introduce new dependencies or directory structures.
- The diff is small, with no extra files or leftover debug code.
- No extra construction was done to make the result look complete.

## General Principles

Confirm intent first, then complete acceptance with minimal changes.
Designs that cannot prove necessity are not done by default.
Tests that cannot prove necessity are not added by default.
