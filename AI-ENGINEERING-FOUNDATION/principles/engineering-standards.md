# Engineering Standards

The standards every piece of work is judged against. This file is also the single source for three shared definitions used across the foundation: **risk tiers**, **evidence labels**, and **severity levels**.

---

## Shared definitions

### Risk tiers

Scale the process to the risk. The orchestrator assigns a tier at the start of each task and may raise it if investigation reveals more risk.

| Tier | Typical work | Minimum process |
| --- | --- | --- |
| **0 — Trivial** | Typo, comment, copy text, formatting, a dependency patch bump with no behavior change | Make the change. Run the fastest relevant check. No specialist roles. |
| **1 — Standard** | Contained bug fix, small feature inside an existing module, test additions | Workflow 06 and 07. Self-review against `checklists/implementation.md`. Independent review recommended. |
| **2 — Significant** | New feature spanning modules, schema change, new API endpoint, new dependency, behavior change visible to users or clients | Requirements confirmed. Data/API design where relevant. Workflows 06–09. Independent code review required. Security review if any trust boundary is touched. |
| **3 — High risk** | Authentication, authorization, payments, personal or regulated data, cryptography, destructive migrations, multi-tenant isolation, infrastructure or production configuration | Full design (02–05) with approval. Independent security assessment and code review required. Release readiness (12) before shipping. User approval at each checkpoint. |

When unsure between two tiers, choose the higher one and say why.

### Evidence labels

Every finding, claim, and status report uses one of these labels.

| Label | Meaning |
| --- | --- |
| **Verified** | Confirmed by evidence produced or inspected in this session: command output, a test result, a reproduced failure, a specific line of code read. Cite the evidence. |
| **Likely** | Strong indication from code reading or partial evidence, but not reproduced or executed. |
| **Unverified concern** | Plausible risk without direct evidence. Worth checking; not established. |
| **Recommendation** | A suggested improvement, not a defect. |
| **Open question** | Information that is missing and needed to decide. |

Never present a Likely or Unverified item as Verified. "Tests pass" without command output is unverified.

### Severity levels

Used for review, security, and release findings.

| Severity | Meaning | Default handling |
| --- | --- | --- |
| **Critical** | Data loss or corruption, security breach with realistic exploitation, production outage, legal or regulatory exposure. | Blocks merge and release. |
| **High** | Incorrect behavior in a main path, significant security weakness, breaking change without migration path. | Blocks merge unless the user explicitly accepts the risk. |
| **Medium** | Incorrect behavior in an edge path, missing validation with limited impact, maintainability problem likely to cause defects. | Fix before release or record as accepted debt. |
| **Low** | Minor defect, small inconsistency, missing test for an unlikely path. | Fix when convenient. |
| **Info** | Observation or suggestion with no defect. | Optional. |

Severity reflects realistic impact and likelihood in this project's context, not worst-case theory.

---

## Requirements-driven development

- Every change traces to a requirement, a confirmed defect, or an approved improvement. If you cannot name which, stop and ask.
- Acceptance criteria are written before implementation for Tier 2 and above.
- Do not add features, options, or configuration nobody asked for.
- When a requirement is ambiguous, ask. When it is merely incomplete, state the assumption you are making and proceed.

## Domain understanding

- Use the domain's own vocabulary in code, data models, and documentation.
- Model real business rules explicitly rather than burying them in conditionals spread across layers.
- Before designing, identify the core entities, their lifecycle, who acts on them, and which invariants must always hold.
- Generic designs (a "manager", a "processor", a "generic entity service") are a sign that the domain has not been understood.

## Architectural simplicity

- Start with the simplest structure that meets the known requirements: usually one deployable unit, one database, clear internal modules.
- Add a component, service, queue, cache, or framework only when a stated requirement needs it.
- Each component has one clear responsibility that can be described in a sentence.
- Prefer boring, well-understood technology unless a requirement justifies otherwise.

## Maintainability

- Optimize for the next engineer reading the code, including a future AI session with no memory of this one.
- Keep changes small and reviewable.
- Code that is hard to test is usually hard to maintain; treat that as a design signal.

## Error handling

- Decide for each failure: recover, retry, translate, or propagate. Do not swallow errors.
- Errors crossing a boundary (API, UI, process) are translated into a stable, documented form without leaking internals.
- Fail fast on programmer errors and invalid configuration at startup.
- Partial failures in multi-step operations must leave data consistent (transactions, compensation, or idempotent retries).

## Observability

- Log events that an operator would need to diagnose a problem: what happened, to which resource, with which correlation identifier. Never log secrets or unnecessary personal data.
- Expose health information for anything that is deployed.
- Add metrics or tracing in proportion to the system's operational importance, not by default.

## Data integrity

- Enforce invariants at the lowest reliable layer, usually the database (constraints, foreign keys, unique indexes), and validate earlier for good error messages.
- Every write path considers concurrency: what happens if two requests do this at once?
- Destructive data operations require a backup or rollback strategy and user approval.

## Backward compatibility

- Identify consumers of anything you change: APIs, schemas, file formats, configuration, events, CLIs.
- Breaking changes need an explicit decision, a migration path, and user approval.
- Prefer additive change, then deprecation, then removal.

## Testing

- Tests prove the acceptance criteria and protect against regression.
- Test behavior, not implementation details.
- Every bug fix includes a test that fails without the fix, where practical.
- A test that is flaky is a defect. Fix it or quarantine it with a recorded reason; do not ignore it.
- Do not weaken assertions, add skips, or mock away the behavior under test to make a test pass.

## Documentation

- Document what a reader cannot quickly infer from the code: purpose, setup, configuration, decisions, operations.
- Documentation describes what exists. Planned behavior is labeled as planned.
- Update documentation in the same change as the behavior it describes.

## Technical debt

- Debt is acceptable when it is deliberate, recorded, and has a known cost.
- Record deliberate debt in `docs/project-status.md` (Known limitations) with the reason and the trigger for repaying it.
- Do not repay unrelated debt inside a feature change; propose it separately.

## Dependency management

- Add a dependency only when it removes meaningful effort or risk compared with writing the code.
- Before adding one, check: maintenance activity, license compatibility, known vulnerabilities, transitive weight, and whether the project already has something equivalent.
- Pin or lock versions using the ecosystem's standard mechanism.
- New major dependencies (frameworks, databases, platforms) require user approval.

## Engineering trade-offs

- Every significant choice has costs. Name them.
- Use `principles/engineering-decision-making.md` for decisions with long-term consequences.
- Prefer reversible decisions; spend more care on irreversible ones.
