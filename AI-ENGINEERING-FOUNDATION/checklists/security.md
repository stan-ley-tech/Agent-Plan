# Checklist: Security

Gate for `workflows/05-security-assessment.md` and `prompts/security-review.md`. Apply only the sections relevant to the application and its deployment context.

**Rules:** tick `[x]` only with evidence (file:line, tool output, test result). Mark items that do not apply `N/A — reason`. "Reviewed" means inspected in the actual code or configuration, not assumed. Passing this checklist does not mean the system is secure.

## Required — Threat Model

- [ ] Scope, deployment context, and assessment depth stated
- [ ] Assets identified, with sensitivity
- [ ] Actors identified (legitimate users, administrators, attackers)
- [ ] Trust boundaries identified
- [ ] Attack surfaces identified (entry points enumerated from the code)
- [ ] Abuse cases by legitimate users considered

## Conditional — Authentication (if the system authenticates anyone)

- [ ] Authentication requirements defined
- [ ] Credential handling reviewed (established library; no custom hashing or crypto)
- [ ] Session/token handling reviewed (lifetime, revocation, storage, cookie attributes)
- [ ] Account lifecycle considered (creation, recovery, lockout, deactivation)

## Conditional — Authorization (if any operation is restricted)

- [ ] Permissions defined per operation
- [ ] Resource ownership checked server-side (object-level and tenant-level)
- [ ] Privilege escalation considered
- [ ] Administrative operations protected
- [ ] Default is deny for new operations

## Required — Input/Data

- [ ] Input validation reviewed at trust boundaries
- [ ] Injection risks reviewed (query, command, template, path, deserialization, SSRF, XSS)
- [ ] Sensitive data identified
- [ ] Sensitive data exposure reviewed (responses, logs, errors, analytics)
- [ ] Encryption requirements reviewed (in transit; at rest where needed)

## Conditional — Application/API (if the system exposes interfaces)

- [ ] API authentication reviewed
- [ ] API authorization reviewed
- [ ] Rate limiting considered
- [ ] Error responses reviewed (no stack traces or internals)
- [ ] CORS/CSRF considerations reviewed — where browsers are clients
- [ ] File upload handling reviewed — where uploads exist

## Required — Dependencies/Infrastructure

- [ ] Dependencies reviewed (audit tool run if available; results recorded; reachability assessed)
- [ ] Secrets reviewed (none in code, history, logs, or CI output; locations reported, values never printed)
- [ ] Configuration reviewed (debug off, safe defaults, no default credentials)

## Conditional — Dependencies/Infrastructure (if deployed)

- [ ] Production configuration reviewed
- [ ] Network exposure reviewed (exposed services, admin interfaces, CI token scope)

## Required — Observability

- [ ] Security-relevant events logged (actor, action, target, time)
- [ ] Logs avoid sensitive information
- [ ] Audit requirements considered

## Verification

- [ ] Security tests executed where applicable (negative authorization, validation); results recorded
- [ ] Tools not run are listed with the reason
- [ ] Findings documented in `templates/security-assessment.md`
- [ ] Each finding has severity, evidence, impact, affected area, remediation, and verification method
- [ ] Unverified concerns kept separate from evidenced findings
- [ ] Remediation verified (Workflow 09) for every finding marked Reverified

**Final Status**

```text
Findings: Critical __  High __  Medium __  Low __  Info __
Critical/High reported to user: YES / NO / NONE FOUND
Scope not assessed:
Unticked items and reasons:
Report location:
```
