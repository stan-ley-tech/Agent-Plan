# Workflow 07 — Testing and Verification

> **Lifecycle:** 06 Implementation → **07 Testing and Verification** → 08 Independent Code Review. Iterative; see "Workflow lifecycle" in `README.md`.

## 1. Purpose

Establish with evidence whether the implementation meets its requirements and keeps existing behavior intact.

It exists because "it compiles" and "the tests are green" are not the same as "it works". Verification ties each requirement to an executed test with an observed result, and states honestly what remains unproven.

## 2. When to Use

Use when:

- After every Tier 1+ implementation.
- During remediation, to verify fixes (Workflow 09).
- On request, to assess an area's real coverage or test reliability.

Do not use when:

- Tier 0 changes: run the fastest relevant check only.

## 3. Required Inputs

- Acceptance criteria and business rules.
- The change and the code under test.
- Baseline results from Workflow 06.
- Security findings' verification requirements (Workflow 05), where applicable.
- Performance NFRs, where applicable.
- Test tooling and run instructions from the repository.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Test Engineer | Leads; designs, runs, and reports. |
| Implementation Engineer | Fixes defects found, as a separate task. |
| Security Engineer | Supplies security verification requirements; confirms security tests prove the control. |
| Database Specialist | Advises on database and migration tests. |
| Performance Engineer | Only when NFRs set performance targets. |

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Test environment | Determine how tests run (scripts, configuration, CI). Record runtime versions, services, and data setup. Use local or disposable environments only. | — |
| 2. Baseline | Run existing relevant suites; record results to separate new failures from old. | 1 |
| 3. Requirement mapping | Map every acceptance criterion and business rule to existing or planned tests. List unmapped items. | — |
| 4. Unit tests | Business rules and logic through public interfaces. | 3 |
| 5. Integration tests | Components with real collaborators where practical (database, file system, queues). | 3 |
| 6. Database tests | Constraints reject invalid data; migrations run forward and backward; transactions keep data consistent under failure and concurrency. | 3 |
| 7. API tests | Contracts, status codes, error shapes, validation, pagination, authorization (including access to other users' or tenants' resources). | 3 |
| 8. End-to-end tests | Only for critical user workflows where lower-level tests cannot give confidence. | 3 |
| 9. Edge cases | Empty, minimum, maximum, just out of range, invalid formats, duplicates, time zones, rounding, unicode, as relevant to the domain. | 4–8 |
| 10. Failure paths | Dependency failure, timeout, invalid state transitions, partial failure, concurrent conflicting operations. | 4–8 |
| 11. Regression | Each fixed defect has a test that fails without the fix; full relevant suites rerun. | 4–8 |
| 12. Security verification | Execute the verification requirements from security findings; negative tests for authentication, authorization, and validation. | 4–8 |
| 13. Performance considerations | Only against stated NFRs; label local measurements as indicative. Escalate measured problems to the Performance Engineer. | 4–8 |
| 14. Execute and classify | Run everything relevant; classify each failure as defect in the change, pre-existing defect, test defect, or environment problem. | 4–13 |
| 15. Evidence and gaps | Report results and remaining coverage gaps with their risk. | 14 |

## 6. Investigation Requirements

- Read the code under test and its branches to find boundaries and failure paths; do not test from the specification alone.
- Check that each new test fails when the behavior is broken, by reasoning or by temporarily breaking the code locally (then restoring it).
- Inspect existing tests for weakened assertions, skips, or mocks that hide the behavior under test.
- Investigate every failure before classifying it.

## 7. Decision Rules

- Tests verify behavior and requirements. **Coverage percentage is informational, never the goal or the completion criterion.**
- Use the lowest test level that can credibly verify a behavior.
- Mock at process boundaries; prefer real collaborators inside them.
- A flaky test is a defect. Fix it or quarantine it with a recorded reason; never retry until green and report a pass.
- Never weaken an assertion, broaden a tolerance, add a skip, or mock away the behavior under test to obtain a pass.
- Test effort is proportional to risk: Tier 3 paths get failure-path and security tests; a copy change does not.

## 8. Expected Deliverables

- New or updated tests.
- Test report (`templates/test-plan.md` for Tier 2+; a concise summary for Tier 1) containing: requirement-to-test mapping with results; exact commands; pass/fail/skip counts; each failure with classification and evidence; security verification results; coverage gaps with risk and recommendation.

## 9. Verification / Completion Criteria

- Every acceptance criterion is verified by an executed test or documented manual check, or has a gap the user has acknowledged.
- Every security verification requirement in scope is executed.
- No new failure is unexplained.
- Every reported result was observed in this session; anything not run is listed with the reason.
- No test was weakened to pass.
- `checklists/testing.md` applied.

## 10. Escalation Conditions

- A defect in approved scope → Workflow 09.
- Tests reveal a design problem → Workflow 03 or 04.
- A critical path cannot be tested → user decides whether to accept the gap.
- The test environment cannot be established.
- Pre-existing failures hide the results of the current change.

## 11. Failure / Stop Conditions

- Stop and report if tests cannot be run at all; do not substitute claims for results.
- Stop if the only way to pass is to weaken a test or a control.
- Do not run tests against production or shared environments, or with real personal data or secrets.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/07-testing-and-verification.md acting
as the Test Engineer (agents/test-engineer.md).
Scope: [CHANGE / FEATURE]  Acceptance criteria: [AC IDS OR TEXT]

1. Determine the test environment; run a baseline.
2. Map every acceptance criterion and business rule to tests.
3. Add unit, integration, database, API, and (only where warranted)
   end-to-end tests, covering edge cases, failure paths, and regressions.
4. Execute security verification requirements and negative access tests.
5. Consider performance only against stated NFRs.
6. Run all relevant suites; report exact commands and actual results;
   classify every failure.
7. Report gaps with risk. Coverage percentage is not a goal. Never weaken
   assertions, add skips, or mock away the behavior under test.
```
