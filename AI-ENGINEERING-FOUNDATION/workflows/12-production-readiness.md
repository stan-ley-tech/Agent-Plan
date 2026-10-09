# Workflow 12 — Production Readiness

## Purpose

Decide on evidence whether a release is ready for production, and make the blockers and risks explicit.

## When to invoke

- Before releasing Tier 2 or Tier 3 changes to production.
- Before running migrations against production data.

## Required inputs

- Release scope (version, branch, or commit range).
- Test reports, code review reports, security assessments for the scope.
- Migration plan, deployment plan, configuration inventory.
- Monitoring, rollback, and recovery procedures.
- Open findings and known issues.

## Relevant agents

- **Release and Reliability Engineer** — leads; read-only.
- **Test Engineer**, **Security Engineer**, **Database Specialist**, **DevOps Engineer**, **Documentation Engineer** — provide or confirm evidence for their areas.
- **Engineering Orchestrator** — collects evidence and tracks blockers.

## Steps

1. Define release scope from version control.
2. Tests: current results for the release scope; failures explained.
3. Security: assessment current for the scope; Critical/High findings resolved or accepted.
4. Code review: all Tier 2+ changes reviewed; findings resolved.
5. Migrations: tested, ordered with deployment, reversibility known, data impact understood.
6. Configuration: every required value exists for the target environment; secrets in a secret store.
7. Observability: health checks, logs, metrics, and alerts for the release's critical paths.
8. Rollback: procedure defined; irreversible steps identified.
9. Recovery: backups exist and restore procedure is known; note when it was last exercised.
10. Documentation: updated for user-visible, API, configuration, and operational changes.
11. Compile open findings by severity.
12. Complete `checklists/production-readiness.md`.
13. Write `templates/release-readiness-report.md` in `docs/reviews/` with a recommendation.

## Deliverables

- Release readiness report with recommendation: **Ready**, **Ready with accepted risks**, or **Not ready**, and a list of blockers.

## Verification criteria

- Every area cites evidence specific to this release scope.
- Missing evidence is recorded as a finding, not assumed to be fine.

## Completion criteria

- Report delivered to the user. The user decides whether and when to deploy.

**A passing readiness assessment does not authorize deployment.** Deployment requires explicit user authorization for that specific release.

## Escalation conditions

- Any open Critical finding (blocks release).
- Open High findings (block unless the user explicitly accepts the risk).
- Irreversible migrations or missing rollback path.

## Stop conditions

- Stop at the recommendation. Do not deploy, merge to a release branch, or run production migrations as part of this workflow.
