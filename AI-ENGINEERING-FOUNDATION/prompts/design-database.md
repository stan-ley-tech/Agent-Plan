# Prompt: Design Database

```text
Task: Design (or change) the data model and migrations for the requirement
below.

Requirement: [DOMAIN REQUIREMENT OR FEATURE]
Database engine: [ENGINE AND VERSION, OR "USE WHAT THE PROJECT USES"]
Expected data volume: [ROWS / GROWTH, OR "UNKNOWN"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/database-specialist.md
- AI-ENGINEERING-FOUNDATION/workflows/04-data-and-api-design.md
- AI-ENGINEERING-FOUNDATION/principles/engineering-standards.md
  ("Data integrity", "Backward compatibility")
- docs/project-specification.md and docs/architecture.md, if present

Process:
1. Inspect the existing schema, migrations, and data-access code.
2. List entities and the business rules that constrain them. Ask about rules
   that are unclear.
3. Design the model. Enforce invariants with constraints where the engine allows.
4. Identify access patterns and derive indexes from them.
5. Define transactions and concurrency handling for each write path.
6. Plan migrations: order, reversibility, locking and duration risk on
   realistic volumes, impact on existing rows, and ordering relative to
   application deploys. Use expand/migrate/contract for breaking changes.
7. If sensitive data is involved, consult agents/security-engineer.md.
8. Document trade-offs considered (normalization, data types, soft vs hard delete).
9. Verify migrations forward and backward against a local or disposable
   database if available.

Quality and safety:
- Never run migrations against shared, staging, or production databases.
- Never delete or transform existing data without my explicit approval.
- Do not introduce a new database technology without an ADR and my approval.

Deliverables:
- Data model, constraints, indexes with justifying queries, transaction
  approach, migration plan, trade-offs, risks to existing data, and the
  migration files if implementation was requested.

Verification:
- Every business rule maps to an enforcement mechanism.
- Migration test results are reported as actually observed, or labeled
  Unverified if they could not be run.

Ask me before any destructive or irreversible migration, and whenever a
business rule is ambiguous.
```
