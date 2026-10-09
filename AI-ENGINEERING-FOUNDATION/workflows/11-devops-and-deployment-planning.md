# Workflow 11 — DevOps and Deployment Planning

## Purpose

Ensure the project can be built, tested, configured, deployed, and observed reliably, with infrastructure proportional to its needs.

## When to invoke

- New projects, once the architecture is approved and before the first deployment.
- When adding environments, changing deployment targets, or introducing CI/CD.
- When builds or deployments are unreliable.

## Required inputs

- Architecture document.
- Existing build, CI, container, and infrastructure files.
- Target environment details from the user. Never invented.
- Operational requirements: availability, environments, who operates the system.

## Relevant agents

- **DevOps Engineer** — leads.
- **Security Engineer** — consulted on secrets, access, and pipeline permissions.
- **Release and Reliability Engineer** — consulted on rollback and health checks.

## Steps

1. Inventory current build, CI, environment, and deployment setup.
2. Verify the local build and tests run from documented steps.
3. Build a configuration inventory: every setting and secret, its purpose, and its source per environment.
4. Define the CI pipeline: checks that run on every change, matching local checks.
5. Define the deployment path and its gates (tests, review, approval).
6. Define health checks, logging, key metrics, and alerts proportional to importance.
7. Define the rollback mechanism for code and configuration.
8. Identify drift between environments.
9. Propose changes, marking which require approval (anything touching production, cost, or access).
10. Document the procedure (Workflow 10).

## Deliverables

- Configuration inventory.
- CI/CD and deployment plan.
- Monitoring and rollback plan.
- Proposed changes with approval requirements.

## Verification criteria

- Local build and test steps were executed, with actual results.
- No secret is stored in the repository.
- Configuration files that were changed are syntactically validated where tooling allows; otherwise labeled Unverified.

## Completion criteria

- The user approves the deployment plan. **Approval checkpoint for any production-affecting change.**

## Escalation conditions

- Any production change, cost, or access grant.
- Secrets discovered in the repository or logs.
- Unknown target environment.

## Stop conditions

- Stop before creating cloud resources, changing production configuration, or deploying. These require explicit user authorization for the specific action.
