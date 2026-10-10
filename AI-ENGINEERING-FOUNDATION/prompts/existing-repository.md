# Prompt: Existing Repository

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 01 Project Discovery (Track A), then a plan that names the next workflows.

## 1. Purpose

Build an evidence-based understanding of an unfamiliar repository and produce a project-specific development plan, without changing any code.

## 2. When to Use

Use when taking over or first working in a codebase you (or the AI) have not worked in before.

Use something else when:

- A discovery report and `docs/project-status.md` already exist and are recent → `continue-project.md`.
- You only need one focused change in a small, obvious area → `implement-feature.md` or `investigate-bug.md` (they include targeted inspection).

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Repository | Path or URL | Or "the currently open repository". |
| Goal | What you intend to do with it: take over, add a capability, stabilize, audit | Sets the depth of discovery. |
| Known context | Anything not in the repository: history, known problems, who uses it | Optional. |
| Permission to run | Whether the AI may run build and tests locally | Default: yes for local, non-destructive commands. |

Do not describe the stack or structure; the AI must discover them from the code.

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/existing-repository.md
(sections 5–8) and workflows/01-project-discovery.md (Track A).

Repository: [PATH OR URL, OR "THE CURRENTLY OPEN REPOSITORY"]
Goal: [GOAL]
Known context: [CONTEXT, OR "NONE"]

Rules:
- This task is read-only. Do not modify, reformat, or "improve" code, even
  where you dislike it. Record concerns as findings instead.
- Do not install or upgrade dependencies, run migrations, seed data, deploy,
  or contact external services. Ask before installing anything.
- If a URL is given, clone it locally; do not push.
- Read existing project instructions first; they take precedence over the
  foundation where they conflict. Report conflicts.
- Cite files or command output for every claim. Label findings Verified,
  Likely, Unverified concern, or Open question. Never print secret values.
- Stop for my review before creating any project documents.
```

## 5. Execution Sequence

1. **Read existing instructions and records**: `CLAUDE.md`, `AGENTS.md`, README, CONTRIBUTING, `docs/`, ADRs, CI configuration.
2. **Inspect** per Workflow 01 Track A: structure, stack and dependencies, entry points, architecture (trace one primary workflow end to end), database, APIs, integrations, configuration, tests, build/CI/deployment, documentation accuracy.
3. **Run the baseline**: build and tests, if safe; record exact commands and results.
4. **Analyze**: current limitations, known technical debt, technical risks (with severity where applicable), unknowns, areas not inspected.
5. **Plan** for the stated goal: priorities, recommended next workflow(s), first milestone, approval checkpoints, and which specialists will be needed.
6. **Report** and stop. Offer to create `docs/project-status.md` and, if missing, `docs/architecture.md` describing the current architecture.

## 6. Expected Output

- Discovery report in the structure defined in Workflow 01 section 8 (stack, structure, architecture, data, APIs, integrations, configuration, build/CI/deploy, tests and baseline results, documentation accuracy, limitations, technical debt, risks, unknowns, areas not inspected).
- Conflicts between existing project instructions and the foundation.
- Proposed development plan for the goal.
- Confirmation that no files were modified (version-control status).

## 7. Completion Criteria

- Every applicable area of Workflow 01 is covered or marked N/A with a reason.
- Every statement about the code cites files or command output.
- Baseline build and test results are recorded, or the reason they could not be run.
- Unknowns and uninspected areas are listed.
- Version control shows no changes.
- The plan names the next workflow and its approval checkpoints.

## 8. Stop / Escalation Conditions

Stop and report when:

- Secrets or production credentials are found in the repository (report location only).
- The build or tests cannot run without installing dependencies or accessing external services.
- Documentation materially contradicts the code.
- Existing project instructions conflict with the foundation.
- The repository is far larger than the goal requires → propose a narrower scope.
- There is evidence of compromise or malicious code.
- Any step would modify code, data, configuration, or an external system.
