# Workflow 07 — Testing and Verification

## Purpose

Establish with evidence whether the change meets its acceptance criteria and does not break existing behavior.

## When to invoke

- After every implementation at Tier 1 and above.
- During remediation (Workflow 09).
- On request, to assess an area's test coverage.

## Required inputs

- Acceptance criteria.
- The change and the code under test.
- Test tooling and run instructions from the repository.
- Baseline results from Workflow 06.

## Relevant agents

- **Test Engineer** — leads.
- **Implementation Engineer** — fixes defects found (as a separate task).

## Steps

1. Determine how tests are run in this repository.
2. Map each acceptance criterion to tests. Identify gaps.
3. Identify boundary conditions and failure paths relevant to the change.
4. Add missing tests in proportion to risk.
5. Run unit, integration, and other relevant suites. Run type checks, linters, and build if they exist.
6. Record exact commands and results.
7. Classify each failure: defect in the change, pre-existing defect, test defect, or environment problem.
8. Report remaining coverage gaps and their risk.
9. Write the report using `templates/test-plan.md` (Tier 2+) or inline summary (Tier 1).
10. Complete `checklists/testing.md`.

## Deliverables

- Test report: coverage of acceptance criteria, commands run, actual results, failures and causes, gaps.

## Verification criteria

- Results are observed, not inferred.
- New failures are distinguished from pre-existing ones.
- No assertion was weakened, test skipped, or behavior mocked away to obtain a pass.

## Completion criteria

- All acceptance criteria are verified or have a documented, user-acknowledged gap.
- No new failures remain unexplained.

## Escalation conditions

- Defects found in approved scope.
- Critical paths cannot be tested.
- Test environment cannot be established.

## Stop conditions

- Stop and report if tests cannot be run at all; do not substitute claims for results.
- Stop if the only way to pass is to weaken a test or control.
