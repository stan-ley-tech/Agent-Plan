# Workflow 03 — Architecture and Planning

> **Lifecycle:** 02 Requirements and Scope → **03 Architecture and Planning** → 04 Data and API Design. Iterative; see "Workflow lifecycle" in `README.md`.
> Decision method and ADR threshold: `principles/engineering-decision-making.md`.

## 1. Purpose

Translate approved requirements into an implementation-ready architecture and a sequenced plan.

It exists so that structure is decided deliberately, against requirements, before code makes it expensive to change, and so that every component and technology can be justified by something other than popularity or habit.

## 2. When to Use

Use when:

- A new project has an approved specification.
- A feature adds a component, a service, an integration, or a new data flow.
- A change crosses module boundaries or introduces new infrastructure or a major dependency.
- Implementation or testing reveals that the current architecture cannot meet a requirement.

Do not use when:

- The change fits inside one module's existing responsibility and uses existing patterns (go to Workflow 06, or 04 if data or contracts change).

## 3. Required Inputs

- Approved `docs/project-specification.md`.
- Discovery report (for existing systems: the current architecture with file references).
- Existing `docs/architecture.md` and ADRs.
- Operational constraints: hosting (as stated by the user), budget, team skills, who will operate the system.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Software Architect | Leads: boundaries, components, technology decisions, trade-offs, ADRs, sequencing. |
| Security Engineer | Assesses trust boundaries and security-relevant architecture choices. |
| DevOps Engineer | Assesses deployment model and operational burden of each option. |
| Database Specialist, API and Integration Specialist | Consulted on data ownership and integration boundaries at a high level; detailed design is Workflow 04. |
| Performance Engineer | Only when NFRs set demanding latency, throughput, or volume targets. |
| Engineering Orchestrator | Tracks decisions, conflicts, and the approval checkpoint. |

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Architectural drivers | List the requirements and constraints that shape structure: NFRs, integrations, data sensitivity, scale, team, budget. | Spec |
| 2. Current architecture | For existing systems, start from the discovered structure. The default is to extend it. | Discovery |
| 3. System boundaries | What is inside the system, what is external, who and what interacts with it. | 1 |
| 4. Components and responsibilities | Each component with a one-sentence responsibility and the data it owns. | 3 |
| 5. Service boundaries | Default: one deployable unit with clear internal modules. Separate deployables only for a stated need (independent scaling, isolation, separate ownership). | 4 |
| 6. Integration boundaries | How components and external systems communicate; synchronous vs asynchronous and why. | 4 |
| 7. Data flow | Trace each primary user workflow through the components. Gaps or duplicated responsibilities mean stage 4 is wrong. | 4–6 |
| 8. Technology decisions | For each significant choice, at least two realistic options evaluated per `principles/engineering-decision-making.md`. | 1 |
| 9. Cross-cutting concerns | Reliability (failure handling, redundancy needs), scalability (to the stated scale), observability (what operators must see), security considerations (trust boundaries, authentication approach), deployment considerations (target, environments). | 4–8 |
| 10. Failure modes | For each component and integration: how it fails, detection, impact, handling. | 4–6 |
| 11. Trade-offs and ADRs | Record consequential decisions as ADRs. | 8–10 |
| 12. Implementation sequencing | Milestones that each deliver working, testable functionality. Build a thin end-to-end slice first; tackle the riskiest assumptions early; order work by dependency. | all |
| 13. Review and approval | Present architecture, ADRs, and plan. | all |

## 6. Investigation Requirements

- For existing systems, base every statement about current architecture on code inspected in Workflow 01 or now, with file references.
- Check what the project and team already use before proposing anything new.
- Verify claims about external services or platforms against their documentation; otherwise label them Unverified.
- Do not design from the specification alone when existing code constrains the design.

## 7. Decision Rules

- Every component, service, and technology must trace to a driver from stage 1. If none, remove it.
- "Popular", "modern", "industry standard", or "more scalable" are not justifications without a requirement that needs the property.
- Prefer the existing stack and patterns; change them only for a requirement they cannot meet.
- Design for the stated scale with a known path to the next order of magnitude; do not build for imagined scale.
- Evaluate options on requirements, constraints, complexity, security, operational burden, cost, maintainability, failure modes, reversibility, and future change.
- Decide reversible choices quickly; spend effort on irreversible ones.
- Consequential decisions are recommendations until the user approves them.

## 8. Expected Deliverables

- `docs/architecture.md` from `templates/architecture-document.md`.
- One ADR per consequential decision in `docs/adr/`, from `templates/architecture-decision-record.md`.
- `docs/implementation-plan.md` from `templates/implementation-plan.md`, with milestones, work packages, dependencies, and approval checkpoints.

## 9. Verification / Completion Criteria

- Every component maps to at least one requirement; every primary workflow traces through components without gaps.
- Every consequential decision has an ADR with alternatives and revisit conditions.
- Failure modes and trust boundaries are identified.
- Each milestone delivers something testable.
- The user approves architecture, ADRs, and plan. **Approval checkpoint.**

## 10. Escalation Conditions

- Requirements cannot be met within constraints → present options and trade-offs.
- The simplest viable design still carries high operational cost or risk.
- The existing architecture blocks the requested work → propose a bounded structural change as separate scope.
- Specialists disagree on a consequential decision → orchestrator records both positions and asks the user.

## 11. Failure / Stop Conditions

- Do not start without an approved specification (return to Workflow 02).
- Do not begin implementation until the architecture is approved.
- Stop and return to Workflow 02 if architecture work reveals contradictory or missing requirements.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/03-architecture-and-planning.md
acting as the Software Architect (agents/software-architect.md).
Inputs: docs/project-specification.md, discovery output, existing
architecture and ADRs.

1. List architectural drivers from the requirements and constraints.
2. Start from the existing architecture where one exists; cite files.
3. Define boundaries, components (one-sentence responsibilities), service and
   integration boundaries, and data flow for each primary workflow.
4. Evaluate at least two options for each significant technology decision
   using principles/engineering-decision-making.md. Justify every choice by a
   requirement, never by popularity.
5. Address reliability, scalability (to stated scale), observability,
   security, deployment, and failure modes.
6. Write docs/architecture.md, ADRs, and docs/implementation-plan.md with
   milestones that each deliver testable functionality.
7. Stop for my approval before any implementation.
```
