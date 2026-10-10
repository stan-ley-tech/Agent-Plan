# Prompt: Security Review

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 05 Security Assessment (code-level, or design-level for designs). Remediation is a separate task under Workflow 09.

## 1. Purpose

Perform an independent, risk-based security assessment of actual code and configuration (or of a design), producing evidence-backed, prioritized findings that can be fixed and verified.

## 2. When to Use

Use before production readiness for Tier 2–3 releases, after significant changes to authentication, authorization, sensitive data, secrets, or infrastructure, or when assessing an inherited codebase.

Use something else when:

- You want a general review of a specific change → `code-review.md` (it includes a first security pass).
- You want findings fixed → run this first, then fix them as a separate, authorized task following `workflows/09-remediation-and-reverification.md`.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Scope | Whole repository, a feature, or a branch/diff | |
| Deployment context | Public internet, internal network, local only, unknown | Determines depth and severity. |
| Sensitive data | Types handled, if known | |
| Regulatory context | Any applicable regulation or contract | Optional. |
| Known concerns | Specific worries or past incidents | Optional. |

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/security-review.md
(sections 5–8) acting as the Security Engineer
(agents/security-engineer.md), using workflows/05-security-assessment.md and
principles/security-principles.md.

Scope: [SCOPE]
Deployment context: [PUBLIC / INTERNAL / LOCAL / UNKNOWN]
Sensitive data: [TYPES, OR "UNKNOWN"]
Regulatory context: [CONTEXT, OR "NONE KNOWN"]
Known concerns: [CONCERNS, OR "NONE"]

Rules:
- You are read-only. Do not modify code or configuration.
- Base every finding on evidence from the actual code, configuration, or
  tool output. Do not invent vulnerabilities; a plausible risk without
  evidence is reported as an Unverified concern, not a finding.
- Prioritize by realistic exploitability in this deployment context.
- Run available audit tools and report their actual output; list tools not run.
- Never print secret values; report locations only.
- Do not attack systems or test against production.
- Never state that the application is secure.
- Report Critical findings to me immediately.
```

## 5. Execution Sequence

1. **Scope and depth**: state what will be assessed and how deeply.
2. **Inspect** entry points from the code: routes, handlers, consumers, jobs, CLI and file inputs.
3. **Threat model**: assets, actors, trust boundaries, threats per entry point, abuse cases by legitimate users.
4. **Authentication** review.
5. **Authorization** review: server-side, resource-level, tenant-level, admin functions, default deny.
6. **Input validation and injection**: query, command, template, path, deserialization, SSRF, cross-site scripting.
7. **Secrets handling**: code, configuration, history, CI, logs.
8. **Sensitive data**: exposure in responses, logs, errors; encryption; retention.
9. **Dependency risks**: audit tool results and reachability.
10. **API security**: rate limiting, enumeration, mass assignment, unbounded queries, business-logic abuse.
11. **Configuration and infrastructure/deployment**: debug modes, CORS, headers, cookies, default credentials, exposed services, CI token scope.
12. **Logging and auditing** of security events.
13. **Cross-check** against common vulnerability classes (for example the OWASP Top 10 and API Security Top 10).
14. **Prioritize and report** using `templates/security-assessment.md`.

## 6. Expected Output

A report in `docs/reviews/` from `templates/security-assessment.md`. Every finding includes:

| Field | Meaning |
| --- | --- |
| Severity | Critical / High / Medium / Low / Info (`principles/engineering-standards.md`) |
| Evidence | Evidence label plus file:line, reproduction steps, or tool output (never secret values) |
| Impact | Consequence if exploited, with the attack scenario |
| Affected area | Component, endpoint, and file location |
| Recommended remediation | Specific fix |
| Verification method | How the fix will be proven (the template's "verification requirement") |

Also: summary by severity, scope assessed and not assessed, tools run and not run, unverified concerns listed separately, residual risks.

## 7. Completion Criteria

- Every applicable area in section 5 is covered or marked N/A with a reason.
- Every finding has all six fields with real evidence.
- Unverified concerns are separated from findings.
- Scope not assessed and tools not run are listed.
- Critical and High findings have been reported to the user.

## 8. Stop / Escalation Conditions

Stop and report immediately when:

- A Critical finding is confirmed.
- Secrets or credentials are found (location only; recommend rotation).
- There is evidence of active compromise or malicious code.
- Assessment would require access, testing, or systems the user has not authorized.
- A finding requires an architectural change (flag for Workflow 03).
- Deployment context is unknown and materially changes severity → ask.
