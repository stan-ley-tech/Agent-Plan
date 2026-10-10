# Workflow 10 — Documentation

> **Lifecycle:** 09 Remediation and Reverification → **10 Documentation** → 11 DevOps and Deployment Planning. Also runs whenever documented behavior changes. Iterative; see "Workflow lifecycle" in `README.md`.

## 1. Purpose

Produce and maintain documentation that describes the system as it actually is, so that developers, operators, API consumers, and future AI sessions can work without rediscovering it.

It exists because stale or aspirational documentation is worse than none: it causes confident mistakes.

## 2. When to Use

Use when:

- Implementation changed setup, configuration, interfaces, architecture, operations, or user-visible behavior.
- A repository has missing or stale documentation (often found in Workflow 01).
- Before a release (feeds Workflow 12).
- A significant decision or known limitation must be recorded.

Do not use when:

- The change is invisible to every reader of every document (an internal refactor with no setup, interface, or behavior change). Updating `docs/project-status.md` is still expected if project state changed.

## 3. Required Inputs

- The change (diff) or the area to document.
- The actual code, configuration, scripts, and interface definitions.
- Existing documentation and ADRs.
- The intended audience for each document.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Documentation Engineer | Leads; writes and verifies documentation against the code. |
| Role responsible for the changed area | Confirms accuracy: Software Architect (architecture), API and Integration Specialist (API reference), DevOps Engineer (setup, deployment, configuration), Release and Reliability Engineer (runbooks, rollback). |

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Impact mapping | Map the change to affected documents using the table below. | — |
| 2. Read the source | Read the code, configuration, and scripts each affected document describes. | 1 |
| 3. Discrepancies | List where current documentation differs from actual behavior. | 2 |
| 4. Update | Update each affected document for its audience. Remove content for behavior that no longer exists. | 3 |
| 5. Verify procedures | Run documented commands (setup, build, test, run) where safe; record results. | 4 |
| 6. Decisions and limitations | Ensure consequential decisions have ADRs; record known limitations and accepted risks in `docs/project-status.md`. | 4 |
| 7. Links and consistency | Check paths and links; one fact in one place, linked elsewhere. | 4 |

| Change type | Documents to check |
| --- | --- |
| New or changed component, boundary, data flow | Architecture document, ADRs |
| Interface or contract change | API reference, changelog |
| New dependency, tool, or setup step | Setup instructions, development workflow |
| New or changed setting or secret | Configuration reference (purpose, default, required, secret or not) |
| Build, CI, or deployment change | Deployment documentation, development workflow |
| New failure mode or operational procedure | Troubleshooting guide, runbooks (deploy, roll back, recover, rotate credentials) |
| Accepted debt, limitation, or risk | `docs/project-status.md` known limitations |
| Anything maintainers must know to keep it working | Maintenance notes (upgrade paths, scheduled tasks, ownership) |

## 6. Investigation Requirements

- Document from the code and configuration, not from the specification or memory.
- Confirm every configuration setting documented exists in the code, and every setting in the code is documented.
- Run commands before documenting them as working; otherwise label them not verified.
- Check whether existing documentation already covers the topic before adding new text.

## 7. Decision Rules

- Accuracy over completeness: a short correct document beats a long speculative one.
- Describe the actual system. Planned behavior is labeled as planned, or omitted.
- Document what readers cannot quickly infer from code: purpose, setup, configuration, decisions, operations, limitations. Do not restate code.
- Follow the project's existing documentation structure and tone.
- Examples use placeholders; never real secrets, internal hostnames, or personal data.
- Where code and specification disagree, report it; do not silently pick one.

## 8. Expected Deliverables

- Updated documents: architecture, API reference, setup, development workflow, configuration, deployment, troubleshooting, runbooks, ADRs, maintenance notes, as affected.
- Updated `docs/project-status.md`.
- A short report: documents changed, what each was verified against, discrepancies found and resolved, commands run and results, items not verified.

## 9. Verification / Completion Criteria

- Every affected document reflects current behavior, verified against code or by execution.
- Documented commands were run, or are labeled not verified with the reason.
- No stale content remains for removed behavior.
- No secrets or real infrastructure details in examples.
- A new developer could set up and run the project from the documentation (for setup changes).

## 10. Escalation Conditions

- Code and specification disagree and intended behavior is unclear → user decides; may return to Workflow 02.
- Operational procedures cannot be verified without production access.
- Documenting a procedure would expose security-sensitive detail → Security Engineer.

## 11. Failure / Stop Conditions

- Stop rather than document behavior you cannot confirm exists.
- Do not change code to match documentation within this workflow; report the mismatch.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/10-documentation.md acting as the
Documentation Engineer (agents/documentation-engineer.md).
Scope: [CHANGE / AREA]  Audience: [AUDIENCE]

1. Map the change to affected documents using the workflow's table.
2. Read the actual code, configuration, and scripts behind each document.
3. List discrepancies, then update documents to match actual behavior;
   remove stale content.
4. Run documented commands where safe and record results.
5. Ensure decisions have ADRs and limitations are in docs/project-status.md.
6. Do not document planned or unimplemented behavior as existing; use
   placeholders in examples. Report documents changed, discrepancies, and
   anything not verified.
```
