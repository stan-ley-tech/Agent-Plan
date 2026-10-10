# Prompt: Design API

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 04 Data and API Design (interface stages I1–I9), consulting 05 for authorization and sensitive operations.

## 1. Purpose

Design a new interface, or a change to an existing one, with complete contracts, validation, authorization, errors, and integration behavior. For existing APIs, include a backward-compatibility analysis.

## 2. When to Use

Use for HTTP, RPC, GraphQL, event, CLI, or library interfaces, and for integrations with external services or webhooks.

Use something else when:

- The data model needs designing as well → also `design-database.md`.
- The design is approved and you want it built → `implement-feature.md`.
- You want an existing API assessed for vulnerabilities → `security-review.md`.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Purpose | What the interface must let callers do | Or a spec reference. |
| Consumers | Who calls it: browser app, mobile app, partners, internal services, scripts | Affects compatibility and auth. |
| Access rules | Who may perform which operations, if known | The AI will ask about gaps. |
| External services | Third-party APIs or webhooks involved | Name and documentation link. |
| Style constraint | Only if a style is mandated | Otherwise the project's existing style is followed. |

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/design-api.md
(sections 5–8) acting as the API and Integration Specialist
(agents/api-integration-specialist.md), using workflows/04-data-and-api-design.md.

Purpose: [WHAT THE API MUST DO]
Consumers: [CONSUMERS]
Access rules: [RULES, OR "DERIVE AND ASK"]
External services: [SERVICES + DOCS, OR "NONE"]
Style constraint: [STYLE, OR "FOLLOW THE PROJECT"]

Rules:
- Inspect existing APIs and follow their conventions (naming, errors,
  authentication, pagination, versioning). Cite the files that establish
  each convention and each known consumer.
- Derive operations from user workflows; do not add operations no
  requirement needs.
- For any change to an existing API, analyze backward compatibility for
  every known consumer.
- Assume external services can be slow, unavailable, duplicating, or wrong.
  Cite their documentation; label undocumented behavior Unverified.
- Do not call real third-party APIs with real credentials.
- Consult agents/security-engineer.md for operations that change
  permissions, move money, or expose personal data.
```

## 5. Execution Sequence

1. **Inspect** existing interfaces, conventions, data model, and specification.
2. **Resources and operations** (endpoints, methods, or equivalents) from user workflows.
3. **Request/response contracts** with types, required fields, and concrete examples.
4. **Validation** rules per input.
5. **Authentication and authorization**: identity required and resource-level access per operation.
6. **Errors**: one shape, stable codes, protocol status mapping, no leaked internals.
7. **Pagination and filtering** for every collection: page model, limits, sort, allowed filters.
8. **Idempotency** for operations that may be retried.
9. **Versioning and compatibility**: consumer impact analysis for existing APIs; additive change, deprecation path, or approved breaking change.
10. **Rate limiting** where abuse or cost is plausible.
11. **Observability**: what is logged and measured per operation, without sensitive data.
12. **Security review** of the design: abuse cases, mass assignment, enumeration, data exposure.
13. **External integrations**: timeouts, retries, failure behavior, rate limits, webhook verification and deduplication.
14. **Report** and stop for approval of breaking changes.

## 6. Expected Output

- Operation table: operation, method/path or name, auth required, idempotent, purpose.
- Contracts per operation with success and error examples (placeholder data).
- Validation rules and authorization per operation.
- Error contract.
- Pagination, filtering, and sorting rules.
- Compatibility analysis per consumer (for existing APIs) and versioning plan.
- Rate limiting, observability, and security considerations.
- Integration behavior table: service, timeout, retry policy, failure behavior, rate limit, assumptions.
- Open questions.

## 7. Completion Criteria

- Every operation has contract, validation, authorization, and errors defined.
- Every collection has pagination limits.
- Every retried operation is idempotent.
- Every external call has a timeout and failure behavior.
- Every change to an existing API has a compatibility analysis; breaking changes are approved.
- Examples exist for success and main error cases.

## 8. Stop / Escalation Conditions

Stop and ask when:

- It is unclear who may perform an operation.
- A change would break existing consumers.
- An operation moves money, changes permissions, or exposes personal data and controls are undefined.
- External service behavior on a critical path is undocumented.
- The data model cannot support the contract without changes → `design-database.md`.
