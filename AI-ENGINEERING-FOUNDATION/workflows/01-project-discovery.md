# Workflow 01 — Project Discovery

> **Lifecycle:** **01 Discovery** → 02 Requirements and Scope. The lifecycle is iterative; see "Workflow lifecycle" in `README.md`.
> Risk tiers, evidence labels, and severity levels are defined in `principles/engineering-standards.md`.

## 1. Purpose

Build an evidence-based understanding of the project as it actually exists before anyone defines requirements, designs, or changes code.

It exists because the most common failure of AI-assisted development is acting on an assumed system: guessing the stack, inventing conventions, and producing changes that conflict with code nobody read.

Discovery is **read-only**. It produces understanding, not changes.

## 2. When to Use

Use when:

- Working in a repository for the first time, or inheriting a project.
- Starting significant work in an area of the codebase not yet understood.
- Project documents are missing, stale, or contradicted by the code.
- Starting a new project with no code yet (Track B below).

Do not use when:

- A current discovery report and `docs/project-status.md` exist and the task stays inside an already-understood area. Use `prompts/continue-project.md` instead.
- The task is Tier 0. Read the file being changed and make the change.

**Tracks**

- **Track A — Existing repository.** Full inspection (stages A1–A12).
- **Track B — New project, no code.** Short context capture (stages B1–B6). Detailed problem definition belongs to Workflow 02.

## 3. Required Inputs

- Access to the repository (local checkout or URL to clone). Track B: the project idea and any existing material.
- The user's goal for the project or the upcoming work, which sets the depth of discovery.
- Ability to run local, non-destructive commands (optional but strongly preferred).

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Engineering Orchestrator | Chooses track and depth, assigns the initial risk tier, assembles the report. |
| Software Architect | Maps structure, entry points, components, and request flow (A3–A4). |
| Database Specialist | Inspects data stores, schema, migrations, data access (A5). |
| API and Integration Specialist | Inventories exposed interfaces and external integrations (A6). |
| DevOps Engineer | Inspects configuration, build, CI, deployment evidence (A7–A8). |
| Test Engineer | Determines how tests run and records the baseline (A9). |
| Security Engineer | Read-only sweep for evident red flags only: committed secrets, missing authentication on obvious entry points (A7, A11). The full assessment is Workflow 05. |
| Documentation Engineer | Compares documentation to the code (A10). |
| Product Analyst | Track B lead; in Track A, records current user-facing behavior when requirements work follows. |

For a small repository, one session can perform all roles in sequence. Involve only the roles whose areas exist in the project.

## 5. Workflow Sequence

### Track A — Existing repository

| Stage | What happens | Depends on |
| --- | --- | --- |
| A1. Existing instructions and records | Read `CLAUDE.md`, `AGENTS.md`, `README`, `CONTRIBUTING`, `docs/`, ADRs, `docs/project-status.md`. Note any project rules that override the foundation. | — |
| A2. Technology stack and dependencies | Identify languages, frameworks, runtime versions, and package manager from manifests and lockfiles. Note outdated or unusual dependencies. | A1 |
| A3. Structure and entry points | Map top-level layout and every entry point: servers, route definitions, CLIs, workers, scheduled jobs, event consumers. | A2 |
| A4. Existing architecture | Identify modules, layering, and boundaries. Trace one primary workflow end to end, from entry point to storage and back. | A3 |
| A5. Database | Identify engine, schema source, migration history, data-access approach, and notable constraints or their absence. | A3 |
| A6. APIs and integrations | List exposed interfaces and their authentication. List outbound services, webhooks, queues, and how failures are handled. | A3 |
| A7. Configuration | List configuration sources, environment variables, example files, and where secrets are expected to come from. Record secret *locations* only. | A2 |
| A8. Build, CI, and deployment | Inspect build scripts, CI files, container files, infrastructure code. Record what deployment evidence exists; do not infer a target that is not evidenced. | A2 |
| A9. Tests | Identify test frameworks and commands. Run the suite if safe. Record pass/fail/skip counts and which areas have no tests. | A2 |
| A10. Documentation state | Compare documented setup, architecture, and behavior to what the code shows. List contradictions. | A1–A9 |
| A11. Limitations, risks, unknowns | Synthesize: current limitations, technical risks (untested critical paths, fragile areas, security red flags, debt), and unknowns. | A1–A10 |
| A12. Report and checkpoint | Produce the discovery report and recommend the next workflow. | A11 |

Depth is proportional to the goal: a focused change needs A1–A4 plus the areas it touches. A takeover of the whole project needs every stage.

