# Workflow 02 — Requirements and Scope

## Purpose

Turn the approved project concept into testable requirements with clear scope, so that design and implementation have a fixed target.

## When to invoke

- After Workflow 01 is approved.
- Before implementing any Tier 2+ feature that lacks written acceptance criteria.

## Required inputs

- Approved discovery summary.
- Existing specification, if any.
- User availability to answer questions.

## Relevant agents

- **Product Analyst** — leads.
- **Security Engineer** — consulted for security and privacy requirements when sensitive data or trust boundaries are involved.
- **Engineering Orchestrator** — confirms the risk tier.

## Steps

1. Write the user workflows: for each user type, the steps to reach their goal, including failure and cancellation paths.
2. Derive functional requirements (FR-n) from the workflows.
3. Identify business rules (BR-n) and invariants.
4. Identify nonfunctional requirements (NFR-n) that actually matter: performance, availability, security, privacy, accessibility, compliance, platforms. Make each measurable or remove it.
5. Write acceptance criteria (AC-n) for each functional requirement, phrased so they can be tested.
6. List non-goals explicitly.
7. List constraints.
8. List unresolved decisions with their impact and the person who decides.
9. Label each item Stated, Assumed, or Open question.
10. Record the result in `docs/project-specification.md` using `templates/project-specification.md`.

## Deliverables

- `docs/project-specification.md`.

## Verification criteria

- Every functional requirement has at least one acceptance criterion.
- Every acceptance criterion is testable.
- No requirement is untraceable to the user, existing documents, or observed behavior.
- Assumptions are visible.

## Completion criteria

- The user approves the specification. **This is an approval checkpoint.** Scope changes after this point require user approval.

## Escalation conditions

- Requirements conflict with each other or with constraints.
- Requirements imply regulatory obligations not yet addressed.
- The user wants to add scope that would materially change timeline or risk.

## Stop conditions

- Stop if blocking open questions remain unanswered.
- Stop if acceptance criteria cannot be written for a core requirement; it is not yet understood.
