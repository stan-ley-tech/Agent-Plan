# Workflow 09 — Remediation and Reverification

## Purpose

Fix confirmed findings from review, testing, or security assessment, and prove with evidence that each fix works and broke nothing else.

## When to invoke

- After Workflow 07, 08, or 05 produces confirmed findings that must be fixed.

## Required inputs

- The findings to address, with severity and location.
- The original requirements.
- The current code and tests.

## Relevant agents

- **Implementation Engineer** — implements fixes.
- **Test Engineer** — adds regression tests and reruns suites.
- **Code Reviewer** or **Security Engineer** — whoever raised the finding reverifies it. Not the implementer.
- **Engineering Orchestrator** — tracks each finding's state.

## Steps

1. List findings to address, ordered by severity. Confirm which are in scope with the user if any are disputed or expensive.
2. For each finding, confirm it is real (reproduce or re-read). If it is not, record why and return it to the reviewer.
3. Implement a focused fix. Do not combine unrelated changes.
4. Add a regression test that fails without the fix, where practical.
5. Rerun the relevant tests and checks; record results.
6. Hand back to the original reviewer for reverification against the finding.
7. Track each finding as: Open → Fix attempted → Reverified, or Disputed, or Accepted risk (user decision).
8. Document unresolved findings in `docs/project-status.md`.

## Deliverables

- Fixes and regression tests.
- Updated finding list with state and evidence for each.

## Verification criteria

- Each fix has evidence: regression test result and reviewer reverification.
- No new failures introduced.

## Completion criteria

- All Critical and High findings are Reverified or explicitly accepted by the user.
- Remaining findings are recorded.

**An attempted fix is not a verified fix.** Do not report a finding as resolved until reverification evidence exists.

## Escalation conditions

- A fix requires design change or scope expansion.
- A finding is disputed between roles.
- A fix cannot be verified.

## Stop conditions

- Stop if fixing requires weakening a control or a test.
- Stop if a fix introduces new Critical or High issues; return to review.
