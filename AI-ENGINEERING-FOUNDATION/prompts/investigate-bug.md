# Prompt: Investigate Bug

```text
Task: Find the root cause of the bug below, fix it with a focused change,
and prove the fix with a regression test.

Bug: [BUG DESCRIPTION]
Expected behavior: [EXPECTED]
Actual behavior: [ACTUAL]
Steps to reproduce: [STEPS, OR "UNKNOWN"]
Evidence: [ERROR MESSAGES, LOGS, SCREENSHOTS, OR "NONE"]
Environment: [WHERE IT HAPPENS, VERSION]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/implementation-engineer.md
- AI-ENGINEERING-FOUNDATION/agents/test-engineer.md
- AI-ENGINEERING-FOUNDATION/workflows/06-implementation.md and
  07-testing-and-verification.md

Process:
1. Restate the bug. Assign a risk tier.
2. Reproduce it where practical, preferably as a failing automated test.
   If you cannot reproduce it, say so and explain what you tried.
3. Investigate. Read the relevant code paths, recent changes in version
   control history, and logs. Form more than one hypothesis.
4. Test hypotheses against evidence. Do not accept the first plausible
   explanation; confirm the root cause explains every observed symptom.
5. Evaluate fix options (at least two if the cause is non-trivial). Prefer
   the one that fixes the cause, not the symptom, with the smallest safe change.
6. Implement the fix. Keep it focused.
7. Confirm the regression test now passes and failed before the fix.
8. Run the relevant suites; report actual results.
9. Check for the same defect pattern elsewhere and report (do not fix
   unrelated instances without approval).
10. For Tier 2+, independent review (workflows/08).

Quality and safety:
- Do not mask the bug (catching and ignoring the error, adding a special
  case for the reported input) unless I approve it as a temporary mitigation.
- If the bug involves data corruption or a security weakness, stop and report
  before fixing.

Deliverables:
- Root cause with evidence, options considered, the fix, regression test,
  test results, and related instances found.

Verification:
- The regression test fails without the fix and passes with it.
- Root cause is labeled Verified only if reproduced; otherwise Likely.

Ask me if the bug cannot be reproduced and the fix would be speculative, or
if the correct behavior is unclear.
```
