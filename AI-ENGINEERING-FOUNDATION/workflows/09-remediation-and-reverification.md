# Workflow 09 — Remediation and Reverification

> **Lifecycle:** 08 Independent Code Review (or 05, 07) → **09 Remediation and Reverification** → back to the workflow that raised the findings, then 10 Documentation. Iterative; see "Workflow lifecycle" in `README.md`.

## 1. Purpose

Resolve findings from testing, security assessment, or code review, and prove with evidence that each one is actually fixed without introducing new problems.

It exists because "I changed the code" is not "the issue is fixed". A finding closes only when independent evidence shows the problem no longer occurs.

## 2. When to Use

Use when:

- Workflow 05, 07, 08, or 12 produced findings that must be addressed.
- A previously accepted risk is being remediated.

Do not use when:

- The finding is really a new feature or requirement; treat it as a change request (Workflow 02).

## 3. Required Inputs

- The findings, each with severity, location, evidence, and (for security findings) verification requirement.
- The original requirements and design.
- The current code, tests, and the report that raised each finding.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Implementation Engineer | Analyzes root cause and implements fixes. |
| Test Engineer | Adds regression tests; runs targeted and full verification. |
| Code Reviewer / Security Engineer | Whoever raised the finding reverifies it. Never the implementer. |
| Engineering Orchestrator | Tracks each finding's state and escalates decisions. |

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Classification | Classify each finding: **Confirmed** (reproduced or evident in code), **Not reproducible** (return to raiser with what was tried), **Duplicate**, **Disputed** (reasoned disagreement recorded), or **New scope** (becomes a change request). | — |
| 2. Prioritization | Order confirmed findings: Critical and High first; then by dependency (fixes that unblock others); then Medium and Low. Confirm with the user any that are expensive or disputed. | 1 |
| 3. Root-cause analysis | For each confirmed finding: why it happened, not only where. Check whether the same pattern exists elsewhere. | 2 |
| 4. Remediation | Focused fix addressing the root cause. One finding (or one root cause) per change; no unrelated edits. | 3 |
| 5. Regression prevention | Add a test that fails without the fix and passes with it; for security findings, implement the stated verification requirement. Where the same pattern exists elsewhere, report it (fix only with approval). | 4 |
| 6. Targeted testing | Run the regression test and the tests around the changed code. | 5 |
| 7. Full reverification | Rerun the full relevant suites and checks. Hand back to the original reviewer, who reverifies against the finding using the actual diff. | 6 |
| 8. Unresolved findings | Record anything not fixed with state, reason, and owner in `docs/project-status.md`. | 7 |
| 9. Residual risk acceptance | For findings the user chooses not to fix: record who accepted, when, why, and revisit conditions. | 8 |

### Finding states

`Open` → `Fix attempted` → `Reverified` (closed). Other terminal states: `Disputed` (with recorded reasoning), `Accepted risk` (user decision).

A finding moves to `Reverified` only when **both** exist: passing regression evidence and reverification by the role that raised it.

## 6. Investigation Requirements

- Confirm each finding before fixing it: reproduce it, or show the defect in the code.
- Analyze root cause before choosing a fix; a fix to the symptom is recorded as a mitigation, not a resolution.
- Search the codebase for the same defect pattern.
- After fixing, check the fix did not change behavior elsewhere (callers, related tests).

## 7. Decision Rules

- **Never mark a finding resolved because code was changed.** Evidence decides.
- Fix root causes; temporary mitigations require user approval and stay open as findings.
- Smallest fix that addresses the root cause; refactoring beyond that is separate scope.
- Only the user accepts residual risk. Critical findings cannot be accepted for a release (`principles/engineering-standards.md`); High findings can be accepted only explicitly by the user.
- Disagreements between implementer and reviewer are resolved on evidence; the orchestrator records the outcome or escalates.

## 8. Expected Deliverables

- Fixes and regression tests.
- Updated finding register: each finding with classification, root cause, fix reference, regression test, verification results, reverifier, and final state.
- Updated reports (status fields in the review or security report).
- Unresolved findings and accepted risks recorded in `docs/project-status.md`.

## 9. Verification / Completion Criteria

- Every Critical and High finding is `Reverified`, or `Accepted risk` (High only) with recorded user approval.
- Every `Reverified` finding has a regression test result and reverifier confirmation.
- Full relevant suites pass, or remaining failures are classified and pre-existing.
- No new Critical or High issues were introduced by the fixes.
- Remaining findings are recorded with owner and state.

## 10. Escalation Conditions

- A fix requires design change → Workflow 03 or 04.
- A fix requires scope expansion → Workflow 02.
- Implementer and reviewer disagree on a consequential finding.
- A fix cannot be verified (no feasible test, no reproduction).
- The same defect pattern is widespread.

## 11. Failure / Stop Conditions

- Stop if a fix would require weakening a test or control.
- Stop if fixes introduce new Critical or High issues; return them to review.
- Do not close findings without reverification evidence.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/09-remediation-and-reverification.md.
Findings: [REPORT LOCATION OR LIST]

1. Classify each finding: Confirmed, Not reproducible, Duplicate, Disputed,
   or New scope. Prioritize Critical and High first.
2. For each confirmed finding, find the root cause and check for the same
   pattern elsewhere.
3. Implement a focused fix (agents/implementation-engineer.md) and a
   regression test that fails without it; for security findings, implement
   the stated verification requirement.
4. Run targeted tests, then full relevant suites; report actual results.
5. Hand back to the role that raised each finding for reverification
   against the actual diff.
6. Mark a finding Reverified only with regression evidence and reverifier
   confirmation. Record unresolved findings and user-accepted risks in
   docs/project-status.md.
```
