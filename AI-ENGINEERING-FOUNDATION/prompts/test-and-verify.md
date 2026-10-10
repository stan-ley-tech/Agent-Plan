# Prompt: Test and Verify

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 07 Testing and Verification. Defects found go to Workflow 09.

## 1. Purpose

Determine what behavior must be proven, create the tests needed to prove it, run them, and report actual evidence — including what remains unproven.

## 2. When to Use

Use after an implementation, before a release, to verify fixes, or to assess an area's real coverage.

Use something else when:

- You also need the feature built → `implement-feature.md` (it includes testing).
- You are tracking down a specific failure → `investigate-bug.md`.
- The concern is speed → `performance-review.md`.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Scope | Feature, change, branch, or area | |
| Requirements | Acceptance criteria or spec reference | Or "use `docs/project-specification.md`". |
| Known risks | Areas you are worried about | Optional. |
| Security findings | Findings whose fixes need verification | Optional; reference the report. |

Do not describe how to run tests; the AI will discover it.

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/test-and-verify.md
(sections 5–8) acting as the Test Engineer (agents/test-engineer.md), using
workflows/07-testing-and-verification.md.

Scope: [SCOPE]
Requirements: [AC / SPEC REFERENCE]
Known risks: [RISKS, OR "NONE"]
Security findings to verify: [REPORT, OR "NONE"]

Rules:
- Inspect requirements, the code under test, and existing tests first.
- Every result you report must have been observed in this session. If
  something could not be run, say so and why. Never invent results.
- Never weaken assertions, broaden tolerances, add skips, or mock away the
  behavior under test to get a pass.
- Coverage percentage is not a goal; verified behavior is.
- Do not change production code; report defects.
- Use local or disposable environments and synthetic data only.
```

## 5. Execution Sequence

1. **Understand requirements**: list testable behaviors from acceptance criteria and business rules.
2. **Inspect existing tests** and how they run; run a baseline.
3. **Map** behaviors to existing tests; identify gaps.
4. **Create tests** at the lowest credible level:
   - unit tests for logic and rules;
   - integration tests with real collaborators where practical;
   - API tests for contracts, errors, validation, and authorization;
   - end-to-end tests only where critical workflows justify them.
5. **Edge cases** and **failure paths** relevant to the domain and code branches.
6. **Regression tests** for fixed defects.
7. **Security verification** where relevant: negative authorization and validation tests; execute verification methods from security findings.
8. **Execute** all relevant suites and checks.
9. **Classify** each failure: defect in the change, pre-existing defect, test defect, or environment problem.
10. **Report** evidence and gaps.

## 6. Expected Output

- Behavior → test mapping with actual results.
- Tests added or changed.
- Exact commands and results (pass/fail/skip counts, failing test names).
- Each failure with classification and evidence.
- Security verification results, where relevant.
- Gaps: untested behavior, risk, recommendation.
- For Tier 2+, a report from `templates/test-plan.md`.

## 7. Completion Criteria

- Every acceptance criterion is verified by an executed test or documented manual check, or has a gap the user acknowledged.
- Every new failure is investigated and classified.
- Every reported result was observed; anything not run is listed with the reason.
- No test was weakened to obtain a pass.

## 8. Stop / Escalation Conditions

Stop and report when:

- Tests cannot be run at all (do not substitute claims for results).
- Acceptance criteria are untestable or unclear.
- The only way to pass is to weaken a test or control.
- A defect is found in approved scope (hand to Workflow 09).
- Testing requires production systems, real personal data, or secrets.
