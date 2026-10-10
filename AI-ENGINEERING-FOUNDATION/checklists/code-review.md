# Checklist: Code Review

Gate for `workflows/08-independent-code-review.md` and `prompts/code-review.md`. Use as a final sweep after reading the diff in context; it does not replace tracing the code.

**Rules:** tick `[x]` only after inspecting the actual diff and surrounding code. Mark items that do not apply `N/A — reason`. "Looks good" is not a review result: every concern is recorded as a finding with evidence, or the item is left unticked.

## Required — Independence

- [ ] Reviewer is not the author (or the lack of independence is stated in the report)
- [ ] Diff obtained directly from version control
- [ ] Requirements read before the code

## Required — Correctness

- [ ] Requirements satisfied (each acceptance criterion checked against the code)
- [ ] Behavior correct on main paths
- [ ] Edge cases handled
- [ ] Failure paths handled
- [ ] Callers and consumers of changed code still work (no regressions)

## Required — Architecture

- [ ] Changes fit the existing architecture and boundaries
- [ ] Responsibilities are appropriate
- [ ] Unnecessary coupling avoided
- [ ] Unnecessary complexity avoided (speculative abstractions, unused options, filler)

## Required — Code Quality

- [ ] Code is understandable
- [ ] Duplication is justified/controlled
- [ ] Error handling is appropriate (nothing swallowed, nothing leaked across boundaries)
- [ ] Abstractions are justified
- [ ] Naming is clear and uses domain terms
- [ ] Style issues raised only where they break an established project standard

## Conditional — Security (if the change touches inputs, access, data, or configuration)

- [ ] Authentication reviewed
- [ ] Authorization reviewed, including resource ownership
- [ ] Input validation reviewed
- [ ] Sensitive data handling reviewed
- [ ] Secrets reviewed (none introduced)
- [ ] Security regressions considered
- [ ] Security Engineer review requested — for Tier 3 or trust-boundary changes

## Conditional — Database/API (if schema or contracts change)

- [ ] Migrations safe for existing data; reversibility and ordering stated
- [ ] Transactions and constraints protect integrity
- [ ] Contract changes compatible, or breaking change approved

## Conditional — Performance (if hot paths or large data are touched)

- [ ] Expensive operations reviewed
- [ ] Database queries reviewed (N+1, unbounded, missing indexes)
- [ ] Network calls reviewed (timeouts, sequential calls)
- [ ] Concurrency considerations reviewed
- [ ] Unnecessary work identified

## Required — Testing

- [ ] Tests cover important behavior
- [ ] Regression coverage exists where needed
- [ ] Tests are meaningful (would fail if the behavior broke)
- [ ] No tests weakened, skipped, or deleted without justification
- [ ] Tests and checks run by the reviewer; actual results recorded (or "not run" with reason)

## Final Review

- [ ] Findings categorized: confirmed issues / risks / suggestions / questions
- [ ] Severity assigned to every confirmed issue
- [ ] Evidence recorded (file:line, trace, failing input, or output)
- [ ] Unresolved issues documented
- [ ] Recommendation recorded: Approve / Approve with minor findings / Changes required / Blocked

**Final Status**

```text
Verdict:
Open Critical/High: __ (any open → Changes required or Blocked)
Independence approach: SUBAGENT / SEPARATE SESSION / SEPARATE PASS
Checks run and results:
Report location:
```
