# Checklist: Implementation

Gate for `workflows/06-implementation.md`. Use the Before Coding section before the first change, and the rest as the self-review before handing off to testing and independent review.

**Rules:** tick `[x]` only with evidence (file, diff, command output). Mark items that do not apply `N/A — reason`. Unticked items go under Final Status. The implementer's own checklist is not a substitute for independent review.

## Required — Before Coding

- [ ] Requirements and acceptance criteria understood (IDs or text recorded)
- [ ] Scope confirmed, including what is out of scope
- [ ] Risk tier assigned
- [ ] Architecture reviewed; change fits existing boundaries
- [ ] Affected components, callers, and consumers identified
- [ ] Dependencies identified (no new major dependency without approval)
- [ ] Testing strategy identified
- [ ] Baseline tests and checks run; pre-existing failures recorded

## Conditional — Before Coding

- [ ] Database changes identified and designed (Workflow 04) — if schema or data changes
- [ ] API changes identified and designed; compatibility assessed (Workflow 04) — if contracts change
- [ ] Security implications identified (Workflow 05) — if a trust boundary, authentication, authorization, secrets, or sensitive data is involved
- [ ] Breaking changes or destructive migrations approved by the user — if any

## Required — During Implementation

- [ ] Changes remain within scope
- [ ] Existing patterns and abstractions are respected and reused
- [ ] Unnecessary rewrites avoided; diff is proportionate to the task
- [ ] Error handling implemented deliberately (no swallowed errors)
- [ ] Validation implemented at trust boundaries
- [ ] Logging/observability considered, without secrets or unnecessary personal data
- [ ] No placeholder code presented as complete

## Conditional — During Implementation

- [ ] Security controls implemented as designed — if security requirements apply
- [ ] Migrations handled safely: reversible or flagged, run only locally, deploy ordering stated — if migrations exist
- [ ] Timeouts, retries, and idempotency implemented per design — if external integrations change

## Required — Testing

- [ ] Unit tests added/updated
- [ ] Edge cases tested
- [ ] Failure paths tested
- [ ] No tests weakened, skipped, or deleted to obtain a pass

## Conditional — Testing

- [ ] Integration tests added/updated — where components interact with real collaborators
- [ ] Regression tests added — where a defect is being fixed

## Verification

- [ ] Each acceptance criterion maps to a test or documented manual check
- [ ] Changed files reviewed in the diff
- [ ] Tests, type checks, linters, and build pass — exact commands and results recorded
- [ ] No unrelated changes introduced
- [ ] Known limitations and deviations documented
- [ ] Affected documentation updated or flagged for Workflow 10

**Final Status**

```text
Ready for testing and independent review: YES / NO
Commands run and results:
Unticked items and reasons:
Deviations / limitations:
```
