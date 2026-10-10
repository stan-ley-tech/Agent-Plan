# Workflow 05 — Security Assessment

> **Lifecycle:** 04 Data and API Design → **05 Security Assessment** → 06 Implementation. Runs again at code level before 12 Production Readiness. Iterative; see "Workflow lifecycle" in `README.md`.
> Principles: `principles/security-principles.md`. Severity and evidence labels: `principles/engineering-standards.md`.

## 1. Purpose

Identify the realistic ways the system can be attacked or misused, assess the controls against them, and produce prioritized findings that can be fixed and verified.

It exists so that security is designed in rather than discovered after release, and so that security claims rest on evidence instead of checklists or reassurance.

**Two modes:**

- **Design-level** — after Workflows 03–04, before implementation. Produces security requirements and design findings.
- **Code-level** — against the actual code and configuration, before Workflow 12 (and on request). Produces implementation findings.

## 2. When to Use

Use when:

- Design-level: new projects; Tier 2 features that touch a trust boundary; all Tier 3 work.
- Code-level: before production readiness for Tier 2–3 releases; after significant changes to authentication, authorization, sensitive data, secrets, or infrastructure; on request.

Do not use when:

- Tier 0–1 changes with no trust-boundary impact. The code reviewer's security pass in Workflow 08 is enough.

Depth is proportional to context: a local single-user tool needs a short assessment; an internet-facing multi-tenant system handling payments needs a thorough one.

## 3. Required Inputs

- Specification: users, sensitive data, regulatory context, NFRs.
- Architecture and data/API design: components, trust boundaries, entry points, authorization model.
- Code-level: the code, configuration, dependency manifests and lockfiles, CI and deployment files.
- Deployment context: public internet, internal network, local only, or unknown.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Security Engineer | Leads; **read-only** throughout. |
| Software Architect | Clarifies boundaries and component responsibilities. |
| Database Specialist | Clarifies data storage, access paths, and sensitive fields. |
| API and Integration Specialist | Clarifies authorization per operation and external integrations. |
| DevOps Engineer | Clarifies infrastructure, CI permissions, and secret delivery. |
| Test Engineer | Turns verification requirements into security tests (with Workflow 07). |

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Scope and depth | State mode, scope, deployment context, and resulting depth. | — |
| 2. Assets and sensitive data | What is worth protecting and how sensitive it is. | 1 |
| 3. Trust boundaries and entry points | Map boundaries; enumerate entry points (from the design, or from the code: routes, handlers, consumers, jobs, file inputs). | 1 |
| 4. Threat modeling | For each entry point and actor: spoofing, tampering, information disclosure, denial of service, privilege escalation, repudiation. Include abuse by legitimate users. | 2–3 |
| 5. Authentication | Mechanism, library, session or token lifetime and revocation, credential storage, brute-force protection. | 3 |
| 6. Authorization and access control | Server-side checks on every protected operation; object-level ownership; tenant isolation; admin functions; default deny. | 3 |
| 7. Input validation and injection | Validation at boundaries; query, command, template, path, header, deserialization, SSRF, and cross-site scripting risks. | 3 |
| 8. Secrets | Location, delivery, rotation; none in code, history, logs, or CI output. | 3 |
| 9. Sensitive data and encryption | Exposure in responses, logs, errors, analytics; encryption in transit and at rest where needed; key handling; retention. | 2 |
| 10. Dependency risks | Audit tool results if available; reachability of vulnerable code; pinning; untrusted install scripts. | — |
| 11. API abuse | Rate limiting, enumeration, mass assignment, unbounded queries, resource exhaustion, business-logic abuse. | 3 |
| 12. Logging and auditing | Security events logged with actor, action, target, time; no secrets or unnecessary personal data in logs. | 3 |
| 13. Infrastructure and deployment risks | Exposed services, permissive network or CORS settings, debug modes, default credentials, CI token scope, infrastructure-code permissions. | 3 |
| 14. Common vulnerability classes | Cross-check against a recognized list (for example the OWASP Top 10 and OWASP API Security Top 10) to catch omissions. A cross-check, not the method. | 4–13 |
| 15. Security testing | Define (design-level) or run (code-level) tests that prove controls: negative authorization tests, validation tests, tool scans where available. | 4–13 |
| 16. Findings and prioritization | Rate by severity and realistic exploitability; assign evidence labels. | 4–15 |
| 17. Report | Write the assessment. | 16 |

