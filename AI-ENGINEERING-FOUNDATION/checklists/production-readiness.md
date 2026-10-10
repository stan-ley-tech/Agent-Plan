# Checklist: Production Readiness

Gate for `workflows/12-production-readiness.md`, `prompts/production-readiness.md`, and `templates/release-readiness-report.md`.

**Rules:** every ticked item needs evidence that applies to **this release scope** (report, command output on the release commit, or file). Missing or stale evidence is a blocker, not a pass. Mark items that do not apply `N/A — reason`. Completing this checklist does not authorize deployment.

Release scope: `[VERSION / BRANCH / COMMIT RANGE]`

## Required — Requirements

- [ ] Required functionality complete (nothing half-built reachable by users)
- [ ] Acceptance criteria satisfied (verification report referenced)
- [ ] Scope confirmed from version control

## Required — Testing

- [ ] Required tests pass on the release commit
- [ ] Regression testing complete
- [ ] Critical failures resolved
- [ ] Known test gaps documented

## Required — Security

- [ ] Security assessment completed and covers this scope
- [ ] No open Critical findings
- [ ] High findings resolved or explicitly accepted by the user (acceptance recorded)
- [ ] Authentication verified
- [ ] Authorization verified
- [ ] Secrets protected (secret store; none in repository or logs)
- [ ] Sensitive data protected

## Required — Reliability

- [ ] Failure handling reviewed for new paths
- [ ] Retries/timeouts reviewed for new integrations
- [ ] Dependency failures considered
- [ ] Health checks available — where the system is deployed as a service

## Conditional — Performance (if NFRs exist or critical paths changed)

- [ ] Critical paths evaluated against targets
- [ ] Known bottlenecks addressed or accepted
- [ ] Resource requirements understood

## Required — Observability

- [ ] Logs available for new critical paths (no sensitive data)
- [ ] Useful metrics available
- [ ] Alerts defined where necessary, with named recipients
- [ ] Health/status visibility available

## Conditional — Database (if data or migrations are in scope)

- [ ] Migrations reviewed and tested on realistic data
- [ ] Migration safety considered (locking, duration, ordering with deploy, reversibility)
- [ ] Irreversible steps approved, with forward-fix plan
- [ ] Indexes reviewed
- [ ] Backups considered (taken immediately before irreversible steps)
- [ ] Recovery process considered; last verified restore recorded

## Required — Deployment

- [ ] Production configuration verified (every required value defined)
- [ ] Secrets configured in the target environment
- [ ] Deployment process verified (rehearsed in a non-production environment where one exists)
- [ ] Rollback process verified for code, configuration, and data
- [ ] Environment differences understood

## Required — Operations

- [ ] Documentation complete for user-visible, API, configuration, and operational changes
- [ ] Troubleshooting guidance available
- [ ] Ownership established (who deploys, who watches, who is alerted)
- [ ] Operational responsibilities understood

## Final Decision

Apply the decision rules in `workflows/12-production-readiness.md`:

| Outcome | Requires |
| --- | --- |
| **READY** | Every required item ticked with current evidence; no open Critical or High findings. |
| **READY WITH CONDITIONS** | No open Critical findings; every open High finding explicitly accepted by the user; every remaining gap covered by a documented condition with evidence, owner, and deadline. |
| **NOT READY** | Any open Critical finding, unaccepted High finding, missing evidence in a required area, unapproved irreversible step, or no rollback path. |

Select one:

- [ ] **READY**
- [ ] **READY WITH CONDITIONS**
- [ ] **NOT READY**

```text
Decision evidence (reports, commands, files):

Blockers (finding — severity — evidence — action to unblock):

Conditions (condition — evidence — owner — deadline):

Accepted risks (risk — accepted by — date):

Report location:
```

- [ ] Deployment awaits explicit user authorization for this release.
