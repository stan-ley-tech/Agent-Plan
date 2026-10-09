# Checklist: Testing

Use at the end of Workflow 07. Mark items N/A with a reason.

## Expected behavior

- [ ] Each acceptance criterion maps to at least one test or a documented manual check.
- [ ] Business rules and invariants are tested.

## Boundaries

- [ ] Empty, minimum, maximum, and just-outside-range inputs.
- [ ] Invalid formats and types at trust boundaries.
- [ ] Domain-specific edges (time zones, currency rounding, unicode, duplicates) where relevant.

## Failure paths

- [ ] Dependency failures and timeouts.
- [ ] Unauthorized and forbidden access.
- [ ] Invalid state transitions.
- [ ] Concurrent operations where they can conflict.

## Regression

- [ ] Each fixed defect has a test that fails without the fix.
- [ ] Existing suites still pass, or failures are classified.

## Test quality

- [ ] Tests check behavior, not implementation details.
- [ ] Tests are deterministic and isolated.
- [ ] No assertions weakened, skips added, or behavior under test mocked away.
- [ ] Test data is synthetic; no real personal data or secrets.

## Execution results

- [ ] Exact commands recorded.
- [ ] Actual results recorded (pass, fail, skip counts).
- [ ] Each failure classified: defect, pre-existing, test issue, or environment.
- [ ] Anything not run is listed with the reason.

## Gaps

- [ ] Untested behavior listed with risk and recommendation.
