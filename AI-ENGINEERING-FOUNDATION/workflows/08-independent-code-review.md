# Workflow 08 — Independent Code Review

## Purpose

Have someone other than the author judge the actual change for correctness, security, data integrity, regressions, and maintainability before it is accepted.

## When to invoke

- Required for Tier 2 and Tier 3 changes. Recommended for Tier 1.
- Before merging any change that touches a trust boundary, data, or a public interface.

## Required inputs

- The diff, obtained from version control by the reviewer.
- Requirements and acceptance criteria.
- Design documents and ADRs relevant to the change.
- Test results from Workflow 07.

## Relevant agents

- **Code Reviewer** — leads; read-only; must not be the author.
- **Security Engineer** — independent security review in addition, for Tier 3 or any change touching authentication, authorization, sensitive data, or secrets.
- **Performance Engineer** — consulted when the change affects hot paths or large data volumes.
- **Database Specialist** — consulted when the change includes migrations.

## Independence in practice

If real subagents or a separate session are available, run the review there, starting from the diff and requirements only. If not, perform the review as a clearly separated pass: re-read the requirements, obtain the diff fresh, and review it as if someone else wrote it. State which approach was used. A single-session self-review is weaker; say so in the report.

## Steps

1. Obtain the diff and the list of changed files.
2. Read requirements before reading code.
3. Review each changed file in full context, including callers and tests.
4. Check correctness, regressions, security, data integrity, error handling, compatibility, tests, and unnecessary complexity.
5. Run tests and checks if available; do not rely on reported results alone.
6. Apply `checklists/code-review.md`.
7. Write findings with severity, evidence label, file and line, impact, and fix.
8. Give a verdict: Approve, Approve with minor findings, Changes required, or Blocked.
9. Write the report using `templates/code-review-report.md` in `docs/reviews/` for Tier 2+.

## Deliverables

- Code review report with prioritized findings and verdict.

## Verification criteria

- Every finding is located and actionable.
- The reviewer inspected the actual diff.
- Check results are actual.

## Completion criteria

- Verdict is Approve or Approve with minor findings, or the change goes to Workflow 09.

## Escalation conditions

- Critical or High findings.
- Evidence of weakened tests or controls.
- Scope exceeded.

## Stop conditions

- Stop if the diff cannot be obtained.
- Stop and recommend splitting if the change is too large to review reliably.
- The reviewer does not fix code during review.
