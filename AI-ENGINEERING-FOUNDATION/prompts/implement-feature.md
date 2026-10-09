# Prompt: Implement Feature

```text
Task: Implement the feature below within its approved scope, with tests and
independent review.

Feature: [FEATURE DESCRIPTION]
Acceptance criteria: [ACCEPTANCE CRITERIA, OR "DERIVE AND CONFIRM WITH ME"]
Related requirement or issue: [REFERENCE, OR "NONE"]
Out of scope: [EXCLUSIONS, OR "NONE STATED"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/principles/code-quality.md
- AI-ENGINEERING-FOUNDATION/workflows/06-implementation.md,
  07-testing-and-verification.md, 08-independent-code-review.md,
  09-remediation-and-reverification.md
- AI-ENGINEERING-FOUNDATION/agents/implementation-engineer.md
- docs/project-specification.md and docs/architecture.md, if present

Process:
1. Assign a risk tier (principles/engineering-standards.md) and state it.
2. If acceptance criteria are missing or vague, propose them and wait for my
   confirmation.
3. Inspect the relevant code, tests, callers, and conventions.
4. For Tier 2+: if the feature changes data or interfaces, apply
   workflows/04-data-and-api-design.md; if it touches a trust boundary, apply
   workflows/05-security-assessment.md. Share the plan before large changes.
5. Run baseline tests. Implement in small steps following existing conventions.
6. Add tests for each acceptance criterion, boundaries, and failure paths.
7. Run all relevant checks and report actual results.
8. Independent review (workflows/08). Use a separate subagent or session if
   available; otherwise do a clearly separated review pass starting from the
   diff. Include a security review for Tier 3 or trust-boundary changes.
9. Fix confirmed findings and reverify (workflows/09).
10. Update affected documentation and docs/project-status.md.

Quality and safety:
- No unrelated refactoring, no scope expansion, no new major dependency
  without approval.
- Do not weaken tests or security controls.
- Do not run destructive operations, shared-database migrations, or deploy.

Deliverables:
- The change, tests, implementation report, review report, and status update.

Verification:
- Map each acceptance criterion to the test or check that proves it, with
  actual results. Report review findings and their resolution state.

Ask me when acceptance criteria are ambiguous, when the work needs scope or
design changes, or when a finding requires a decision.
```
