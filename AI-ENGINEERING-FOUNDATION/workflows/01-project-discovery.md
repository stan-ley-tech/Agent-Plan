# Workflow 01 — Project Discovery

## Purpose

Understand the problem, the people who have it, and the outcome they want before anyone designs or builds anything.

## When to invoke

- A new project starts from an idea.
- An existing project takes on a substantially new goal.
- A request is too vague to write requirements for.

Skip for well-defined changes inside an established project.

## Required inputs

- The user's description of the idea or problem.
- Any existing material: notes, documents, competitor references, existing system.

## Relevant agents

- **Engineering Orchestrator** — runs the workflow, assigns risk tier.
- **Product Analyst** — leads discovery.
- **Software Architect** — consulted only for feasibility questions; does not design yet.

## Steps

1. Restate the problem in two or three sentences. Confirm with the user.
2. Identify users and stakeholders: who uses it, who administers it, who pays, who is affected.
3. Describe the intended outcome: what changes for the users when this works.
4. Describe how the problem is handled today, if at all.
5. Identify constraints: budget, timeline, required technology, hosting, regulation, existing systems that must be integrated.
6. Identify business rules and domain terms already known.
7. Identify data sensitivity: personal, financial, health, credentials, confidential.
8. Draft initial scope boundaries: what is clearly in, what is clearly out.
9. List assumptions and missing information. Ask the user the questions that block progress; record the rest.
10. Assign an initial risk tier for the project (see `principles/engineering-standards.md`).
11. Complete `checklists/project-discovery.md`.

Do not choose technologies, design architecture, or write code in this workflow.

## Deliverables

- A discovery summary (problem, users, outcome, constraints, sensitivity, initial scope, assumptions, open questions). It can become the first draft of `docs/project-specification.md`.

## Verification criteria

- The user has confirmed the problem statement.
- Every item is labeled as stated by the user or assumed.
- Blocking questions are answered or explicitly deferred by the user.

## Completion criteria

- The user approves the discovery summary. **This is an approval checkpoint.**

## Escalation conditions

- The user's goals conflict.
- The idea implies legal, regulatory, financial, or safety exposure.
- Constraints make the outcome infeasible.

## Stop conditions

- Stop and wait if the problem statement is not confirmed.
- Stop if the user has not answered questions that determine whether the project is viable.
