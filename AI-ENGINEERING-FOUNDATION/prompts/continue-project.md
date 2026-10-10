# Prompt: Continue Project

> **How to use:** fill in the context fields in section 4 and paste the block at the start of a session. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** state verification first; then whichever workflow the next step belongs to.

## 1. Purpose

Resume work on a project by establishing its true current state, from the repository rather than from notes, and identifying the next appropriate step without duplicating or skipping work.

## 2. When to Use

Use at the start of any session on a project that already has project records (`docs/project-status.md`, plan, specification) or recent work.

Use something else when:

- You have never worked in the repository and there are no project records → `existing-repository.md`.
- You already know the exact next task and the state is fresh → the task's own prompt.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Immediate objective | What you want from this session, or "whatever is next" | |
| Recent context | Anything done outside the repository since the last session (decisions, meetings, incidents) | Optional. |
| Branch | If work should continue on a specific branch | Optional; the AI will check the current one. |

Do not restate what was completed; the AI must verify it.

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/continue-project.md
(sections 5–8), acting as the Engineering Orchestrator
(agents/engineering-orchestrator.md).

Immediate objective: [OBJECTIVE, OR "WHATEVER IS NEXT"]
Recent context: [CONTEXT, OR "NONE"]
Branch: [BRANCH, OR "CURRENT"]

Rules:
- Treat project notes as claims to verify, not facts. Confirm completed work
  exists in the code and its tests pass before relying on it.
- Do not discard, reset, stash, or overwrite uncommitted or unpushed work.
  Report it.
- Check whether the objective is already partly or fully implemented before
  planning new work, to avoid duplicate implementation.
- Label each item Verified, Reported (claimed but not verified), or Unknown.
- Do not start the next task until I confirm it.
```

## 5. Execution Sequence

1. **Read project records**: `docs/project-status.md`, `docs/implementation-plan.md`, specification, architecture, recent ADRs, reports in `docs/reviews/`.
2. **Inspect repository state**: current branch, uncommitted changes, unpushed commits, worktrees where relevant, recent commit history since the status file's "last verified commit".
3. **Run tests and checks**; record results.
4. **Verify claims**: for each item recorded as complete, confirm the code and tests exist and pass. For each open finding, check its current state.
5. **Reconcile**: list discrepancies between records and repository.
6. **Check the objective** against existing code: already implemented, partly implemented, or not started.
7. **Determine the next step**: the workflow it belongs to, its risk tier, and whether it sits at an approval checkpoint.
8. **Report** and stop. Offer to update `docs/project-status.md`.

## 6. Expected Output

- Repository state: branch, uncommitted/unpushed work, recent changes.
- Test and check results with commands.
- Status table: Completed (Verified, with commit/test evidence) · Reported but not verified · In progress · Pending · Blocked.
- Open findings and known issues with current state.
- Discrepancies between records and repository.
- Proposed next step with workflow, risk tier, and checkpoint status.

## 7. Completion Criteria

- Every "completed" item is either Verified with evidence or reclassified.
- Repository state and test results are recorded from this session.
- Discrepancies are listed.
- The next step is identified and the user has confirmed it before work begins.

## 8. Stop / Escalation Conditions

Stop and ask when:

- Records and repository disagree in a way that changes what to do next.
- Uncommitted or unpushed work exists whose purpose is unclear.
- Tests fail in areas recorded as complete.
- The objective conflicts with the approved plan or scope (route through Workflow 02 as a change request).
- The next step is at an approval checkpoint.
