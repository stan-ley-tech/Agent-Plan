# Engineering Decision-Making

How to choose between alternatives, and when to write it down.

## When this applies

Use this process for **significant decisions**: those that are expensive to reverse, affect several components or teams, introduce a new technology, change a public contract, or shape security and data handling.

Do not use it for trivial choices: naming a local variable, choosing between two equivalent standard-library functions, formatting. Make those choices and move on.

## Evaluation criteria

For each significant decision, evaluate at least two realistic options (one is often "keep what exists" or "do the simplest thing") against:

| Criterion | Question |
| --- | --- |
| **Requirements** | Which stated requirements does each option satisfy, and how well? |
| **Constraints** | Does it fit budget, timeline, team skills, platform, regulation, existing systems? |
| **Complexity** | How many new concepts, components, and failure points does it add? |
| **Security** | What attack surface, data exposure, or privilege does it introduce? |
| **Operational burden** | What must someone run, monitor, upgrade, and be paged for? |
| **Cost** | Build cost, run cost, licensing, and the cost of the people to maintain it. |
| **Maintainability** | Can a new engineer understand and safely change it? |
| **Failure modes** | How does it fail, how visible is the failure, and what is the blast radius? |
| **Reversibility** | If wrong, how hard is it to undo? What would be lost? |
| **Future change** | Which likely changes does it make easy or hard? Only consider changes with real evidence, not speculation. |

Not every criterion matters equally for every decision. Say which ones dominate and why.

## Procedure

1. **State the decision** as a question: "How should background jobs be executed?"
2. **State the drivers**: the requirements and constraints that make this decision necessary now.
3. **List options**, including the simplest viable one.
4. **Evaluate** each option against the relevant criteria. Be concrete; cite requirements and evidence.
5. **Decide**, or present a recommendation to the user if the decision is consequential.
6. **Record** the decision if it meets the ADR threshold below.
7. **Define revisit conditions**: what evidence would make you reconsider.

## Bias checks

- Prefer what the project already uses unless it fails a requirement.
- Distrust options chosen because they are fashionable, familiar, or "more scalable" without a scale requirement.
- Distrust options that solve problems the project does not have.
- If every option looks bad, the problem statement may be wrong. Revisit the requirements.

## Architecture decision records

Write an ADR (`templates/architecture-decision-record.md`, stored as `docs/adr/NNNN-short-title.md`) when a decision:

- Selects or replaces a framework, language, database, hosting platform, or major dependency.
- Defines a system boundary, service split, or integration pattern.
- Sets a data ownership, consistency, or retention approach.
- Establishes a security model (authentication approach, tenancy isolation, secret handling).
- Accepts a significant known risk or technical debt.
- Reverses a previous ADR.

ADRs are short: one to two pages. They record context and reasoning, not implementation detail.

ADRs are immutable once accepted. To change a decision, write a new ADR that supersedes the old one and update the old one's status.

## Who decides

- The engineering roles **recommend**. The user **approves** consequential decisions (anything warranting an ADR, and anything listed under "Safety and human authority" in `CLAUDE.md`).
- When specialist roles disagree, the orchestrator records both positions, the trade-off, and its recommendation, then asks the user if the decision is consequential.
