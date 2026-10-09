# Workflow 04 — Data and API Design

## Purpose

Define how data is owned, stored, constrained, and changed, and how the system's interfaces behave, before implementation locks them in.

## When to invoke

- New projects, after architecture approval.
- Any schema change, new API, changed API contract, or new external integration.

Skip if the work touches neither persistent data nor interfaces.

## Required inputs

- Approved specification and architecture.
- Existing schema, migrations, and API code.
- Documentation for external services involved.

## Relevant agents

- **Database Specialist** — data model, constraints, transactions, migrations.
- **API and Integration Specialist** — contracts, errors, integrations.
- **Security Engineer** — consulted on authorization per operation and on sensitive data.

## Steps

1. Identify data ownership: which component owns which data.
2. Design or update the data model from business rules; express invariants as constraints.
3. Define transaction boundaries and concurrency handling for each write path.
4. Derive indexes from access patterns.
5. Plan migrations: order, reversibility, locking risk, data impact, and coordination with application deploys.
6. Define API operations from user workflows: inputs, outputs, errors, authorization, idempotency.
7. Define the error contract and pagination conventions, following existing project conventions.
8. Define integration behavior for each external service: timeouts, retries, failure handling, rate limits, webhooks.
9. Identify compatibility risks for existing consumers and existing data.
10. Add the results to `docs/architecture.md` or a dedicated design document linked from it.

## Deliverables

- Data model with constraints, indexes, and migration plan.
- API contracts with examples.
- Integration behavior definitions.
- List of compatibility and migration risks.

## Verification criteria

- Every business invariant has an enforcement mechanism.
- Every operation has defined authorization and errors.
- Every external call has a timeout and failure behavior.
- Every migration states its reversibility and its impact on existing data.

## Completion criteria

- Designs are reviewed against the specification. For Tier 2+, the user approves breaking changes and destructive migrations. **Approval checkpoint for breaking or destructive changes.**

## Escalation conditions

- Breaking changes for existing consumers.
- Destructive or long-running migrations.
- Sensitive data added or moved.
- External dependencies with undocumented failure behavior on a critical path.

## Stop conditions

- Stop if data ownership is unclear between components.
- Stop before implementing a destructive migration without approval.
