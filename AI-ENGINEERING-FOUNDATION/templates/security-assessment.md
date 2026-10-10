# Security Assessment: [SCOPE]

| | |
| --- | --- |
| Scope | [REPOSITORY / FEATURE / COMMIT RANGE] |
| Type | [Design-level / Code-level] |
| Deployment context | [PUBLIC / INTERNAL / LOCAL / UNKNOWN] |
| Date | [YYYY-MM-DD] |
| Assessed by | Security Engineer ([HOW: SUBAGENT / SEPARATE SESSION / SEPARATE PASS]) |

Severity levels and evidence labels: see `principles/engineering-standards.md`.

## 1. Summary

[Two to four sentences: overall risk picture, count of findings by severity, most important action.]

| Critical | High | Medium | Low | Info |
| --- | --- | --- | --- | --- |
| [N] | [N] | [N] | [N] | [N] |

## 2. Assets

| Asset | Sensitivity | Location |
| --- | --- | --- |
| [ASSET, e.g. "CUSTOMER ADDRESSES"] | [HIGH / MEDIUM / LOW] | [WHERE STORED OR PROCESSED] |

## 3. Trust boundaries

| Boundary | Entry points | Controls |
| --- | --- | --- |
| [BOUNDARY] | [ROUTES / HANDLERS / INPUTS] | [CONTROLS PRESENT] |

## 4. Threats

| Threat | Actor | Entry point | Relevant asset |
| --- | --- | --- | --- |
| [THREAT] | [ACTOR] | [ENTRY POINT] | [ASSET] |

## 5. Attack scenarios

### [SCENARIO NAME]
[Step-by-step description of how an actor could exploit the system.]

## 6. Existing controls

| Control | Where | Assessed effectiveness |
| --- | --- | --- |
| [CONTROL] | [FILE / COMPONENT] | [EFFECTIVE / PARTIAL / INEFFECTIVE / NOT VERIFIED] |

## 7. Findings

### [SEV-N] [TITLE]

| | |
| --- | --- |
| Severity | [Critical / High / Medium / Low / Info] |
| Evidence | [Verified / Likely / Unverified concern] |
| Location | [path/to/file:line] |

- Description: [WHAT IS WRONG]
- Evidence detail: [CODE REFERENCE, TOOL OUTPUT, OR REPRODUCTION STEPS — NEVER SECRET VALUES]
- Impact: [CONSEQUENCE IF EXPLOITED]
- Remediation: [SPECIFIC FIX]
- Verification requirement: [HOW THE FIX WILL BE PROVEN, e.g. "AUTOMATED TEST: OTHER TENANT'S RECORD RETURNS 404"]
- Status: [Open / Fix attempted / Reverified / Accepted risk]

## 8. Tools run

| Tool / check | Result |
| --- | --- |
| [TOOL OR "NOT RUN — REASON"] | [ACTUAL OUTPUT SUMMARY] |

## 9. Scope not assessed

- [AREAS NOT REVIEWED AND WHY]

## 10. Residual risks

| Risk | Reason it remains | Owner |
| --- | --- | --- |
| [RISK] | [REASON] | [WHO ACCEPTED IT] |

This assessment reports what was examined and found. It is not a guarantee that the system is secure.
