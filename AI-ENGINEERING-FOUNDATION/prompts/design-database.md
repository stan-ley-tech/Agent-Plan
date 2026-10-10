# Prompt: Design Database

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 04 Data and API Design (data stages D1–D7), consulting 05 for sensitive data.

## 1. Purpose

Design a new data model or a change to an existing one, including constraints, indexes, transactions, and a safe migration plan, with trade-offs made explicit.

## 2. When to Use

Use when adding or changing entities, relationships, constraints, indexes, or migrations, or when diagnosing data integrity or concurrency defects at the design level.

Use something else when:

- You need the API contract designed as well → also `design-api.md`.
- The problem is a slow query with an otherwise sound schema → `performance-review.md`.
- The design is approved and you want it built → `implement-feature.md`.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Requirement | The domain need or feature driving the change | Or a spec reference. |
| Business rules | Rules the data must always satisfy, if known | The AI will ask about gaps. |
| Expected volume | Rows, growth, read/write ratio | "Unknown" is acceptable. |
| Engine constraint | Only if a specific database is mandated | Otherwise the project's existing engine is used. |
| Existing data concerns | Anything known about production data quality or size | Optional. |

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/design-database.md
(sections 5–8) acting as the Database Specialist
(agents/database-specialist.md), using workflows/04-data-and-api-design.md.

Requirement: [REQUIREMENT]
Business rules: [RULES, OR "DERIVE FROM SPEC AND ASK"]
Expected volume: [VOLUME, OR "UNKNOWN"]
Engine constraint: [ENGINE, OR "USE THE PROJECT'S EXISTING ENGINE"]
Existing data concerns: [CONCERNS, OR "NONE KNOWN"]

Rules:
- Inspect the existing schema, migrations, and data-access code first, and
  cite them for every statement about the current model.
- Enforce business rules with database constraints where the engine allows.
- Explain every important trade-off (normalization, types, delete strategy,
  indexes, consistency model).
- Run migrations only against local or disposable databases; never shared,
  staging, or production.
- Never delete or irreversibly transform existing data without my approval.
- Consult agents/security-engineer.md when sensitive data is involved.
- Label performance claims Unverified unless measured.
```

## 5. Execution Sequence

1. **Inspect** existing schema, migrations, ORM or query code, and the specification.
2. **Requirements**: list the business rules and access patterns the design must serve; ask about unclear rules.
3. **Entities and ownership**: which component owns each entity.
4. **Relationships**: cardinality, optionality, delete behavior.
5. **Lifecycle**: states, transitions, retention, soft vs hard delete.
6. **Constraints**: map each business rule to an enforcement mechanism.
7. **Normalization/denormalization**: default normalized; justify any denormalization and its consistency mechanism.
8. **Indexes**: derived from access patterns; each with the query it serves.
9. **Transactions and concurrency**: per write path, atomicity, isolation, and conflict handling.
10. **Migrations**: order, reversibility, locking and duration risk on realistic volume, existing-row impact, deploy ordering; expand → migrate → contract for breaking changes.
11. **Performance, security, backup/recovery implications**: query cost at expected volume; sensitive columns, access, encryption needs; what a restore or rollback means for this change.
12. **Verify** migrations forward and backward locally if possible.
13. **Report** and stop for approval of breaking or destructive changes.

## 6. Expected Output

- Data model (table or diagram) with types and ownership.
- Business rule → constraint mapping.
- Index list with justifying queries.
- Transaction and concurrency approach per write path.
- Migration plan: step, change, reversible?, locking/duration risk, deploy ordering, existing-data impact.
- Trade-offs with reasons.
- Performance, security, and backup/recovery implications.
- Migration test results (actual), or "not run" with the reason.
- Open questions.

## 7. Completion Criteria

- Every business rule has an enforcement mechanism.
- Every index has a query that needs it.
- Every write path has a defined concurrency approach.
- Every migration states reversibility, data impact, and deploy ordering.
- Trade-offs are explained.
- Breaking or destructive changes are approved by the user.

## 8. Stop / Escalation Conditions

Stop and ask when:

- A business rule is ambiguous.
- Data ownership between components is unclear.
- A migration would delete, truncate, or irreversibly transform data, or may lock large tables for long.
- A change breaks running application versions or other consumers.
- Sensitive data is added or moved without a clear protection requirement.
- Verifying the design would require access to shared or production databases.