## 6. Investigation Requirements

- Code-level findings come from reading the actual code and configuration; cite file and line.
- Enumerate entry points from the source, not from documentation.
- For each protected operation, find the authorization check and confirm it covers the specific resource, not only the route.
- Run available audit tools and report their actual output; if a tool was not run, say so.
- Never print secret values; reference location only.
- Do not attack systems the user does not own, and do not test against production without explicit authorization.

## 7. Decision Rules

- Prioritize realistic risk in this deployment context over theoretical worst cases.
- Fix classes of problems (centralized authorization, parameterized queries everywhere) rather than single instances where possible.
- Controls are proportionate to the risk profile.
- A concern without evidence is an Unverified concern, not a vulnerability.
- Never recommend weakening a control for convenience.
- Never conclude that the system is secure; report scope, findings, and residual risk.

## 8. Expected Deliverables

A report in `docs/reviews/` from `templates/security-assessment.md`. Every finding includes:

| Field | Content |
| --- | --- |
| Severity | Critical / High / Medium / Low / Info |
| Evidence | Evidence label plus the evidence itself (file:line, reproduction steps, tool output) |
| Attack scenario | Who could do what, and how |
| Impact | Consequence if exploited |
| Remediation | Specific fix |
| Verification requirement | How the fix will be proven, e.g. "request for another tenant's invoice returns 404; covered by an automated test" |
| Status | Open / Fix attempted / Reverified / Disputed / Accepted risk |

Design-level mode also produces security requirements to feed into the specification and implementation plan.

## 9. Verification / Completion Criteria

- All applicable stages covered or marked N/A with a reason.
- Every finding has all fields above.
- Scope not assessed and tools not run are listed.
- Critical and High findings have been reported to the user and are either scheduled for Workflow 09 or explicitly accepted (Critical findings still block release; see `principles/engineering-standards.md`).
- `checklists/security.md` applied for the relevant sections.

## 10. Escalation Conditions

- Any Critical or High finding → report to the user immediately, before the full report.
- Secrets in code, history, or logs → report location and recommend rotation.
- Sensitive or regulated data without adequate controls.
- A security finding requires an architectural change → return to Workflow 03.
- A requirement conflicts with security (for example, a request to disable authentication).

## 11. Failure / Stop Conditions

- Stop affected implementation if a Critical design flaw is found, until the user decides.
- Stop and report immediately on evidence of active compromise.
- Stop if assessment would require access the user has not authorized.
- The assessment does not modify code; remediation is a separate task under Workflow 09.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/05-security-assessment.md acting as
the Security Engineer (agents/security-engineer.md). Remain read-only.
Mode: [DESIGN-LEVEL / CODE-LEVEL]  Scope: [SCOPE]
Deployment context: [PUBLIC / INTERNAL / LOCAL / UNKNOWN]

1. State scope and depth. List assets, trust boundaries, and entry points
   (from the code for code-level).
2. Threat-model each entry point, including abuse by legitimate users.
3. Assess authentication, authorization (resource-level and tenant-level),
   validation and injection, secrets, sensitive data and encryption,
   dependencies (run the audit tool if available), API abuse, logging,
   infrastructure and deployment configuration.
4. Cross-check against common vulnerability classes.
5. Define or run security tests that prove controls.
6. Report each finding with severity, evidence, attack scenario, impact,
   remediation, verification requirement, and status, using
   templates/security-assessment.md. Never print secrets. Never state that
   the system is secure. Report Critical findings to me immediately.
```
