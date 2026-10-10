# Workflow 12 — Production Readiness

> **Lifecycle:** 11 DevOps and Deployment Planning → **12 Production Readiness** → release decision by the user. A NOT READY outcome returns work to the workflow that owns each blocker. Iterative; see "Workflow lifecycle" in `README.md`.

## 1. Purpose

Make a final, evidence-based assessment of whether a release can go to production, and state the outcome plainly.

It exists so that release decisions rest on current evidence for this exact release scope, not on momentum, optimism, or another agent's report, and so that blockers are named before users find them.

## 2. When to Use

Use when:

- Releasing Tier 2 or Tier 3 changes to production.
- Running migrations against production data.
- The user asks whether something is ready to ship.

Do not use when:

- Tier 0–1 changes released through an established, automated routine with passing checks (the routine is the gate).

## 3. Required Inputs

- Release scope: version, branch, or commit range.
- Specification and acceptance criteria for the scope.
- Test reports, code review reports, security assessments covering the scope.
- Migration plan, deployment plan, configuration inventory, rollback and recovery procedures (Workflow 11).
- Open findings and known issues.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Release and Reliability Engineer | Leads; **read-only**; makes the recommendation. |
| Test Engineer | Confirms test evidence for the scope. |
| Security Engineer | Confirms security status for the scope. |
| Database Specialist | Confirms migration readiness. |
| DevOps Engineer | Confirms configuration, deployment, observability, rollback mechanics. |
| Performance Engineer | Confirms performance evidence where NFRs exist. |
| Documentation Engineer | Confirms documentation is current. |
| Engineering Orchestrator | Collects evidence, tracks blockers, presents the outcome. |

## 5. Workflow Sequence

Each area must have evidence specific to this release scope. Stages 2–14 can be gathered in parallel; stage 15 depends on all of them.

| Stage | Area | Evidence required |
| --- | --- | --- |
| 1 | Release scope | Exact commits, migrations, and configuration changes from version control. |
| 2 | Functional completeness | Every in-scope requirement implemented; nothing half-built is reachable by users (or it is disabled and documented). |
| 3 | Requirements | Every acceptance criterion in scope verified (Workflow 07 report). |
| 4 | Testing | Relevant suites run on the release commit; failures resolved or classified. |
| 5 | Security | Assessment covers the scope; Critical findings resolved; High findings resolved or explicitly accepted. |
| 6 | Performance | Evidence against NFRs where they exist; otherwise "no NFR" recorded. |
| 7 | Reliability | Failure modes for new paths handled; timeouts and retries in place for new integrations. |
| 8 | Observability | Logs, metrics, health checks, and alerts cover new critical paths. |
| 9 | Deployment | Procedure defined and rehearsed in a non-production environment where one exists. |
| 10 | Rollback | Procedure for code, configuration, and data; irreversible steps identified with forward-fix plan. |
| 11 | Database readiness | Migrations tested on realistic data; deploy ordering; locking and duration risk; backup immediately before irreversible steps. |
| 12 | Documentation | Updated for user-visible, API, configuration, and operational changes. |
| 13 | Operational readiness | Who deploys, who watches, who is alerted, how to reach them; recovery procedure and last verified restore. |
| 14 | Known risks and unresolved findings | Every open finding with severity, owner, and state. |
| 15 | Release decision | Outcome, blockers, and conditions. |

## 6. Investigation Requirements

- Determine scope from version control, not from a description.
- Check that each piece of evidence applies to this release scope; evidence from an earlier commit is flagged as stale.
- Run tests on the release commit where possible.
- **Missing evidence is a finding**, never an assumption of readiness.
- Walk through deployment and rollback step by step and identify where each could fail.

## 7. Decision Rules

| Outcome | When |
| --- | --- |
| **READY** | Every area has current evidence; no open Critical or High findings; no blocking gaps. |
| **READY WITH CONDITIONS** | No open Critical findings. Every open High finding is explicitly accepted by the user. Each remaining gap is covered by a specific condition with evidence, an owner, and a deadline (before deployment, or a stated time after). |
| **NOT READY** | Any open Critical finding; any unaccepted High finding; missing evidence in a required area; an irreversible step without approval or forward-fix plan; or no rollback path. |

- Every blocker and every condition cites its evidence: report, file, command output, or the specific missing artifact.
- When in doubt between two outcomes, choose the more conservative one and explain why.
- Recommending NOT READY is a valid and expected outcome.
- The outcome is a recommendation. **The user decides whether and when to deploy.**

## 8. Expected Deliverables

- Release readiness report in `docs/reviews/` from `templates/release-readiness-report.md`, ending with:
  - Outcome: READY, READY WITH CONDITIONS, or NOT READY.
  - Blocking findings, each with evidence and the action required to unblock.
  - Conditions, each with evidence, owner, and deadline.
  - Accepted risks with the user's acceptance recorded.

## 9. Verification / Completion Criteria

- Every area in stages 2–14 has evidence for this scope, or a recorded finding for its absence.
- The outcome follows from the decision rules.
- Every blocker and condition has supporting evidence.
- `checklists/production-readiness.md` applied.
- The report is delivered to the user. The workflow is complete at the recommendation, not at deployment.

## 10. Escalation Conditions

- Any open Critical finding.
- Open High findings needing a user decision.
- Irreversible migrations or missing rollback path.
- Stale or missing evidence that cannot be produced without production access.
- Pressure to release despite blockers: present the risks plainly to the user.

## 11. Failure / Stop Conditions

- Stop at the recommendation. Do not deploy, merge to a release branch, run production migrations, or change production configuration as part of this workflow.
- A passing assessment is not authorization to deploy; deployment requires explicit user authorization for that specific release.
- Stop if the release scope cannot be determined.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/12-production-readiness.md acting as
the Release and Reliability Engineer (agents/release-reliability-engineer.md).
Remain read-only. Release: [VERSION / BRANCH / COMMIT RANGE]

1. Determine scope from version control.
2. Collect evidence for this scope: functional completeness, requirements,
   tests (run on the release commit), security, performance, reliability,
   observability, deployment, rollback, database readiness, documentation,
   operational readiness, known risks, and unresolved findings.
3. Treat missing or stale evidence as a finding.
4. Walk through deployment and rollback step by step.
5. Apply the decision rules and state READY, READY WITH CONDITIONS, or
   NOT READY. Cite evidence for every blocker and condition.
6. Write the report from templates/release-readiness-report.md.
Do not deploy or change anything. The deployment decision is mine.
```
