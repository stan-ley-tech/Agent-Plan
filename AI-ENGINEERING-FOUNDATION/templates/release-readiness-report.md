# Release Readiness Report: [VERSION]

| | |
| --- | --- |
| Release | [VERSION / BRANCH / COMMIT RANGE] |
| Target environment | [ENVIRONMENT] |
| Date | [YYYY-MM-DD] |
| Assessed by | Release and Reliability Engineer |
| Recommendation | [Ready / Ready with accepted risks / Not ready] |

This report is a recommendation. It does not authorize deployment.

## 1. Release scope

- Changes: [SUMMARY OR LINK TO CHANGELOG]
- Commits: [RANGE]
- Migrations: [LIST OR "NONE"]
- Configuration changes: [LIST OR "NONE"]

## 2. Test results

| Suite / command | Result | Run on (commit) |
| --- | --- | --- |
| [COMMAND] | [ACTUAL RESULT] | [COMMIT] |

## 3. Security status

- Assessment: [LINK; DOES IT COVER THIS SCOPE? YES / NO]
- Open findings: [COUNT BY SEVERITY]

## 4. Migration status

| Migration | Tested where | Reversible | Locking / duration risk | Ordering with deploy |
| --- | --- | --- | --- | --- |
| [MIGRATION] | [ENVIRONMENT] | [Yes / No] | [RISK] | [BEFORE / AFTER CODE] |

## 5. Configuration readiness

| Setting | Defined for target | Secret stored in secret store |
| --- | --- | --- |
| [SETTING] | [Yes / No] | [Yes / No / N/A] |

## 6. Observability

- Health checks: [WHAT THEY CHECK]
- Logs: [WHAT IS LOGGED FOR NEW PATHS]
- Metrics and alerts: [WHAT EXISTS; WHO IS NOTIFIED]

## 7. Rollback and recovery

- Rollback procedure: [STEPS OR LINK]
- Irreversible steps: [LIST OR "NONE"]
- Backups: [WHAT, WHERE, LAST VERIFIED RESTORE DATE OR "NOT VERIFIED"]

## 8. Known risks

| Risk | Severity | Mitigation | Accepted by |
| --- | --- | --- | --- |
| [RISK] | [SEVERITY] | [MITIGATION] | [NAME OR "NOT ACCEPTED"] |

## 9. Blocking findings

| Finding | Severity | Source | Required to unblock |
| --- | --- | --- | --- |
| [FINDING] | [SEVERITY] | [REPORT] | [ACTION] |

## 10. Recommendation

**[Ready / Ready with accepted risks / Not ready]**

[Reasoning in two to four sentences.]

Conditions for release:

- [CONDITION]
