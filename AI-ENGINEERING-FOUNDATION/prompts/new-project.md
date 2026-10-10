# Prompt: New Project

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent, opened in the project repository. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** 01 (Track B, or A if files exist) → 02 → 03 → 04 → 05 (design-level) → implementation plan. Implementation happens later, one milestone at a time, via `prompts/implement-feature.md`.

## 1. Purpose

Take a project from an idea or specification to an approved, phased implementation plan, with requirements, architecture, data and API design, and security requirements decided before code is written.

## 2. When to Use

Use when starting a new project or a new product built from scratch.

Use something else when:

- Code already exists and you are new to it → `existing-repository.md`.
- You are resuming planned work → `continue-project.md`.
- The project is planned and you are building a milestone → `implement-feature.md`.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Project idea | What it should do and for whom | A paragraph is enough; the AI will ask questions. |
| Target users | Who uses it, if known | "Unknown" is acceptable. |
| Constraints | Budget, deadline, required or forbidden technology, hosting, regulation | Only constraints you actually have. |
| Existing material | Specs, notes, mockups, systems it must integrate with | Paths or links. |
| Data sensitivity | Personal, financial, health, or confidential data expected | If known. |

Do not choose the stack in advance unless it is a real constraint; the architecture stage will justify one.

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/new-project.md
(sections 5–8). This is a staged planning task. Do not write application code.

Project idea: [PROJECT IDEA]
Target users: [TARGET USERS, OR "UNKNOWN"]
Constraints: [CONSTRAINTS, OR "NONE KNOWN"]
Existing material: [PATHS/LINKS, OR "NONE"]
Data sensitivity: [TYPES, OR "UNKNOWN"]

Rules:
- Inspect the repository first. If it is not empty, report what exists and
  do not overwrite it.
- Act as the Engineering Orchestrator (agents/engineering-orchestrator.md);
  involve specialists per its "When to involve each specialist" table.
- Follow workflows 01, 02, 03, 04 (where data or interfaces exist) and 05
  (design-level), and principles/engineering-decision-making.md.
- Label everything Stated, Assumed, or Open question, and trace each
  requirement to its source (my input, a document, or existing code). Do not
  invent requirements; ask when missing information affects correctness or risk.
- Justify every component and technology by a requirement, never by popularity.
- Stop at each approval checkpoint and wait for me.
```

## 5. Execution Sequence

1. **Inspect** the repository and any existing material (Workflow 01; Track B if empty, Track A if files exist).
2. **Understand** the idea: problem, users, outcome, constraints, data sensitivity, unknowns. Ask blocking questions. → **Checkpoint 1: discovery summary approved.**
3. **Define requirements and scope** (Workflow 02): numbered FRs, NFRs, BRs, ACs; non-goals; assumptions; open questions. → **Checkpoint 2: specification approved.**
4. **Design architecture** (Workflow 03): drivers, simplest viable structure, options for significant decisions, ADRs, failure modes, trust boundaries.
5. **Design data and APIs** (Workflow 04) where relevant.
6. **Assess security at design level** (Workflow 05): threats, required controls, security requirements.
7. **Plan implementation**: milestones that each deliver testable functionality, thin end-to-end slice first, riskiest assumptions early; note when Workflow 11 (environments, CI) should start.
8. **List unresolved decisions** with owner and needed-by milestone.
9. **Report** and stop. → **Checkpoint 3: architecture, ADRs, security requirements, and plan approved.**

## 6. Expected Output

- `docs/project-specification.md` (from `templates/project-specification.md`).
- `docs/architecture.md` and ADRs in `docs/adr/`.
- Data and API design (in the architecture document or a linked design document), where relevant.
- Design-level security assessment in `docs/reviews/`.
- `docs/implementation-plan.md` with milestones, dependencies, and approval checkpoints.
- `docs/project-status.md`.
- A summary: risk tier, key decisions with their drivers, unresolved decisions, and the recommended first milestone.

## 7. Completion Criteria

- All three checkpoints approved by the user.
- Every FR has a testable AC; every NFR is measurable.
- Every component and technology traces to a requirement or constraint; every consequential decision has an ADR with alternatives.
- Security requirements are recorded and reflected in the plan.
- Every milestone delivers something testable.
- No application code was written.

## 8. Stop / Escalation Conditions

Stop and ask when:

- The problem statement or target users cannot be confirmed.
- Blocking questions remain unanswered.
- Requirements conflict, or scope cannot fit the constraints.
- The project implies legal, regulatory, financial, or safety obligations not yet addressed.
- A decision would commit to cost, accounts, or infrastructure.
- The repository contains existing work that the plan would replace.
- You are asked to "just build it" before checkpoints are approved: explain what is undecided and confirm first.
