# Prompt: Production Readiness

```text
Task: Assess whether the release below is ready for production and produce
a release-readiness report. Do not deploy.

Release: [VERSION / BRANCH / COMMIT RANGE]
Target environment: [ENVIRONMENT NAME]
Planned release date: [DATE, OR "NOT SET"]
Known issues: [LIST, OR "NONE KNOWN"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/release-reliability-engineer.md
- AI-ENGINEERING-FOUNDATION/workflows/12-production-readiness.md
- AI-ENGINEERING-FOUNDATION/checklists/production-readiness.md
- Reports in docs/reviews/ and docs/project-status.md

You are read-only for this task. Do not modify code or configuration.

Process:
1. Define the release scope from version control.
2. Collect and check evidence for each area, specific to this scope:
   - Tests: run them; report actual results.
   - Code review: Tier 2+ changes reviewed; findings resolved or accepted.
   - Security: assessment covers the scope; Critical/High resolved or accepted.
   - Migrations: tested; ordering with deployment; reversibility; data impact.
   - Configuration: all required values defined for the target environment;
     secrets in a secret store.
   - Observability: health checks, logs, metrics, alerts for critical paths.
   - Rollback: procedure for code, configuration, and data; irreversible steps.
   - Recovery: backups and restore procedure; when last exercised.
   - Documentation: updated for user-visible, API, configuration, and
     operational changes.
3. Treat missing or stale evidence as a finding.
4. Walk through deployment and rollback step by step; identify failure points.
5. List open findings by severity.
6. Apply checklists/production-readiness.md.

Quality and safety:
- Open Critical findings block release. Open High findings block unless I
  explicitly accept the risk.
- Do not deploy, merge to release branches, run production migrations, or
  change production configuration.

Deliverables:
- docs/reviews/release-readiness-[VERSION].md from
  templates/release-readiness-report.md, ending with a recommendation:
  READY, READY WITH CONDITIONS, or NOT READY, plus blockers and
  conditions for release.

Verification:
- Every area cites evidence for this release scope.

The deployment decision is mine. A READY outcome is not
authorization to deploy.
```
