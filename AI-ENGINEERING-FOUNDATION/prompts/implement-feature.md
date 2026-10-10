# Prompt: Implement Feature

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 02 (only if criteria are missing) → 04 (if data or contracts change) → 05 (if a trust boundary is touched) → 06 → 07 → 08 → 09 (if findings) → 10.

## 1. Purpose

Implement one specified feature within approved scope, with impact analysis, tests, independent review, and evidence that it works.

## 2. When to Use

Use for a defined feature or a milestone from an implementation plan.

Use something else when:

- Something that should work is broken → `investigate-bug.md`.
- Behavior should stay the same but structure should improve → `refactor-code.md`.
- The feature needs a new schema or API designed first and you want design only → `design-database.md` / `design-api.md`.
- The project has no requirements or architecture yet → `new-project.md`.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Feature | What it should do, for whom | |
| Acceptance criteria | Observable conditions for "done" | Or ask the AI to propose them for your approval. |
| Reference | Spec section, issue, or milestone ID | Optional. |
| Out of scope | Anything explicitly excluded | Optional but helpful. |
| Constraints | Deadlines, compatibility promises, technology limits | Only real ones. |

Do not describe the code layout; the AI will inspect it.

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/implement-feature.md
(sections 5–8).

Feature: [FEATURE DESCRIPTION]
Acceptance criteria: [CRITERIA, OR "PROPOSE THEM FOR MY APPROVAL"]
Reference: [SPEC / ISSUE / MILESTONE, OR "NONE"]
Out of scope: [EXCLUSIONS, OR "NONE STATED"]
Constraints: [CONSTRAINTS, OR "NONE"]

Rules:
- Inspect the relevant code, tests, callers, and conventions before changing
  anything. Assign a risk tier (principles/engineering-standards.md).
- Act as the Implementation Engineer (agents/implementation-engineer.md);
  involve specialists only where the orchestrator's triggers apply.
- Change only what the feature requires. No unrelated refactoring, no
  changes to unrelated functionality, no new major dependency without approval.
- Do not weaken tests or security controls.
- Independent review is required for Tier 2+: use a separate subagent or
  session if available; otherwise a clearly separated review pass starting
  from the diff. State which.
- Report exact commands and actual results. Do not claim completion without
  evidence.
```

## 5. Execution Sequence

1. **Analyze requirements**: confirm acceptance criteria; if missing or vague, propose them and wait (Workflow 02 scope).
2. **Inspect existing code**: target area, tests, callers, comparable features, existing abstractions.
3. **Impact analysis**: components, data, interfaces, consumers, and behavior affected; assign the risk tier.
4. **Architecture considerations**: does the feature fit existing boundaries? If not, stop for Workflow 03.
5. **Data/API implications**: if schema or contracts change, apply Workflow 04 and get approval for breaking or destructive changes.
6. **Security implications**: if a trust boundary, authentication, authorization, or sensitive data is involved, apply Workflow 05.
7. **Plan**: work units in dependency order; share the plan for Tier 2+.
8. **Baseline**: run relevant tests and checks.
9. **Implement incrementally** with tests alongside (Workflow 06).
10. **Test and verify** (Workflow 07): each criterion, boundaries, failure paths, regressions.
11. **Independent review** (Workflow 08); **remediate and reverify** findings (Workflow 09).
12. **Document** affected behavior (Workflow 10); update `docs/project-status.md`.
13. **Report.**

## 6. Expected Output

- Risk tier and impact analysis.
- Plan (for Tier 2+) and any design decisions with their drivers.
- Changed files, each with what changed and why.
- Acceptance criteria → test mapping with actual results.
- Commands run and results; baseline failures distinguished from new ones.
- Review report: findings by severity and their final state.
- Documentation updated.
- Deviations, limitations, and recommendations not implemented.

## 7. Completion Criteria

- Every acceptance criterion is demonstrated by an executed test or documented manual check.
- All relevant checks run, with actual results; nothing reported as passing that was not observed.
- The diff contains only in-scope changes.
- Tier 2+: independent review completed; Critical and High findings Reverified (or High explicitly accepted by the user).
- Affected documentation and project status updated.

## 8. Stop / Escalation Conditions

Stop and ask when:

- Acceptance criteria are ambiguous or the expected behavior is unclear.
- The feature requires an architectural change, a breaking API or schema change, a destructive migration, or a new major dependency.
- Security-critical behavior is uncertain (who may access what).
- The work grows beyond the agreed scope.
- Baseline failures prevent verification.
- A required dependency, service, or permission is unavailable.
