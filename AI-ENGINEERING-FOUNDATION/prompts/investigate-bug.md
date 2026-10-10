# Prompt: Investigate Bug

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** investigation per this prompt → 06 (focused fix) → 07 (regression and verification) → 08 for Tier 2+ → 09 if review finds issues.

## 1. Purpose

Find the actual root cause of a reported defect, fix it with the smallest correct change, and prove the fix with a regression test.

## 2. When to Use

Use when something behaves differently from what it should.

Use something else when:

- The "bug" is a request for new behavior → `implement-feature.md`.
- The problem is slowness or resource use → `performance-review.md`.
- You suspect a vulnerability → `security-review.md` first.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Bug description | What goes wrong | |
| Expected behavior | What should happen | Essential; without it the AI must ask. |
| Actual behavior | What happens instead | |
| Reproduction steps | How to trigger it | "Unknown" is acceptable. |
| Evidence | Error messages, logs, stack traces, screenshots, request IDs | Paste or reference; redact secrets and personal data. |
| Environment | Where it occurs, version, frequency | |

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/investigate-bug.md
(sections 5–8).

Bug: [BUG DESCRIPTION]
Expected behavior: [EXPECTED]
Actual behavior: [ACTUAL]
Reproduction steps: [STEPS, OR "UNKNOWN"]
Evidence: [ERRORS / LOGS / TRACES, OR "NONE"]
Environment: [ENVIRONMENT, VERSION, FREQUENCY]

Rules:
- Do not edit code until the root cause is established, even if the reported
  location looks suspicious.
- Reproduce the failure where practical, preferably as a failing test.
- Form more than one hypothesis and test them against evidence. The first
  plausible explanation is not the root cause until it explains every symptom.
- Distinguish symptoms from causes. Do not mask the bug (catch-and-ignore,
  special-casing the reported input) without my approval.
- Fix with the smallest correct change. No unrelated changes.
- Act as the Implementation Engineer and Test Engineer
  (agents/implementation-engineer.md, agents/test-engineer.md).
- Label the root cause Verified only if reproduced and confirmed; otherwise Likely.
```

## 5. Execution Sequence

1. **Establish the failure**: restate the bug; assign a risk tier; reproduce it (failing test, script, or documented steps). If it cannot be reproduced, record what was tried.
2. **Inspect evidence**: logs, error messages, stack traces, recent changes in version control history touching the area.
3. **Trace execution**: follow the path from entry point to failure through the actual code.
4. **Hypothesize**: list candidate causes; for each, what evidence would confirm or refute it.
5. **Test hypotheses** until one explains every observed symptom; separate cause from symptoms.
6. **Determine impact**: affected components, data (is any data already corrupted?), users, and whether the same pattern exists elsewhere.
7. **Evaluate fixes**: at least two for non-trivial causes; choose the smallest that fixes the cause.
8. **Fix** (Workflow 06).
9. **Regression test**: confirm it failed before the fix and passes after.
10. **Verify** (Workflow 07): relevant suites; check related behavior.
11. **Review** (Workflow 08) for Tier 2+.
12. **Report.**

## 6. Expected Output

- Reproduction: method and result, or what was tried.
- Root cause with evidence (file:line, trace, or reproduction), labeled Verified or Likely.
- Symptoms vs cause explanation.
- Affected components and any existing data impact.
- Fix options considered and the reason for the choice.
- Changed files.
- Regression test: name, result before fix, result after fix.
- Commands run and actual results.
- Same-pattern occurrences found elsewhere (reported, not fixed without approval).

## 7. Completion Criteria

- Root cause identified and explains all observed symptoms.
- A regression test fails without the fix and passes with it (or the reason no automated test is feasible, with a documented manual verification).
- Relevant suites pass, or remaining failures are pre-existing and classified.
- The diff contains only the fix and its tests.
- Tier 2+: independently reviewed.

## 8. Stop / Escalation Conditions

Stop and ask when:

- Expected behavior is unclear or disputed.
- The bug cannot be reproduced and any fix would be speculative.
- The bug has corrupted or exposed data, or is a security weakness → report before fixing.
- The correct fix requires a design, schema, or contract change.
- Reproduction would require production access or real user data.
