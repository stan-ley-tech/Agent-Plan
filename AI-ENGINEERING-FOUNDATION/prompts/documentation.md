# Prompt: Documentation

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 10 Documentation.

## 1. Purpose

Create or update project documentation so that it accurately describes the system as implemented, verified against the code.

## 2. When to Use

Use after changes to setup, configuration, interfaces, architecture, deployment, or operations; when onboarding documentation is missing; or before a release.

Use something else when:

- You need the current system understood first → `existing-repository.md` (its discovery feeds documentation).
- You want documentation of a planned design → that belongs in the specification or architecture documents produced by `new-project.md` or the design prompts, clearly marked as planned.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Scope | A change, feature, or the whole repository | |
| Audience | Developers, operators, API consumers, end users | |
| Documents | Specific files to focus on, or "all affected" | |
| Known gaps | Documentation you know is missing or wrong | Optional. |

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/documentation.md
(sections 5–8) acting as the Documentation Engineer
(agents/documentation-engineer.md), using workflows/10-documentation.md.

Scope: [SCOPE]
Audience: [AUDIENCE]
Documents: [FILES, OR "ALL AFFECTED"]
Known gaps: [GAPS, OR "NONE"]

Rules:
- Document only what the code actually does. Read the code, configuration,
  and scripts behind every statement.
- Never describe functionality that does not exist. Label planned items as
  planned, or omit them.
- Run documented commands where safe before calling them working;
  otherwise mark them not verified.
- One fact in one place; link instead of duplicating. Do not restate code.
- Use placeholders in examples; never real secrets, hosts, or personal data.
- Do not change code to match documentation; report mismatches.
```

## 5. Execution Sequence

1. **Identify** affected documents using the impact table in Workflow 10.
2. **Inspect** the code, configuration, and scripts each document describes.
3. **List discrepancies** between existing documentation and actual behavior.
4. **Write or update**, where relevant: setup, architecture, APIs, configuration (purpose, default, required, secret), development workflow, testing, deployment, operations and runbooks, troubleshooting, important decisions (ADRs), known limitations.
5. **Remove** content describing behavior that no longer exists.
6. **Verify** documented commands where safe.
7. **Check** links and paths; update `docs/project-status.md`.
8. **Report.**

## 6. Expected Output

- Documents created or changed, each with what it was verified against (code file or command run).
- Discrepancies found and how each was resolved.
- Commands verified with results.
- Items not verified, with the reason.
- Code/spec mismatches reported for decision.

## 7. Completion Criteria

- Every changed statement was checked against code or by execution.
- No document describes unimplemented functionality as existing.
- Every configuration setting in the code is documented, and every documented setting exists.
- No secrets or real infrastructure details in examples.
- Stale content for removed behavior is gone.

## 8. Stop / Escalation Conditions

Stop and ask when:

- Code and specification disagree and the intended behavior is unclear.
- A procedure cannot be verified without production access.
- Documentation would expose security-sensitive operational detail → involve the Security Engineer.
- The requested documentation describes features that are not implemented.
