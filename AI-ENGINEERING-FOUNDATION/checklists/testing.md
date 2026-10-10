# Checklist: Testing

Gate for `workflows/07-testing-and-verification.md` and `prompts/test-and-verify.md`.

**Rules:** tick `[x]` only when a test was executed and its result observed in this session, or a manual check is documented. Mark items that do not apply `N/A — reason`. Coverage percentage is not evidence of verified behavior. Never weaken a test to tick an item.

## Required — Requirements

- [ ] Requirements identified
- [ ] Acceptance criteria identified (IDs recorded)
- [ ] Test scenarios mapped to requirements; unmapped criteria listed

## Required — Unit Testing

- [ ] Core logic and business rules tested
- [ ] Edge cases tested (empty, min, max, out of range, invalid formats, domain-specific edges)
- [ ] Error conditions tested

## Conditional — Integration Testing

- [ ] Database behavior tested (constraints, transactions, migrations forward/back) — if data persists
- [ ] External integrations tested, with test doubles at process boundaries — where relevant
- [ ] API behavior tested (contracts, status codes, error shapes, pagination) — if interfaces exist
- [ ] Authentication/authorization tested — if access is restricted

## Conditional — End-to-End (where critical workflows justify it)

- [ ] Critical user flows tested
- [ ] Failure scenarios tested
- [ ] Important integrations tested

## Required — Regression

- [ ] Previous functionality checked (relevant suites rerun)
- [ ] Affected areas checked
- [ ] Known bugs covered (each fix has a test that fails without it)

## Conditional — Security (where relevant)

- [ ] Authorization tested, including access to other users' or tenants' resources
- [ ] Validation tested with invalid and malicious input
- [ ] Abuse cases tested
- [ ] Sensitive data exposure checked (responses, logs, errors)
- [ ] Verification methods from security findings executed

## Conditional — Performance (where NFRs exist)

- [ ] Baseline established
- [ ] Critical paths measured (local measurements labeled indicative)
- [ ] Bottlenecks investigated or escalated to the Performance Engineer

## Evidence

- [ ] Test commands recorded exactly
- [ ] Test results recorded (pass / fail / skip counts, failing test names)
- [ ] Failures investigated and classified (defect / pre-existing / test issue / environment)
- [ ] No assertions weakened, skips added, or behavior mocked away
- [ ] Known gaps documented with risk
- [ ] Final verification completed on the code being handed off

**Final Status**

```text
All acceptance criteria verified: YES / NO (gaps acknowledged by user: YES / NO)
New unexplained failures: __
Commands and results:
Known gaps:
Report location (templates/test-plan.md for Tier 2+):
```
