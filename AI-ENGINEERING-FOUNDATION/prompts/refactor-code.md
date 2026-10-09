# Prompt: Refactor Code

```text
Task: Improve the structure of the code below without changing its behavior.

Target: [FILES, MODULE, OR AREA]
Intended improvement: [GOAL, e.g. "make pricing rules testable", "remove duplicated validation"]
Constraints: [ANY, OR "NONE"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/principles/code-quality.md (especially
  "Refactoring discipline" and "Duplication")
- AI-ENGINEERING-FOUNDATION/agents/implementation-engineer.md
- AI-ENGINEERING-FOUNDATION/workflows/08-independent-code-review.md

Process:
1. Restate the goal as a concrete, checkable outcome. If the goal is vague,
   propose one and wait for my confirmation.
2. Inspect the target code, its callers, and its tests.
3. Assess regression risk: what depends on this code, and how well is current
   behavior covered by tests?
4. If coverage is insufficient, first add characterization tests that pin
   current behavior. Run them and confirm they pass before refactoring.
5. Plan the refactor as small, behavior-preserving steps.
6. Apply the steps, running tests after each.
7. Run all relevant checks; report actual results.
8. Independent review focused on behavior preservation (workflows/08).

Quality and safety:
- Do not change behavior, public interfaces, or data formats unless I approve.
- Do not refactor areas outside the target.
- Do not introduce abstractions without a stated benefit; prefer removing
  complexity over adding it.
- Stop when the stated goal is reached.

Deliverables:
- The refactor, any characterization tests, a short before/after explanation,
  test results, and review result.

Verification:
- The same tests pass before and after. Any test changes are explained
  (tests should only change if they were coupled to internals).

Ask me if the refactor would require changing behavior or public interfaces,
or if it grows beyond the target area.
```
