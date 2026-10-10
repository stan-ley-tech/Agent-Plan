# Workflow 11 — DevOps and Deployment Planning

> **Lifecycle:** 10 Documentation → **11 DevOps and Deployment Planning** → 12 Production Readiness. For new projects, start early (after 03) so environments and CI exist before features accumulate. Iterative; see "Workflow lifecycle" in `README.md`.

## 1. Purpose

Prepare the system to be built, configured, deployed, observed, and recovered reliably, with infrastructure proportional to its actual needs.

It exists because deployment failures usually come from undocumented manual steps, configuration drift, missing rollback paths, and infrastructure assumed rather than known.

## 2. When to Use

Use when:

- A new project needs environments and CI before or alongside the first milestone.
- Preparing a first production deployment, or changing the deployment target or strategy.
- Adding environments, services, data stores, or infrastructure dependencies.
- Builds or deployments are unreliable.

Do not use when:

- Application changes have no build, configuration, infrastructure, or deployment impact.

## 3. Required Inputs

- Architecture document (components, data stores, external services).
- Existing build scripts, CI files, container files, infrastructure code, environment examples.
- **Target environment details provided by the user** (hosting, accounts, regions, domains). Never invented.
- Operational requirements: availability, recovery objectives, environments needed, who operates the system.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| DevOps Engineer | Leads; environments, configuration, CI/CD, deployment, observability. |
| Security Engineer | Secrets delivery, access, CI token scope, network exposure. |
| Database Specialist | Migration execution within deployments; backup approach. |
| Release and Reliability Engineer | Rollback design, health checks, recovery procedures. |
| Engineering Orchestrator | Tracks approvals for anything affecting production or cost. |

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Inventory and evidence | Record what exists and what evidence there is of the target infrastructure. Unknowns are listed, not assumed. | — |
| 2. Environments | Which environments exist or are needed (local, CI, staging, production) and how they differ. | 1 |
| 3. Configuration | Inventory every setting: purpose, required or optional, default, source per environment. Validate at startup. | 1 |
| 4. Secrets | Each secret's source per environment (platform secret store, CI secret store); rotation approach; nothing in the repository. | 3 |
| 5. Build process | Deterministic, scripted build; locked dependencies; reproducible from a clean checkout. Verify locally. | 1 |
| 6. CI/CD | Checks on every change matching local checks; deployment stages and gates (tests, review, manual approval for production). | 5 |
| 7. Migrations in deployment | When migrations run relative to code, who runs them, how failure is handled. | 6 |
| 8. Deployment strategy | Choose proportionately (in-place, rolling, blue-green, canary) based on availability needs and platform support. | 2, 6 |
| 9. Rollback | How to revert code and configuration; how data changes are handled; which steps are irreversible. | 7–8 |
| 10. Observability | Structured logging, key metrics, health checks (liveness vs readiness), alerts with named recipients — proportional to importance. | 2 |
| 11. Backups and disaster recovery | Where appropriate: what is backed up, frequency, retention, restore procedure, and recovery objectives taken from requirements. | 2 |
| 12. Infrastructure dependencies | External services, managed platforms, DNS, certificates; ownership and failure impact. | 1 |
| 13. Operational risks | Single points of failure, manual steps, drift, cost risks, access risks. | all |
| 14. Plan and approval | Present proposed changes, marking each that requires approval. | all |

## 6. Investigation Requirements

- Inventory actual files before proposing anything; cite them.
- Run the build and tests from a clean state locally where possible; record friction and results.
- Compare configuration across environments for drift where evidence exists.
- **Do not assume production infrastructure.** If the target is not evidenced in the repository or stated by the user, record it as unknown and ask.
- Validate changed configuration files syntactically with available tooling; otherwise label them Unverified.

## 7. Decision Rules

- Proportionality: the simplest deployment model that meets availability and recovery requirements. A small internal tool does not need container orchestration or multi-region failover.
- Prefer the hosting platform's managed capabilities over self-operated infrastructure unless there is a recorded reason.
- Everything needed to build and deploy is scripted and versioned, except secrets.
- CI runs the same checks developers run.
- Fail fast on missing configuration.
- Every deployment has a rollback path or a recorded forward-fix plan for irreversible steps.
- Infrastructure choices with long-term consequences get an ADR.

## 8. Expected Deliverables

- Environment and infrastructure inventory (with unknowns).
- Configuration and secrets inventory.
- Build and CI/CD plan (or changes to existing pipelines).
- Deployment strategy, migration ordering, and rollback plan.
- Observability plan: logs, metrics, health checks, alerts.
- Backup and recovery plan where appropriate.
- Operational risk list.
- Proposed changes with approval requirements; documented procedures (via Workflow 10).

## 9. Verification / Completion Criteria

- Local build and tests run from documented steps, with actual results recorded.
- No secret is stored in the repository or printed in CI output.
- Every required setting has a defined source for each target environment, or is listed as an open question.
- Rollback is defined for every deployment step, or irreversible steps are identified with a forward-fix plan.
- Health checks and alerts cover critical paths.
- The user approves the deployment plan. **Approval checkpoint for anything affecting production, cost, or access.**

## 10. Escalation Conditions

- Any action that would change production, create cloud resources, incur cost, or grant access.
- Secrets found in the repository, history, or logs.
- Target environment unknown or contradictory.
- Recovery objectives required but undefined.
- Significant drift between environments.

## 11. Failure / Stop Conditions

- Stop before creating cloud resources, changing production configuration, rotating production secrets, or deploying. Each requires explicit user authorization for that specific action.
- Do not invent providers, accounts, regions, domains, or credentials; use placeholders and ask.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/11-devops-and-deployment-planning.md
acting as the DevOps Engineer (agents/devops-engineer.md).
Target environment: [DETAILS FROM ME, OR "UNKNOWN"]

1. Inventory existing build, CI, container, infrastructure, and config files;
   list unknowns about the target instead of assuming them.
2. Define environments, configuration inventory, and secret sources.
3. Verify the build and tests locally from a clean state; report results.
4. Plan CI/CD gates, migration ordering, deployment strategy, and rollback.
5. Plan logging, metrics, health checks, alerts, and backups/recovery where
   appropriate, proportional to the project.
6. List infrastructure dependencies and operational risks.
7. Mark every change needing approval. Do not create resources, change
   production, incur cost, or deploy.
```
