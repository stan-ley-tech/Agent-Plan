# Prompt: Design API

```text
Task: Design (or change) the API or integration described below.

API purpose: [WHAT THE API OR INTEGRATION MUST DO]
Style: [REST / GRAPHQL / RPC / EVENTS / LIBRARY / CLI, OR "FOLLOW THE PROJECT"]
Consumers: [WHO CALLS IT: BROWSER APP, MOBILE APP, PARTNERS, INTERNAL SERVICES]
External services involved: [SERVICES, OR "NONE"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/api-integration-specialist.md
- AI-ENGINEERING-FOUNDATION/workflows/04-data-and-api-design.md
- AI-ENGINEERING-FOUNDATION/principles/security-principles.md
  ("Authentication and authorization", "Input validation")
- docs/project-specification.md and docs/architecture.md, if present

Process:
1. Inspect existing APIs and identify conventions: naming, error format,
   authentication, pagination, versioning. Follow them.
2. Derive the operations from the user workflows. Do not add operations
   no requirement needs.
3. For each operation define: input, output, validation rules, errors,
   authorization requirement (who may call it, on which resources),
   idempotency.
4. Define the error contract and collection conventions (pagination,
   filtering, sorting) where collections exist.
5. Define compatibility: who is affected by changes, and the versioning
   or deprecation approach.
6. For each external service: timeout, retry policy, idempotency, failure
   behavior visible to users, rate limits. Do not assume reliability.
7. For webhooks: signature verification, replay protection, deduplication,
   ordering.
8. Write concrete request/response examples for success and main error
   cases, using placeholder data.
9. Consult agents/security-engineer.md for operations that change
   permissions, move money, or expose personal data.

Quality and safety:
- Do not call real third-party APIs with real credentials.
- Do not invent external service behavior; cite documentation or label
  assumptions as Unverified.
- Breaking changes to existing consumers require my approval.

Deliverables:
- Operation list, contracts with examples, error contract, collection rules,
  compatibility plan, integration behavior, open questions.

Verification:
- Every operation has authorization and errors defined.
- Every external call has a timeout and failure behavior.
- If implemented, contract tests run and results are reported.

Ask me when it is unclear who may perform an operation, or when a change
would break existing consumers.
```
