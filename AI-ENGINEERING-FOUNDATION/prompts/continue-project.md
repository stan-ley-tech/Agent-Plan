# Prompt: Continue Project

Use at the start of a session to resume work.

```text
Task: Resume work on this project. Establish the true current state, then
propose the next step.

Focus for this session: [FOCUS, OR "WHATEVER IS NEXT"]

Context to read first:
- CLAUDE.md
- docs/project-status.md, docs/implementation-plan.md, docs/project-specification.md,
  docs/architecture.md, and recent ADRs and reports in docs/ (whichever exist)
- AI-ENGINEERING-FOUNDATION/agents/engineering-orchestrator.md

Process:
1. Read the project documents above.
2. Verify against the repository. Do not trust notes blindly:
   - Check recent version-control history and the current branch.
   - Check for uncommitted changes and report them without discarding them.
   - Run the build and tests; report actual results.
   - Confirm that work marked complete actually exists in the code.
3. Reconcile. List where the documents and the repository disagree.
4. Summarize:
   - Completed work (verified in code).
   - Work reported complete but not verified.
   - In-progress work.
   - Pending tasks.
   - Blockers and open findings.
5. Propose the next appropriate step, the workflow it belongs to, and its
   risk tier. If the next step is at an approval checkpoint, say so.
6. Offer to update docs/project-status.md to reflect the verified state.

Quality and safety:
- Do not discard, reset, or overwrite uncommitted work.
- Do not begin the next task until I confirm.

Deliverables:
- Verified status summary, discrepancies, and a proposed next step.

Verification:
- Each "completed" item cites the commit, file, or test that proves it.

Ask me if the documents and repository disagree on something that affects
what to do next.
```
