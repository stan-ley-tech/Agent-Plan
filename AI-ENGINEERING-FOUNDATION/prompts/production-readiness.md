# Prompt: Production Readiness

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 12 Production Readiness, drawing on evidence from 05, 07, 08, 09, 10, and 11.

## 1. Purpose

Determine, on current evidence, whether a specific release is ready for production, and return one outcome — **READY**, **READY WITH CONDITIONS**, or **NOT READY** — with evidence for every condition and blocker. This prompt never deploys.

## 2. When to Use

Use before releasing Tier 2–3 changes to production, before production migrations, or when asked "can we ship this?".

Use something else when:

- Deployment infrastructure has not been planned yet → Workflow 11 (via `continue-project.md` or a direct request) first.
- Security has not been assessed for this scope → `security-review.md` first, or accept that the outcome will be NOT READY.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Release | Version, branch, or commit range | |
| Target environment | Name of the environment | |
| Planned date | If set | Optional. |
| Known issues | Anything already known to be open | Optional. |
| Accepted risks | Risks you have already decided to accept, with reason | Optional; High findings need explicit acceptance. |

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/production-readiness.md
(sections 5–8) acting as the Release and Reliability Engineer
(agents/release-reliability-engineer.md), using
workflows/12-production-readiness.md.

Release: [VERSION / BRANCH / COMMIT RANGE]
Target environment: [ENVIRONMENT]
Planned date: [DATE, OR "NOT SET"]
Known issues: [ISSUES, OR "NONE KNOWN"]
Accepted risks: [RISKS + REASON, OR "NONE"]

Rules:
- You are read-only. Do not deploy, merge to release branches, run
  production migrations, or change production configuration.
- Inspect the repository, reports in docs/reviews/, and docs/project-status.md
  before judging. Determine release scope from version control.
- Evidence must apply to this release scope. Missing or stale evidence is a
  finding, never an assumption of readiness.
- Apply the decision rules in Workflow 12 exactly. When in doubt, choose the
  more conservative outcome and explain why.
- Every blocker and every condition must cite evidence.
- The deployment decision is mine. A READY outcome is not authorization.
```

## 5. Execution Sequence

1. **Define scope** from version control: commits, migrations, configuration changes.
2. **Collect evidence** for each area, specific to this scope:
   - functional requirements (implemented and verified against acceptance criteria);
   - testing (run on the release commit);
   - security (assessment covers scope; Critical/High status);
   - reliability (failure handling, timeouts, retries on new paths);
   - performance (against NFRs, where they exist);
   - observability and monitoring (logs, metrics, health checks, alerts);
   - configuration and secrets (defined for the target; secrets in a secret store);
   - database and migrations (tested on realistic data; ordering; reversibility; locking risk);
   - deployment (procedure defined and rehearsed where possible);
   - rollback (code, configuration, data; irreversible steps);
   - backups (exist; last verified restore);
   - documentation;
   - operational readiness (who deploys, watches, is alerted);
   - unresolved risks and findings.
3. **Walk through** deployment and rollback step by step.
4. **Apply** the Workflow 12 decision rules.
5. **Report** using `templates/release-readiness-report.md`.

## 6. Expected Output

- Report in `docs/reviews/` from `templates/release-readiness-report.md`.
- Outcome: **READY**, **READY WITH CONDITIONS**, or **NOT READY**.
- Evidence per area (report, command output, or file), with stale or missing evidence flagged.
- Blocking findings, each with evidence and the action required to unblock.
- Conditions, each with evidence, owner, and deadline.
- Accepted risks, with the user's acceptance recorded.

## 7. Completion Criteria

- Every area in section 5 has evidence for this scope or a recorded finding for its absence.
- The outcome follows from the Workflow 12 decision rules.
- Every blocker and condition cites evidence.
- Nothing was deployed or changed.

## 8. Stop / Escalation Conditions

Stop and report when:

- The release scope cannot be determined.
- An open Critical finding exists (outcome is NOT READY).
- Open High findings need an explicit user acceptance decision.
- Migrations are irreversible or no rollback path exists.
- Required evidence can only be obtained with production access.
- You are asked to deploy as part of this task: decline, and point out that deployment requires a separate, explicit authorization.
