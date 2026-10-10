# Code Review: [CHANGE TITLE]

| | |
| --- | --- |
| Change | [BRANCH / COMMIT RANGE / PULL REQUEST] |
| Base | [BASE BRANCH OR COMMIT] |
| Requirements | [AC IDS / ISSUE / SPEC LINK] |
| Date | [YYYY-MM-DD] |
| Reviewed by | Code Reviewer ([HOW: SUBAGENT / SEPARATE SESSION / SEPARATE PASS]) |
| Verdict | [Approve / Approve with minor findings / Changes required / Blocked] |

Severity levels and evidence labels: see `principles/engineering-standards.md`.

## 1. Review scope

- Files reviewed: [LIST OR COUNT]
- Context reviewed: [CALLERS, TESTS, RELATED MODULES]
- Not reviewed: [ANYTHING EXCLUDED AND WHY]

## 2. Summary

[Two to four sentences: what the change does, overall quality, the most important issues.]

## 3. Findings

Most severe first.

### [N]. [TITLE] — `[path/to/file:line]`

| | |
| --- | --- |
| Category | [Confirmed issue / Risk / Suggestion / Question] |
| Severity | [Critical / High / Medium / Low / Info — confirmed issues and risks] |
| Evidence | [Verified / Likely / Unverified concern / Recommendation / Open question] |

- Problem: [WHAT IS WRONG, OR THE QUESTION]
- Evidence detail: [REASONING TRACE, FAILING INPUT, OR OUTPUT]
- Impact: [CONSEQUENCE]
- Recommended fix: [SPECIFIC CHANGE]
- Verification status: [Open / Fix attempted / Reverified / Disputed / Accepted risk]

## 4. Checks run

| Command | Result |
| --- | --- |
| [EXACT COMMAND OR "NOT RUN — REASON"] | [ACTUAL RESULT] |

## 5. Outstanding concerns

- [CONCERNS THAT ARE NOT DEFECTS BUT NEED ATTENTION, e.g. "RECOMMEND SECURITY REVIEW OF TOKEN HANDLING"]
