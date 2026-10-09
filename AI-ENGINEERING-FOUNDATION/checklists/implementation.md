# Checklist: Implementation

Self-review before handing a change to testing and independent review. Mark items N/A with a reason when they do not apply.

## Scope

- [ ] Every change traces to an approved requirement, acceptance criterion, or confirmed defect.
- [ ] No unrelated refactoring, formatting churn, or opportunistic changes.
- [ ] No new dependency without justification; major ones approved.

## Code quality

- [ ] Follows existing project conventions (structure, naming, error handling, tests).
- [ ] Names use domain terms and reveal intent.
- [ ] No speculative abstractions, unused options, placeholder code, or narrating comments.
- [ ] No dead or commented-out code added.

## Error handling and validation

- [ ] Each error is handled, translated, or propagated deliberately; none swallowed.
- [ ] Errors crossing a boundary do not leak internals or secrets.
- [ ] External input is validated at the trust boundary.
- [ ] Multi-step writes leave data consistent on failure.

## Security

- [ ] Authorization is checked for every protected operation, including resource ownership.
- [ ] No secrets in code, tests, logs, or examples.
- [ ] No security control weakened.

## Compatibility

- [ ] Callers and consumers of changed interfaces identified and updated or unaffected.
- [ ] Migrations are reversible or flagged; ordering with deploy is stated.
- [ ] Breaking changes approved.

## Tests

- [ ] Tests demonstrate each acceptance criterion.
- [ ] Boundary and failure paths covered in proportion to risk.
- [ ] No tests weakened, skipped, or deleted to obtain a pass.
- [ ] Relevant tests, type checks, linters, and build run; actual results recorded.

## Documentation

- [ ] Affected documentation updated, or flagged for Workflow 10.
- [ ] `docs/project-status.md` updated if project state changed.
