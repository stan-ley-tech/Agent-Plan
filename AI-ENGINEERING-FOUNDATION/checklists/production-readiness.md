# Checklist: Production Readiness

Use with Workflow 12. Every item needs evidence specific to this release scope. Missing evidence is a finding. Completing this checklist does not authorize deployment.

## Scope

- [ ] Release scope defined from version control (commits, migrations, configuration changes).

## Tests

- [ ] Relevant suites run on the release commit; actual results recorded.
- [ ] Failures resolved or explicitly accepted.

## Review and security

- [ ] All Tier 2+ changes independently reviewed.
- [ ] Security assessment covers the release scope.
- [ ] No open Critical findings.
- [ ] Open High findings resolved or explicitly accepted by the user.

## Configuration

- [ ] Every required setting defined for the target environment.
- [ ] Secrets stored in the platform's secret store, not the repository.
- [ ] Configuration validated at startup.

## Migrations

- [ ] Migrations tested on a non-production database with realistic data.
- [ ] Ordering relative to code deployment defined.
- [ ] Reversibility known; irreversible steps approved.
- [ ] Locking and duration risk assessed.

## Observability

- [ ] Health checks reflect real readiness.
- [ ] New critical paths are logged without sensitive data.
- [ ] Alerts exist for critical failures, with a named recipient.

## Rollback and recovery

- [ ] Rollback procedure defined for code, configuration, and data.
- [ ] Irreversible steps identified with a forward-fix plan.
- [ ] Backups exist; restore procedure known and date of last verified restore recorded.

## Documentation

- [ ] User-visible, API, configuration, and operational changes documented.
- [ ] Release notes or changelog updated if the project uses them.

## Decision

- [ ] Blockers listed.
- [ ] Outcome stated: READY, READY WITH CONDITIONS, or NOT READY; every blocker and condition cites evidence.
- [ ] Deployment awaits explicit user authorization.
