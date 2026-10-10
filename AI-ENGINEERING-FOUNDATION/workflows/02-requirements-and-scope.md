# Workflow 02 — Requirements and Scope

> **Lifecycle:** 01 Discovery → **02 Requirements and Scope** → 03 Architecture and Planning. Iterative; see "Workflow lifecycle" in `README.md`.
> Risk tiers, evidence labels, and severity levels: `principles/engineering-standards.md`.

## 1. Purpose

Turn a project idea or change request into testable engineering requirements with fixed scope boundaries.

It exists to stop two failures: building from ambiguous requirements (so "done" cannot be judged) and feature creep (so scope grows without anyone deciding it should).

## 2. When to Use

Use when:

- A new project has completed Workflow 01.
- A Tier 2+ feature lacks written, approved acceptance criteria.
- A request is broad, vague, or disputed.
- Requirements change after approval (re-enter to process the change).

Do not use when:

- Tier 0–1 work already has clear acceptance criteria (a well-specified bug, a small contained change).
- The only open questions are technical design questions; those belong to Workflow 03 or 04.

## 3. Required Inputs

- Discovery report or summary from Workflow 01.
- The user's description of the idea or request, and user availability for questions.
- Existing specification, if any.
- For changes to a running system: current behavior, as verified in the code.

## 4. Relevant Agents

| Agent | Contribution |
| --- | --- |
| Product Analyst | Leads: problem, users, workflows, requirements, rules, criteria, scope. |
| Security Engineer | Contributes security and privacy requirements when sensitive data, authentication, or external exposure is involved. |
| Software Architect | Flags requirements that are infeasible or disproportionately expensive. Does not design. |
| Test Engineer | Optional: confirms acceptance criteria are testable for Tier 3 work. |
| Engineering Orchestrator | Confirms risk tier; owns scope control after approval. |

## 5. Workflow Sequence

| Stage | What happens | Depends on |
| --- | --- | --- |
| 1. Problem definition | State who has what problem, what it costs, and how it is handled today. Confirm with the user. | Discovery |
| 2. Users and actors | List user types, administrators, operators, and external systems that act on the system. | 1 |
| 3. User workflows | For each actor, the steps to reach the goal, including failure, cancellation, and retry paths. | 2 |
| 4. Functional requirements | Derive numbered FRs from the workflows. For existing systems, state current behavior and the required change. | 3 |
| 5. Business rules | Extract numbered BRs: invariants, calculations, state transitions, eligibility rules. Probe edge cases. | 3 |
| 6. Non-functional requirements | Only those that matter, each measurable: performance, availability, security, privacy, accessibility, compliance, platforms. | 2 |
| 7. Constraints | Budget, timeline, technology, hosting, regulation, integration with existing systems. | 1 |
| 8. Assumptions | Everything inferred rather than stated, with the impact if wrong. | 4–7 |
| 9. Acceptance criteria | Numbered ACs for every FR, testable without interpretation. | 4–5 |
| 10. Scope boundaries | In scope for this release or milestone. | 4 |
| 11. Out-of-scope items | Explicit non-goals, including ideas deferred to later. | 10 |
| 12. Risks | Product, delivery, and compliance risks visible at this stage. | 4–11 |
| 13. Unresolved questions | Each with owner, impact, and whether it blocks progress. | all |
| 14. Review and approval | Present the specification. | all |

## 6. Investigation Requirements

- Read the discovery output and any existing specification before writing anything.
- For existing systems, verify current behavior in the code; do not rely on the user's or documentation's recollection alone.
- Ask the user when a requirement has more than one reasonable interpretation. Do not choose silently.
- Check new requirements against existing ones and existing behavior for conflicts.

## 7. Decision Rules

- Every requirement traces to a user statement, an existing document, or observed behavior. Untraceable requirements are removed or turned into questions.
- Vague terms ("fast", "secure", "scalable", "intuitive") become measurable criteria or are removed.
- **Ambiguous** (several plausible meanings) → ask. **Incomplete but low-impact** → record an assumption and proceed.
- Prefer the smallest scope that solves the core problem. Additional ideas go to out-of-scope or a later milestone.
- **Scope control after approval:** any addition is a change request stating the item, its reason, and its impact on effort, risk, and timeline. Only the user approves it. No gold-plating by any agent.
- Technology choices are not requirements unless the user imposes them as constraints.

## 8. Expected Deliverables

- `docs/project-specification.md` from `templates/project-specification.md`, with FR, NFR, BR, and AC numbering and every item labeled Stated, Assumed, or Open question.
- A list of blocking questions, separate from non-blocking ones.
- After approval: a change log section recording approved scope changes.

## 9. Verification / Completion Criteria

- Every FR has at least one AC; every AC is observable and testable.
- Every NFR is measurable.
- Non-goals are explicit.
- No blocking question remains unanswered or undeferred.
- Assumptions are visible to the user.
- The user approves the specification. **Approval checkpoint.**

## 10. Escalation Conditions

- Requirements conflict with each other or with constraints.
- A requirement implies legal, regulatory, financial, or safety obligations.
- Requested scope cannot fit the constraints → present options (reduce scope, extend timeline, accept risk).
- A proposed change after approval would materially change effort or risk.

## 11. Failure / Stop Conditions

- Stop if the problem statement is not confirmed.
- Stop if an acceptance criterion cannot be written for a core requirement; the requirement is not yet understood.
- Do not proceed to Workflow 03 while blocking questions remain.

## 12. Reusable Execution Instructions

```text
Run AI-ENGINEERING-FOUNDATION/workflows/02-requirements-and-scope.md
acting as the Product Analyst (agents/product-analyst.md).
Input: [PROJECT IDEA OR CHANGE REQUEST]; discovery output: [LOCATION]

1. Define the problem and confirm it with me.
2. Identify actors and workflows, including failure paths.
3. Write numbered FRs, BRs, measurable NFRs, constraints, and assumptions.
   For existing systems, verify current behavior in the code first.
4. Write testable ACs for every FR.
5. State scope and explicit out-of-scope items; list risks and unresolved
   questions (blocking vs non-blocking).
6. Ask when a requirement is ambiguous; do not invent details.
7. Produce docs/project-specification.md from templates/project-specification.md
   and stop for my approval. Treat any later addition as a change request.
```
