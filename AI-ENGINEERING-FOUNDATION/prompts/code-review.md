# Prompt: Code Review

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent — ideally in a fresh session or subagent that did not write the change. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 08 Independent Code Review. Fixes go through Workflow 09 as a separate, authorized task.

## 1. Purpose

Independently review an actual change, challenge its assumptions, and report concrete, evidence-backed problems before it is accepted.

## 2. When to Use

Use for any Tier 2–3 change before merge, recommended for Tier 1, and for reviewing a pull request or branch.

Use something else when:

- You want a security-focused assessment → `security-review.md` (in addition, for Tier 3 or trust-boundary changes).
- You want an area of the codebase assessed rather than a specific change → `existing-repository.md` or `security-review.md`.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Change | Branch, commit range, or pull request | |
| Base | Base branch or commit | e.g. `main`. |
| Requirements | Acceptance criteria, issue, or spec reference | Needed to judge correctness. |
| Focus | Any area of particular concern | Optional. |

Do not paste a summary of the change; the reviewer must read the diff itself.

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/code-review.md
(sections 5–8) acting as the Code Reviewer (agents/code-reviewer.md), using
workflows/08-independent-code-review.md.

Change: [BRANCH / COMMIT RANGE / PR]
Base: [BASE]
Requirements: [AC / ISSUE / SPEC REFERENCE]
Focus: [AREAS, OR "NONE"]

Rules:
- You are read-only. Do not modify the code under review.
- Obtain the diff yourself from version control. Read requirements before code.
- Assume the change may be wrong; challenge its assumptions. Another agent's
  report of success is not evidence.
- Report concrete problems with file:line evidence. Style preferences are not
  defects unless they violate an established project standard (cite it).
- If you wrote this change, say so: independent review is not achieved.
- Run tests and checks yourself where possible; report actual results.
```

## 5. Execution Sequence

1. **Obtain** the diff and changed-file list.
2. **Understand intent**: read requirements and relevant design before the code.
3. **Read in context**: each changed file in full, plus callers, consumers, and tests.
4. **Challenge**: for each change, what input, state, timing, or failure makes it wrong?
5. **Review**: correctness; regressions; architecture fit; security; performance in changed paths; reliability (timeouts, retries, partial failure); error handling; database changes (migrations, transactions, constraints); API changes (contracts, compatibility, errors); testing quality (would tests fail if behavior broke? weakened or skipped tests?); maintainability; unnecessary complexity and filler.
6. **Run** tests and checks.
7. **Escalate** to specialists where triggers apply (security, database, API, performance).
8. **Classify** every item (section 6).
9. **Verdict** and **report**.

## 6. Expected Output

A report from `templates/code-review-report.md` with items separated into:

| Category | Evidence label | Meaning |
| --- | --- | --- |
| **Confirmed issues** | Verified | Defects demonstrated by code reading trace, failing input, or test. Each with severity, file:line, impact, fix. |
| **Risks** | Likely / Unverified concern | Probable problems not demonstrated; what would confirm them. |
| **Suggestions** | Recommendation | Improvements that are not defects. |
| **Questions** | Open question | Things the reviewer needs answered to judge correctness. |

Also: verdict (Approve / Approve with minor findings / Changes required / Blocked), scope reviewed, independence approach, checks run with actual results, areas not reviewed. A verdict without listed evidence ("looks good") is not acceptable.

## 7. Completion Criteria

- The actual diff and its context were inspected.
- Every confirmed issue has severity, file:line, impact, and a fix.
- Items are correctly separated into the four categories.
- Check results are actual or listed as not run.
- The verdict follows from the findings: open Critical or High → Changes required or Blocked.

## 8. Stop / Escalation Conditions

Stop and report when:

- The diff cannot be obtained.
- The change is too large to review reliably → recommend splitting.
- Requirements are unavailable, so correctness cannot be judged → ask.
- Tests or security controls appear to have been weakened.
- The change exceeds its approved scope.
- A finding implies a design flaw (flag for Workflow 03 or 04).
