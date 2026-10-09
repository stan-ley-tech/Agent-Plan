# Prompt: Test and Verify

```text
Task: Determine and execute the right verification for the scope below,
and report what is actually proven.

Scope: [FEATURE / CHANGE / BRANCH / AREA]
Acceptance criteria: [CRITERIA, OR "USE docs/project-specification.md"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/test-engineer.md
- AI-ENGINEERING-FOUNDATION/workflows/07-testing-and-verification.md
- AI-ENGINEERING-FOUNDATION/checklists/testing.md

Process:
1. Discover how tests, type checks, linters, and builds run in this repository
   (scripts, configuration, CI files).
2. Run the existing relevant suites to get a baseline.
3. Map each acceptance criterion to tests. Identify untested criteria.
4. Identify boundaries and failure paths relevant to the scope.
5. Add missing tests in proportion to risk. Each new test must be able to
   fail if the behavior breaks.
6. Run all relevant checks. Record exact commands and results.
7. Classify each failure: defect in the change, pre-existing defect, test
   defect, or environment problem, with evidence.
8. List remaining gaps and their risk.

Quality and safety:
- Never invent or assume successful results.
- Never weaken assertions, add skips, broaden tolerances, or mock away the
  behavior under test.
- Do not change production code; report defects instead.
- Do not run tests against production or shared environments.
- Use synthetic test data; never real personal data or secrets.

Deliverables:
- Test report (templates/test-plan.md for Tier 2+; a concise summary
  otherwise): criteria coverage, commands and results, failures and causes,
  gaps.

Verification:
- Every result in the report was observed in this session.
- If something could not be run, the report says so and why.

Ask me if acceptance criteria cannot be tested as written, or if the test
environment cannot be established.
```
