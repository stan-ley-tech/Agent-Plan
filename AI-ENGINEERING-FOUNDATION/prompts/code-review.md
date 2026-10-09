# Prompt: Code Review

```text
Task: Independently review the change below and report prioritized findings.

Change: [BRANCH / COMMIT RANGE / PULL REQUEST]
Base: [BASE BRANCH OR COMMIT, e.g. "main"]
Requirements: [ACCEPTANCE CRITERIA, ISSUE, OR SPEC REFERENCE]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/code-reviewer.md
- AI-ENGINEERING-FOUNDATION/workflows/08-independent-code-review.md
- AI-ENGINEERING-FOUNDATION/principles/code-quality.md
- AI-ENGINEERING-FOUNDATION/checklists/code-review.md

You are read-only for this task. Do not modify the code under review.

Process:
1. Obtain the diff yourself from version control (base...change). Do not rely
   on any summary of the change.
2. Read the requirements before the code.
3. Read every changed file in full context, plus callers, consumers, and tests.
4. Check: correctness in main, error, and edge paths; regressions;
   security (authorization, validation, data exposure, secrets, injection);
   data integrity (transactions, concurrency, migrations); error handling;
   compatibility; test quality (would tests fail if the behavior broke? were
   any weakened or skipped?); unnecessary complexity and AI-generated filler.
5. Run tests and checks if available; report actual results.
6. Apply checklists/code-review.md.
7. If the change touches authentication, authorization, sensitive data, or
   secrets, recommend an additional security review (prompts/security-review.md).

Quality and safety:
- Prioritize concrete defects over style preferences.
- Do not approve on the strength of another agent's reported success.
- If the change is too large to review reliably, say so and suggest a split.

Deliverables:
- A report from templates/code-review-report.md: verdict, scope reviewed,
  findings most severe first (severity, evidence label, file:line, problem,
  impact, fix), checks run, outstanding concerns.

Verification:
- Every finding cites file and line.
- Check results are actual, or listed as not run.

Fixes are a separate remediation task (workflows/09) that I must authorize.
```
