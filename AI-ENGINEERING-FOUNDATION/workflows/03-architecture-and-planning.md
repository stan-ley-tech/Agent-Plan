# Workflow 03 — Architecture and Planning

## Purpose

Choose the simplest structure that satisfies the approved requirements, record the significant decisions, and produce a roadmap that can be implemented in increments.

## When to invoke

- After Workflow 02 is approved for a new project.
- When a feature adds components, integrations, or changes data flow.
- When assessing an existing repository's architecture.

## Required inputs

- Approved `docs/project-specification.md`.
- Existing code, architecture documents, and ADRs, if any.
- Operational constraints: hosting, budget, team.

## Relevant agents

- **Software Architect** — leads.
- **Security Engineer** — consulted on trust boundaries.
- **DevOps Engineer** — consulted on operational implications.
- **Performance Engineer** — consulted only if NFRs include demanding performance targets.
- **Engineering Orchestrator** — tracks decisions and approvals.

## Steps

1. List the requirements and constraints that drive architecture.
2. For an existing system, map the current architecture from the code.
3. Propose the simplest viable structure (default: a single deployable unit with clear modules).
4. For each significant decision (language, framework, data store, hosting, integration pattern, authentication approach), evaluate at least two options using `principles/engineering-decision-making.md`.
5. Define component responsibilities and data flow. Trace each primary user workflow through the components.
6. Identify trust boundaries and external integrations.
7. Identify failure modes and how each is detected and handled.
8. Identify operational needs: environments, deployment model, monitoring.
9. Write ADRs for consequential decisions (`docs/adr/`).
10. Write `docs/architecture.md` using `templates/architecture-document.md`.
11. Produce a phased roadmap: milestones that each deliver working, testable functionality. Use `templates/implementation-plan.md`.

## Deliverables

- `docs/architecture.md`.
- ADRs for consequential decisions.
- Implementation plan with milestones.

## Verification criteria

- Every component maps to at least one requirement.
- Every primary workflow is traceable through components.
- Each consequential decision has an ADR with alternatives considered.
- No infrastructure is included without a requirement that needs it.

## Completion criteria

- The user approves the architecture, ADRs, and roadmap. **This is an approval checkpoint.**

## Escalation conditions

- Requirements cannot be met within constraints.
- The simplest viable design still carries high operational cost.
- Existing architecture blocks the requested work.

## Stop conditions

- Stop if the specification is not approved.
- Stop before implementation until the architecture is approved.
