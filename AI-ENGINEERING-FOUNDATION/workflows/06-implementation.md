# Workflow 06 — Implementation

> **Lifecycle:** 05 Security Assessment → **06 Implementation** → 07 Testing and Verification. Iterative; see "Workflow lifecycle" in `README.md`.
> Standards: `principles/code-quality.md`, `principles/engineering-standards.md`.

## 1. Purpose

Build approved scope as a sequence of small, tested, reviewable changes that fit the existing codebase.

It exists to keep implementation controlled: focused diffs, tests written alongside code, existing conventions respected, and no silent scope growth or uncontrolled rewrites.

## 2. When to Use

Use when:

- Requirements are approved, and for Tier 2+ the relevant design (Workflows 03–05) is approved.
- Fixing confirmed findings (as part of Workflow 09).
- Any Tier 1+ code change.

Do not use when:

- Acceptance criteria are missing or ambiguous (return to Workflow 02).
- The change requires an unapproved architectural, schema, or contract decision (return to 03 or 04).
- Tier 0: make the change directly and run the fastest relevant check.

## 3. Required Inputs

- Approved acceptance criteria for the work package.
- Relevant design: architecture, data and API design, security requirements.
- `docs/implementation-plan.md` for Tier 2+.
- The repository, with the ability to run build and tests where available.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Implementation Engineer | Leads; plans and writes the change and its tests. |
| Test Engineer | Advises on test design for Tier 2+; owns Workflow 07. |
| Database Specialist | Consulted when the work includes migrations. |
| API and Integration Specialist | Consulted when the work implements contracts or integrations. |
| Engineering Orchestrator | Holds scope, tracks work units, triggers review gates. |

The Implementation Engineer is never the only reviewer of its own work (Workflow 08).

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Confirm readiness | Acceptance criteria approved; design approved for Tier 2+; risk tier stated. | — |
| 2. Inspect existing code | Read the code to change, its tests, callers, and neighboring code. Identify conventions and abstractions already available. | 1 |
| 3. Baseline | Run the relevant tests, type checks, and linters. Record pre-existing failures. | 2 |
| 4. Implementation plan | List work units in dependency order, typically: migrations → data access → domain logic → interfaces → UI or integration wiring. Each unit is independently testable. Share the plan for Tier 2+ before large changes. | 2–3 |
| 5. Incremental changes | Implement one unit at a time; run relevant tests after each. Keep each commit coherent. | 4 |
| 6. Tests alongside code | For each unit, add or update tests for its acceptance criteria, boundaries, and failure paths. | 5 |
| 7. Error handling and validation | Validate input at trust boundaries; decide recover, retry, translate, or propagate for each failure; keep data consistent on partial failure. | 5 |
| 8. Observability | Add logging, metrics, or health information that operators need for new behavior, following existing patterns; no secrets or unnecessary personal data. | 5 |
| 9. Migrations | Implement per the Workflow 04 plan; run forward and backward on a local or disposable database. | 4 |
| 10. Integration work | Implement timeouts, retries, and idempotency per the design; use test doubles at process boundaries in tests. | 4 |
| 11. Self-review | Review the diff with `checklists/implementation.md`; remove unrelated changes. | 5–10 |
| 12. Full checks and report | Run all relevant checks; report using the format in `agents/implementation-engineer.md`; hand off to Workflow 07 and, where required, 08. | 11 |

## 6. Investigation Requirements

- Read before writing: the target code, its tests, its callers, and at least one comparable feature to learn conventions.
- Search for existing helpers, validators, error types, and patterns before creating new ones.
- Identify every consumer of an interface you change.
- Establish the test baseline before changing code so new failures can be distinguished from old ones.

## 7. Decision Rules

- Build exactly the approved scope. Improvements noticed along the way are reported as recommendations.
- Reuse existing abstractions and conventions. If an existing pattern is harmful, propose changing it separately; do not introduce a second pattern beside it.
- Prefer the smallest change that correctly meets the criteria.
- **No large uncontrolled rewrites.** Rewriting or restructuring an existing module requires its own approved scope and justification. If the diff grows well beyond the plan, stop and re-plan.
- No new dependency without justification; new major dependencies require approval.
- No placeholder code presented as complete.
- Do not weaken tests, validation, or security controls to make progress.

## 8. Expected Deliverables

- The code change, organized as coherent commits.
- Tests for each acceptance criterion, plus relevant boundaries and failure paths.
- Migrations, if planned, with local forward/backward results.
- Implementation report: criteria-to-test mapping, files changed and why, commands run with actual results, baseline failures, deviations, limitations, recommendations not implemented.
- Documentation updates for affected behavior, or a note for Workflow 10.

## 9. Verification / Completion Criteria

- Every acceptance criterion is demonstrated by a test or a documented manual check.
- All relevant checks were run, with actual results reported; anything not run is stated with the reason.
- The diff contains only in-scope changes.
- Implementation is **Reported**, not complete, until it passes Workflow 07 and, where required, Workflow 08.

## 10. Escalation Conditions

- Acceptance criteria are ambiguous or contradictory → Workflow 02.
- Design does not fit the existing code → Workflow 03 or 04.
- The change requires a breaking change, new major dependency, or destructive migration → user approval.
- Baseline failures block verification.
- A security issue is discovered → Security Engineer.

## 11. Failure / Stop Conditions

- Stop if work requires scope beyond the approved criteria.
- Stop if the diff is growing into a rewrite; re-plan and seek approval.
- Stop before destructive operations, shared-database migrations, or any deployment.
- Stop if the only way forward is to weaken a test or control.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/06-implementation.md acting as the
Implementation Engineer (agents/implementation-engineer.md).
Work package: [WORK PACKAGE]  Acceptance criteria: [AC IDS OR TEXT]

1. Confirm criteria and design are approved; state the risk tier.
2. Read the target code, tests, callers, and a comparable feature. Reuse
   existing abstractions.
3. Run a baseline of tests and checks; record pre-existing failures.
4. Plan work units in dependency order; share the plan for Tier 2+.
5. Implement one unit at a time with tests alongside; handle errors and
   validation deliberately; add observability per existing patterns.
6. Run migrations only locally; implement integration timeouts/retries per design.
7. Self-review with checklists/implementation.md; remove unrelated changes.
8. Run all relevant checks and report exact commands and actual results.
No scope expansion, no rewrites, no weakened tests. Hand off for testing
and independent review.
```
