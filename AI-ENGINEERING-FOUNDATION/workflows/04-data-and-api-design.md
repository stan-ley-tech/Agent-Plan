# Workflow 04 — Data and API Design

> **Lifecycle:** 03 Architecture and Planning → **04 Data and API Design** → 05 Security Assessment. Iterative; see "Workflow lifecycle" in `README.md`.

## 1. Purpose

Design the data model and interface contracts before implementation fixes them in code.

It exists because schemas and public contracts are the hardest parts of a system to change later: they outlive the code, carry existing data, and have consumers. Designing them as an afterthought produces integrity bugs, unsafe migrations, and breaking changes.

## 2. When to Use

Use when:

- A new project has an approved architecture and stores data or exposes interfaces.
- Any change adds or alters a schema, migration, API operation, event, file format, or external integration.
- Defects involve data integrity, concurrency, contract mismatches, duplicates, or retries.

Do not use when:

- The work touches neither persistent data nor any interface.
- A Tier 0–1 change uses existing contracts and schema unchanged.

Run only the half that applies: data (stages D1–D7), interfaces (stages I1–I9), or both.

## 3. Required Inputs

- Approved specification (entities, business rules, workflows).
- Approved architecture (data ownership by component, integration boundaries).
- Existing schema, migrations, data-access code, and API definitions.
- Documentation for external services involved.
- Expected data volumes, if known.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Database Specialist | Leads data stages: model, constraints, indexes, transactions, migrations. |
| API and Integration Specialist | Leads interface stages: contracts, validation, errors, versioning, integration behavior. |
| Security Engineer | Assesses authorization per operation and handling of sensitive fields. |
| Performance Engineer | Only for large volumes or demanding query NFRs. |
| Release and Reliability Engineer | Consulted on migration rollout for existing production data. |

## 5. Workflow Sequence

### Data

| Stage | What happens | Depends on |
| --- | --- | --- |
| D1. Entities and ownership | Entities from the domain; which component owns each. One owner per entity. | Architecture |
| D2. Relationships | Cardinality, optionality, and what happens to children when parents are deleted. | D1 |
| D3. Lifecycle | States and allowed transitions, retention, archival, deletion (soft or hard, and why). | D1 |
| D4. Constraints | Express business rules as not-null, unique, foreign key, check, and type constraints wherever the engine allows. | D1–D3 |
| D5. Transactions and consistency | For each write path: atomicity boundary, isolation, concurrency handling (constraint, lock, version check, idempotency key). Where data spans stores or services, state the consistency model and how it is restored after failure. | D4 |
| D6. Access patterns and indexes | Main reads and writes; an index only where a query needs it. | D1–D4 |
| D7. Migrations | Order, reversibility, locking and duration on realistic volumes, effect on existing rows, ordering relative to code deploys. Use expand → migrate → contract for breaking changes. | D4–D6 |

### Interfaces

| Stage | What happens | Depends on |
| --- | --- | --- |
| I1. Resources and operations | Operations derived from user workflows; follow existing project conventions. | D1 |
| I2. Request/response contracts | Inputs, outputs, types, required fields; concrete examples. | I1 |
| I3. Validation | Rules at the boundary for each input. | I2 |
| I4. Authentication and authorization boundaries | Who may call each operation and on which resources. | I1 |
| I5. Errors | One error shape, stable codes, mapping to protocol status; no internals leaked. | I2 |
| I6. Pagination and filtering | For every collection: page model, limits, sort, allowed filters. | I2 |
| I7. Versioning and compatibility | Consumers affected; additive changes preferred; deprecation path for breaking ones. | I2 |
| I8. Idempotency | Which operations are retried by clients or infrastructure; keys or natural idempotency. | I1, D5 |
| I9. External integrations | Timeouts, retry policy, failure behavior seen by users, rate limits, webhook verification and deduplication. | I1 |

### Cross-check

- X1. Every API operation maps onto the data model without hidden joins or ownership violations; every write operation maps to a transaction defined in D5.
- X2. Review and approval of breaking changes and destructive migrations.

## 6. Investigation Requirements

- Read the existing schema and migrations from the repository, not from documentation alone.
- Read existing API code to identify conventions (naming, errors, authentication, pagination) and follow them.
- Identify all consumers of any contract being changed (other services, clients, scripts, reports).
- Check external service documentation for limits and failure behavior; label undocumented behavior Unverified.
- Run migrations only against local or disposable databases; report actual results.

## 7. Decision Rules

- The database is the last line of defense for integrity: enforce invariants there when possible, and validate earlier for clear errors.
- Normalize by default; denormalize only for a known read need, with the consistency mechanism stated.
- Every external call has a timeout. Retry only operations that are idempotent or made idempotent.
- Assume external services can be slow, unavailable, duplicating, or wrong.
- Prefer additive change. Breaking changes and destructive migrations need a migration path and user approval.
- Follow the protocol's and the project's conventions unless a recorded reason says otherwise.

## 8. Expected Deliverables

- Data design: entities, relationships, lifecycle, constraints mapped to business rules, transactions and concurrency approach, indexes with justifying queries, migration plan.
- Interface design: operation list, contracts with examples, validation, authorization per operation, error contract, collection rules, versioning plan, idempotency, integration behavior.
- Compatibility and migration risk list.
- Recorded in `docs/architecture.md` or a design document linked from it; ADRs for consequential choices.

## 9. Verification / Completion Criteria

- Every business rule has an enforcement mechanism.
- Every write path has a defined transaction and concurrency approach.
- Every operation has authorization, validation, and errors defined.
- Every external call has a timeout and a failure behavior.
- Every migration states reversibility, data impact, and deploy ordering; migrations tested locally where possible.
- Breaking changes and destructive migrations are approved by the user. **Approval checkpoint for those changes.**

## 10. Escalation Conditions

- Breaking change for existing consumers.
- Migration that deletes or irreversibly transforms data, or may lock large tables.
- Sensitive data added, moved, or exposed through a new interface (Security Engineer).
- Unclear data ownership between components (return to Workflow 03).
- Critical-path dependency with undocumented failure behavior.

## 11. Failure / Stop Conditions

- Stop if data ownership is ambiguous.
- Do not implement a destructive or irreversible migration without approval.
- Do not run migrations against shared, staging, or production databases.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/04-data-and-api-design.md.
Scope: [DATA / INTERFACES / BOTH] for [FEATURE OR PROJECT]
Roles: agents/database-specialist.md and agents/api-integration-specialist.md.

1. Inspect existing schema, migrations, data-access code, and API conventions.
2. Data: entities and ownership, relationships, lifecycle, constraints mapped to
   business rules, transactions and concurrency, indexes from access patterns,
   migration plan with reversibility, data impact, and deploy ordering.
3. Interfaces: operations, contracts with examples, validation, authorization
   per operation, error contract, pagination and filtering, versioning,
   idempotency, and external integration behavior (timeouts, retries, failures).
4. Cross-check operations against the data model and transactions.
5. Test migrations only on local or disposable databases; report actual results.
6. Stop for approval of any breaking change or destructive migration.
```
