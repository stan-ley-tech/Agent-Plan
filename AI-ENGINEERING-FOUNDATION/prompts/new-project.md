# Prompt: New Project

Use when starting a project from an idea. Replace the placeholders, then paste everything inside the block into Claude Code, opened in the (possibly empty) project repository.

```text
Task: Take the project idea below from concept to an approved, phased
implementation plan. Do not write application code in this task.

Project idea: [PROJECT IDEA]
Target users: [TARGET USERS, OR "UNKNOWN"]
Known constraints: [BUDGET / TIMELINE / REQUIRED TECHNOLOGY / HOSTING / REGULATION, OR "NONE KNOWN"]
Existing material: [LINKS OR FILES, OR "NONE"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/principles/ (all four documents)
- AI-ENGINEERING-FOUNDATION/agents/engineering-orchestrator.md
- AI-ENGINEERING-FOUNDATION/workflows/01 through 05

Inspect the repository first. If it is not empty, report what exists and do
not overwrite it.

Process — act as the Engineering Orchestrator and run these phases in order.
Stop at each checkpoint and wait for my approval before continuing.

Phase 1 — Discovery (workflows/01-project-discovery.md, agents/product-analyst.md)
  Restate the problem, users, intended outcome, constraints, data sensitivity,
  initial scope, assumptions, and open questions. Ask me the questions that
  block progress. Do not choose technology yet.
  CHECKPOINT 1: I approve the discovery summary.

Phase 2 — Requirements (workflows/02-requirements-and-scope.md)
  Write docs/project-specification.md from templates/project-specification.md.
  Number requirements and acceptance criteria. Label items Stated, Assumed, or
  Open question. List non-goals.
  CHECKPOINT 2: I approve the specification.

Phase 3 — Architecture (workflows/03-architecture-and-planning.md, agents/software-architect.md)
  Propose the simplest architecture that meets the requirements. Evaluate
  alternatives for significant decisions using
  principles/engineering-decision-making.md. Write docs/architecture.md and
  ADRs in docs/adr/.

Phase 4 — Data and API design (workflows/04-data-and-api-design.md)
  Only if the project has persistent data or interfaces.

Phase 5 — Security assessment (workflows/05-security-assessment.md)
  Design-level threat model proportional to the project's risk.

Phase 6 — Implementation plan
  Write docs/implementation-plan.md from templates/implementation-plan.md with
  milestones that each deliver working, testable functionality. Mark approval
  checkpoints. Create docs/project-status.md from templates/project-status.md.
  CHECKPOINT 3: I approve architecture, ADRs, security requirements, and plan.

Quality and safety:
- Do not invent requirements. Ask, or label assumptions.
- Avoid unnecessary services, infrastructure, and dependencies. Justify every
  technology choice against requirements.
- Assign and state a risk tier.
- Do not create cloud resources, accounts, or credentials.

Deliverables:
- docs/project-specification.md, docs/architecture.md, docs/adr/*,
  docs/implementation-plan.md, docs/project-status.md, and a design-level
  security assessment in docs/reviews/.

Verification:
- Every component traces to a requirement; every requirement has acceptance
  criteria; every consequential decision has an ADR with alternatives.
- Run checklists/project-discovery.md and report the result.

Ask me when missing information materially affects correctness, cost, or risk.
Do not begin implementation until I approve Checkpoint 3 and name the first
milestone to build.
```
