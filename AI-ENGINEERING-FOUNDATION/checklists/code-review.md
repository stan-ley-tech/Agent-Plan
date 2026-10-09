# Checklist: Code Review

Final sweep after reading the diff in context. It does not replace tracing the code. Mark items N/A with a reason.

## Independence and scope

- [ ] Reviewer is not the author.
- [ ] Diff obtained directly from version control.
- [ ] Requirements read before code.
- [ ] Change stays within approved scope.

## Correctness

- [ ] Main path meets each acceptance criterion.
- [ ] Error paths and edge cases behave correctly.
- [ ] Concurrent execution does not cause incorrect results.

## Regressions and compatibility

- [ ] Callers and consumers of changed code still work.
- [ ] API, schema, configuration, and file-format changes are compatible or approved as breaking.

## Security

- [ ] Authorization checked for each protected operation, including resource ownership.
- [ ] Input validated at boundaries; no injection paths.
- [ ] No sensitive data exposed in responses, logs, or errors.
- [ ] No secrets introduced.

## Data integrity

- [ ] Transactions wrap operations that must be atomic.
- [ ] Constraints enforce invariants.
- [ ] Migrations are safe for existing data and correctly ordered.

## Error handling

- [ ] No swallowed errors.
- [ ] Errors are translated appropriately at boundaries.

## Maintainability

- [ ] Code is readable and consistent with the codebase.
- [ ] No unnecessary abstractions, speculative options, narrating comments, or dead code.
- [ ] Duplication is reasonable.

## Tests

- [ ] Tests exercise new behavior and would fail if it broke.
- [ ] Failure paths are tested in proportion to risk.
- [ ] No tests weakened, skipped, or deleted without justification.
- [ ] Tests and checks were run by the reviewer, or their absence is noted.

## Report

- [ ] Every finding has severity, evidence label, file and line, impact, and fix.
- [ ] Verdict follows from findings.
