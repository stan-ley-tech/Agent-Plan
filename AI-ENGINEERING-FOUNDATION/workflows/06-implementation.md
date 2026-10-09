# Workflow 06 — Implementation

## Purpose

Build approved scope as focused, tested, maintainable changes that fit the existing codebase.

## When to invoke

- Any code change at Tier 1 and above, once requirements (and design, for Tier 2+) are approved.

## Required inputs

- Acceptance criteria for the work package.
- Relevant design: architecture, data/API design, security requirements.
- Implementation plan (Tier 2+).
- Repository with runnable build and tests where available.

## Relevant agents

- **Implementation Engineer** — leads.
- **Test Engineer** — consulted on test design for Tier 2+.
- **Engineering Orchestrator** — tracks scope and gates.

## Steps

1. Confirm the acceptance criteria. Ask if any are unclear.
2. Inspect the relevant code, tests, and callers. Identify conventions.
3. Run existing tests for the area; record the baseline, including pre-existing failures.
4. Write a short plan: files, approach, tests. For Tier 2+, share it before large changes.
5. Implement in small steps, running relevant tests as you go.
6. Add or update tests for each acceptance criterion, boundaries, and failure paths.
7. Update documentation affected by the change, or flag it for Workflow 10.
8. Run the full relevant checks: tests, type checks, linters, build.
9. Self-review the diff with `checklists/implementation.md`.
10. Report results using the output format in `agents/implementation-engineer.md`.
11. Hand off to Workflow 07 and, for Tier 2+, Workflow 08.

## Deliverables

- The code change.
- Tests.
- Implementation report with actual check results.

## Verification criteria

- Every acceptance criterion is demonstrated by a test or a documented manual check.
- All relevant checks were run, with results reported exactly.
- The diff contains only in-scope changes.

## Completion criteria

- Implementation report delivered with evidence. The work is not complete until it passes Workflow 07 and, where required, Workflow 08.

## Escalation conditions

- Ambiguous criteria, design mismatch, required breaking change, new major dependency, discovered security issue.

## Stop conditions

- Stop if the work requires scope beyond the approved criteria.
- Stop if baseline failures prevent verifying the change; report and ask.
- Stop before any destructive operation, shared-database migration, or deployment.