### Track B — New project, no code

| Stage | What happens |
| --- | --- |
| B1. Idea as stated | Record the idea, intended users, and desired outcome in the user's words. |
| B2. Existing material | Collect notes, references, and any existing systems the project must integrate with. |
| B3. Constraints | Budget, timeline, required or forbidden technology, hosting, regulation. |
| B4. Data sensitivity | Personal, financial, health, credential, or confidential data expected. |
| B5. Unknowns and risks | What is unclear; what could make the project infeasible. |
| B6. Report and checkpoint | Discovery summary and initial risk tier. Hand off to Workflow 02. |

## 6. Investigation Requirements

- **Do not modify anything.** No code edits, formatting, dependency installs or upgrades, migrations, seed scripts, or generated files. The working tree must be unchanged at the end, except for project documents the user approves at the checkpoint.
- Run only local, non-destructive commands: listing, reading, build, test, lint, type check. Never run deploy scripts, migrations, data scripts, or commands that contact external services.
- If running tests requires installing dependencies, ask first.
- Determine the stack from manifests, lockfiles, and source, not from the repository name or a single file.
- Read the code, not only the documentation. Where they disagree, the code describes current behavior; the disagreement is a finding.
- Cite file paths or command output for every statement about the system.
- Never print secret values. Report the file and line.

## 7. Decision Rules

- Discovery makes no design or implementation decisions. Its only decisions are track, depth, and initial risk tier.
- Label every finding with an evidence label. Unknowns are listed as Open questions, never filled in with plausible guesses.
- Existing project conventions are recorded as facts to be followed later, not judged here.
- If the goal needs only part of the repository, narrow the depth and say what was not inspected.

## 8. Expected Deliverables

A **discovery report** (in the session, or saved under `docs/` if the user wants it kept):

```
Summary and recommended next workflow
Initial risk tier and reason
Stack and dependencies            (with file references)
Structure and entry points
Architecture and traced workflow
Database
APIs and integrations
Configuration and secret handling (locations only)
Build, CI, deployment evidence
Tests and baseline results        (commands and actual output)
Documentation accuracy
Current limitations
Technical risks                   (with severity where applicable)
Unknowns / open questions
Areas not inspected
```

After user approval, optionally create `docs/project-status.md` from `templates/project-status.md` and, if missing, `docs/architecture.md` describing the current architecture.

Track B: a discovery summary that seeds `docs/project-specification.md`.

## 9. Verification / Completion Criteria

- Every applicable stage is covered or marked N/A with a reason.
- Every claim about the system cites evidence and carries an evidence label.
- Test baseline is recorded with the command and actual result, or the reason it could not be run.
- Unknowns and areas not inspected are listed.
- Version control shows no changes to code or configuration.
- `checklists/project-discovery.md` has been applied where relevant.
- The user has reviewed the report. **Approval checkpoint.**

## 10. Escalation Conditions

- Committed secrets or production credentials found → report immediately (Security Engineer).
- Build or tests cannot run → report what was tried; ask whether to install dependencies or proceed without a baseline.
- Documentation materially contradicts the code.
- Existing project instructions conflict with the foundation → report; project rules take precedence unless the user decides otherwise.
- The repository is far larger than the stated goal requires → propose a narrower scope.

## 11. Failure / Stop Conditions

- Stop if the user asks for implementation before discovery is complete: explain what is not yet understood and confirm before proceeding.
- Stop before any action that would modify code, data, configuration, or an external system.
- Stop if the repository cannot be accessed.
- Stop and report if there is evidence of compromise (unexpected credentials, malicious scripts, tampered dependencies).

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/01-project-discovery.md.
Goal: [GOAL FOR THIS PROJECT OR UPCOMING WORK]
Track: [A — EXISTING REPOSITORY / B — NEW PROJECT, NO CODE]

This workflow is read-only. Do not modify code, configuration, or data, and
do not install dependencies without asking.
1. Read existing instructions and project records first.
2. Track A: inspect stack, entry points, architecture (trace one workflow end
   to end), database, APIs and integrations, configuration, build/CI/deploy,
   tests (run the baseline if safe), and documentation accuracy.
   Track B: capture the idea, users, outcome, constraints, data sensitivity,
   unknowns, and risks.
3. Cite files or command output for every claim; label each Verified, Likely,
   Unverified concern, or Open question. Never print secret values.
4. List limitations, technical risks, unknowns, and areas not inspected.
5. Produce the discovery report, recommend the next workflow, and stop for
   my review.
```
