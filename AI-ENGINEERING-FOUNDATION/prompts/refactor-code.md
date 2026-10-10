# Prompt: Refactor Code

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 06 (behavior-preserving changes) → 07 (before/after verification) → 08 (review for regressions).

## 1. Purpose

Improve the structure of specific code for a stated reason while preserving its behavior, in small verified steps.

## 2. When to Use

Use when code works but is hard to change, test, or understand, and there is a concrete improvement in mind.

Use something else when:

- Behavior must change → `implement-feature.md` or `investigate-bug.md`.
- The real problem is speed → `performance-review.md`.
- You want an assessment of what needs improving, not a change → `code-review.md` on the area.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Target | Files, module, or area | Keep it bounded. |
| Problem | What is wrong with the current structure | e.g. "pricing rules duplicated in three handlers". |
| Intended improvement | The outcome you want | e.g. "one tested pricing module". |
| Behavior changes allowed | Normally "none" | Any intended change must be explicit. |
| Constraints | Public interfaces or formats that must not change | Optional. |

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/refactor-code.md
(sections 5–8) and principles/code-quality.md ("Refactoring discipline",
"Duplication").

Target: [FILES / MODULE / AREA]
Problem: [CURRENT PROBLEM]
Intended improvement: [GOAL]
Behavior changes allowed: [NONE, OR EXPLICIT LIST]
Constraints: [INTERFACES THAT MUST NOT CHANGE, OR "NONE"]

Rules:
- Understand current behavior before changing anything, and pin it with
  tests if coverage is insufficient.
- Preserve behavior, public interfaces, and data formats unless listed above.
- This is a refactor, not a rewrite. Stay inside the target; make small
  steps; stop when the stated improvement is reached. If the change grows
  beyond the target, stop and ask.
- Do not introduce abstractions without a stated benefit. Prefer removing
  complexity to adding it.
- Review the result for regressions separately from making it (Workflow 08).
- Report exact commands and actual test results before and after; do not
  claim behavior is preserved without that evidence.
```

## 5. Execution Sequence

1. **Inspect** the target, its callers, and its tests.
2. **Understand current behavior**, including edge cases and error behavior.
3. **Identify the actual problem** and confirm it matches the stated one; restate the goal as a checkable outcome.
4. **Evaluate alternatives**: at least two approaches, including the smallest; choose by churn, risk, and benefit.
5. **Assess regression risk**: consumers and current test coverage.
6. **Pin behavior**: add characterization tests where coverage is weak; run them and confirm they pass on the current code.
7. **Refactor in small steps**, running tests after each.
8. **Verify**: same tests pass before and after; run all relevant checks.
9. **Review for regressions** (Workflow 08).
10. **Report.**

## 6. Expected Output

- Problem and goal as a checkable outcome.
- Alternatives considered and the reason for the chosen approach.
- Characterization tests added.
- Before/after summary of structure.
- Changed files.
- Test results before and after the refactor (same tests), with commands.
- Any test changes, each justified (tests should change only if they were coupled to internals).
- Review result.

## 7. Completion Criteria

- The stated improvement is achieved and checkable.
- The same behavior tests pass before and after.
- Public interfaces and formats are unchanged (unless explicitly allowed).
- The diff stays inside the target area, with no unrelated churn.
- Independent review found no regressions, or found ones that were fixed and reverified.

## 8. Stop / Escalation Conditions

Stop and ask when:

- The refactor would require changing behavior, public interfaces, or data formats.
- The change grows beyond the target or toward a rewrite.
- Current behavior is unclear and cannot be pinned by tests.
- Coverage is too weak to detect regressions and characterization tests are not feasible.
- The "problem" turns out to be a defect → `investigate-bug.md`.
