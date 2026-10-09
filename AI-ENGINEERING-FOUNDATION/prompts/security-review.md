# Prompt: Security Review

```text
Task: Perform an independent, risk-based security assessment.

Scope: [WHOLE REPOSITORY / FEATURE / BRANCH OR DIFF]
Deployment context: [PUBLIC INTERNET / INTERNAL NETWORK / LOCAL ONLY / UNKNOWN]
Sensitive data handled: [TYPES, OR "UNKNOWN"]
Regulatory context: [ANY, OR "NONE KNOWN"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/security-engineer.md
- AI-ENGINEERING-FOUNDATION/principles/security-principles.md
- AI-ENGINEERING-FOUNDATION/workflows/05-security-assessment.md
- AI-ENGINEERING-FOUNDATION/checklists/security.md
- docs/architecture.md, if present

You are read-only for this task. Do not modify code or configuration.

Process:
1. Establish what the application does, who uses it, and where it runs.
   Set the assessment depth accordingly and state it.
2. List assets and trust boundaries.
3. Enumerate entry points from the actual code: routes, handlers, consumers,
   scheduled jobs, CLI inputs, file inputs.
4. For each entry point check authentication, authorization including
   resource ownership and tenant isolation, input validation, and output
   encoding.
5. Trace sensitive data through storage, logs, error messages, and responses.
6. Search for secrets in code, configuration, and history. Report locations
   only; never print values.
7. Review dependency manifests; run the ecosystem's audit tool if available
   and report its actual output. Assess reachability before assigning severity.
8. Review security-relevant configuration (debug, CORS, headers, cookies,
   default credentials, admin exposure).
9. Consider abuse cases by legitimate users.
10. Apply checklists/security.md.

Quality and safety:
- Do not attack systems or test against production.
- Prioritize by realistic exploitability in this deployment context.
- Do not state or imply that the application is secure.

Deliverables:
- docs/reviews/security-assessment-[DATE].md from
  templates/security-assessment.md, with each finding's severity, evidence
  label, location, attack scenario, impact, and remediation; scope assessed
  and not assessed; residual risks.

Verification:
- Verified findings cite file:line, reproducible steps, or tool output.
- Tools not run are listed as not run.

Report Critical findings and any discovered secrets to me immediately,
before completing the full report. Remediation is a separate task that I
will authorize.
```
