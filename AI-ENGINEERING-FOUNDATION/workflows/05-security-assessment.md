# Workflow 05 — Security Assessment

## Purpose

Identify realistic threats, define the controls the system needs, and document prioritized risks — during design and again against actual code.

## When to invoke

- Design phase of new projects (after Workflows 03–04).
- Any Tier 2 change that touches a trust boundary.
- All Tier 3 work.
- On request, as an independent assessment of existing code.

## Required inputs

- Specification (sensitive data, users, NFRs).
- Architecture and data/API design (trust boundaries, entry points).
- For code assessment: the actual code, configuration, and dependency manifests.
- Deployment context.

## Relevant agents

- **Security Engineer** — leads; read-only during assessment.
- **Software Architect**, **Database Specialist**, **API and Integration Specialist** — consulted to clarify design.

## Steps

1. Set the depth of the assessment based on context (what the system does, where it runs, what data it holds).
2. List assets and their sensitivity.
3. Map trust boundaries and entry points.
4. Identify actors: legitimate users, administrators, external attackers, compromised dependencies.
5. For each entry point, assess spoofing, tampering, information disclosure, denial of service, and privilege escalation.
6. Identify abuse cases by legitimate users.
7. Define required authentication and authorization per operation.
8. For code assessments: inspect entry points, authorization checks, validation, data handling, secrets, dependencies, and configuration (see `agents/security-engineer.md`).
9. Rate findings by severity and evidence label.
10. Recommend controls and remediation, prioritized.
11. Record residual risks.
12. Write the result using `templates/security-assessment.md` in `docs/reviews/`.
13. Complete `checklists/security.md`.

## Deliverables

- Security assessment report.
- Security requirements to feed into implementation (design phase).
- Prioritized remediation list (code phase).

## Verification criteria

- Each finding has severity, evidence label, location or scenario, and remediation.
- The report states scope assessed and not assessed.
- Tool results are reported as actually observed.

## Completion criteria

- Report delivered. Critical and High findings are acknowledged by the user and either scheduled for remediation (Workflow 09) or explicitly accepted.

## Escalation conditions

- Any Critical or High finding.
- Secrets found in code or history.
- Sensitive or regulated data without adequate controls.

## Stop conditions

- Stop implementation of affected work if a Critical design flaw is found, until the user decides.
- Stop and report immediately if evidence of compromise is found.
- Never state that the system is secure.
