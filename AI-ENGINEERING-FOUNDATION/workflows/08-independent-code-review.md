# Workflow 08 — Independent Code Review

> **Lifecycle:** 07 Testing and Verification → **08 Independent Code Review** → 09 Remediation and Reverification (if findings) or 10 Documentation. Iterative; see "Workflow lifecycle" in `README.md`.

## 1. Purpose

Have someone other than the author examine the actual change and try to prove it wrong before it is accepted.

It exists because authors, human or AI, review their own work through their intentions. Independent review catches defects, regressions, and unnecessary complexity that the author and the author's tests did not.

## 2. When to Use

Use when:

- Required for Tier 2 and Tier 3 changes. Recommended for Tier 1.
- Any change touching a trust boundary, persistent data, or a public interface, before merge.
- Reverifying findings after remediation (Workflow 09).

Do not use when:

- Tier 0 changes.

## 3. Required Inputs

- The diff, obtained from version control by the reviewer.
- Requirements and acceptance criteria.
- Relevant design documents and ADRs.
- Test report from Workflow 07 (as information, not as proof).

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Code Reviewer | Leads; **read-only**; must not be the author. |
| Security Engineer | In-depth security review in addition, for Tier 3 or changes to authentication, authorization, sensitive data, or secrets. |
| Database Specialist | Reviews migrations and transaction logic when present. |
| API and Integration Specialist | Reviews contract changes when present. |
| Performance Engineer | When hot paths or large data volumes are affected. |

### Independence in practice

- Best: a separate subagent or a fresh session that starts from the diff and requirements only.
- Otherwise: a clearly separated review pass in the same session — re-read the requirements, obtain the diff fresh, and review it as someone else's work.
- State in the report which approach was used. A same-session review is weaker and must say so.

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Obtain the diff | Get the change and the list of changed files from version control. Ignore the implementer's summary until after the review. | — |
| 2. Requirements first | Read the criteria and design so you know what the code should do before seeing what it does. | — |
| 3. Read in context | Read each changed file in full, plus callers, consumers, and tests. | 1 |
| 4. Challenge the change | For each change ask: what input, state, timing, or failure makes this wrong? Trace main, error, and edge paths. | 2–3 |
| 5. Review areas | Correctness; regressions; architecture fit (respects boundaries and patterns); security; data integrity and database concerns (transactions, constraints, migrations); API concerns (contract, compatibility, errors); error handling; reliability (timeouts, retries, partial failure); performance (obvious inefficiencies in changed paths); maintainability; unnecessary complexity and filler; tests (would they fail if the behavior broke? were any weakened?). | 4 |
| 6. Run checks | Run tests and checks; do not accept reported results without seeing them. | 1 |
| 7. Specialist escalation | Request specialist review where the triggers above apply. | 5 |
| 8. Findings | Write each finding with severity, evidence, location, impact, and fix. | 5–7 |
| 9. Verdict | Approve / Approve with minor findings / Changes required / Blocked. | 8 |

## 6. Investigation Requirements

- Review the actual diff, never a description of it.
- Read surrounding code; most regressions live in callers, not in the changed lines.
- Verify claims in comments, commit messages, and the implementation report against the code.
- Run the tests yourself where possible.

## 7. Decision Rules

- Assume the change may be wrong until the evidence shows otherwise. Another agent's report of success is not evidence.
- Concrete defects outrank style preferences. Do not block on taste; style is the formatter's and linter's job.
- Every finding is specific, located, and actionable.
- Severity reflects realistic impact (see `principles/engineering-standards.md`).
- If the change is too large to review reliably, say so and recommend splitting it rather than approving it partially.
- The verdict follows from the findings: any open Critical or High finding means Changes required or Blocked.

## 8. Expected Deliverables

- Review report (`templates/code-review-report.md`, saved in `docs/reviews/` for Tier 2+): verdict, scope reviewed, independence approach, findings ordered by severity (severity, evidence label, file:line, problem, impact, recommended fix), checks run with actual results, outstanding concerns, areas not reviewed.

## 9. Verification / Completion Criteria

- The reviewer inspected the actual diff and its context.
- Every finding has severity, evidence, location, and a fix.
- Check results are actual, or listed as not run.
- Workflow ends with Approve or Approve with minor findings, or hands findings to Workflow 09.
- `checklists/code-review.md` applied.

## 10. Escalation Conditions

- Critical or High findings.
- Evidence that tests or controls were weakened.
- The change exceeds approved scope.
- Findings imply a design flaw → Workflow 03 or 04.

## 11. Failure / Stop Conditions

- Stop if the diff cannot be obtained.
- Stop if the reviewer is the author and no separation is possible; report that independent review was not achieved.
- The reviewer does not fix code during review. Fixes go through Workflow 09.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/08-independent-code-review.md acting
as the Code Reviewer (agents/code-reviewer.md). Remain read-only.
Change: [BRANCH / COMMIT RANGE / PR]  Base: [BASE]
Requirements: [AC IDS OR SPEC REFERENCE]

1. Obtain the diff yourself. Read the requirements before the code.
2. Read every changed file in full, with callers, consumers, and tests.
3. Challenge each change: what input, state, timing, or failure breaks it?
4. Review correctness, regressions, architecture fit, security, data and API
   concerns, error handling, reliability, performance, maintainability,
   unnecessary complexity, and test quality.
5. Run tests and checks; report actual results.
6. Request specialist review where triggers apply.
7. Report findings by severity with evidence and file:line, state the
   independence approach used, and give a verdict.
Do not modify the code. Do not approve on the strength of reported success.
```
