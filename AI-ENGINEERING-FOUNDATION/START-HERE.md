# Start Here

The short version. Read `README.md` later if you want the full picture.

## Starting a new project

1. Copy the `AI-ENGINEERING-FOUNDATION/` folder into the new repository's root (or keep it nearby and give Claude Code the relevant files).
2. Copy `AI-ENGINEERING-FOUNDATION/CLAUDE.md` to the repository root as `CLAUDE.md`.
3. Open Claude Code in the repository.
4. Open `prompts/new-project.md`.
5. Replace `[PROJECT IDEA]` and the other placeholders with your project details.
6. Send the prompt to Claude Code.
7. Answer its questions and approve (or correct) the discovery summary, the specification, and the architecture before any code is written.
8. Approve implementation one milestone at a time.

## Working on an existing project

1. Copy the foundation and `CLAUDE.md` into the repository if they are not there. Merge with any existing `CLAUDE.md` rather than overwriting it.
2. Open Claude Code in the repository.
3. Use `prompts/existing-repository.md` the first time, or `prompts/continue-project.md` to resume.
4. Let Claude Code inspect the actual code before it proposes anything.
5. Confirm or correct the plan it proposes.
6. Continue with the task prompts below.

## Common tasks

| To... | Use |
| --- | --- |
| Implement a feature | `prompts/implement-feature.md` |
| Fix a bug | `prompts/investigate-bug.md` |
| Review code | `prompts/code-review.md` |
| Check security | `prompts/security-review.md` |
| Prepare for production | `prompts/production-readiness.md` |

The rest are listed in `README.md`.

## How a task moves through the foundation

1. **Pick a prompt** for the task (tables above and in `README.md`), fill in its context fields, and paste its instruction block.
2. **The prompt routes to workflows.** Claude Code follows the workflows the prompt names, scaled to the task's risk tier. You do not run all twelve for every task.
3. **Workflows assign roles.** Each workflow names the `agents/` roles involved. Claude Code performs them as roles, or through real subagents if you have configured them.
4. **Artifacts are written from templates** into the project's `docs/`: specification, architecture, ADRs, plan, status, and reports.
5. **Checklists close each stage.** A stage is done when its checklist is ticked with evidence, not when the work "looks done".
6. **Findings loop back.** Review, testing, and security findings go through remediation and reverification before the work counts as complete.
7. **Production readiness is the last gate.** `prompts/production-readiness.md` returns READY, READY WITH CONDITIONS, or NOT READY. Deploying is still your decision.

## Things to know

- **You do not paste the agent definitions.** Prompts reference the foundation files by path. Claude Code reads them from the repository.
- **Small tasks stay small.** Claude Code scales the process to risk. A typo fix gets a typo fix, not a security review.
- **You approve the big decisions.** Scope changes, major architecture choices, destructive operations, and production deployments always come back to you.
- **Results must have evidence.** If Claude Code says tests pass, it should show the command and output. If it could not run something, it should say so.
- **Agents are roles, not programs.** The `agents/` files describe how to perform a role. They do not run on their own. If you want real Claude Code subagents, create them using Claude Code's supported configuration (see the Claude Code documentation); the agent files can be converted into that format later. This foundation does not set that up for you.
- **Project records go in `docs/`.** Specification, architecture, decisions, and status are created from `templates/` inside the project, so the next session can pick up where the last one stopped.
