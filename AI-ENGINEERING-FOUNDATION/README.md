# AI Engineering Foundation

A reusable set of Markdown documents that tells Claude Code how to approach software work: the principles to follow, the specialist roles to adopt, the workflows to run, the prompts to start from, and the templates and checklists to produce consistent records.

New here? Read [START-HERE.md](START-HERE.md).

## What it is

- Permanent engineering instructions (`CLAUDE.md`).
- Engineering principles that apply to every project (`principles/`).
- Thirteen specialist role definitions (`agents/`).
- Twelve sequential workflows from discovery to production readiness (`workflows/`).
- Fourteen ready-to-use task prompts (`prompts/`).
- Document templates (`templates/`) and short verification checklists (`checklists/`).

It is language-, framework-, and industry-neutral. Project specifics come from the project, not from the foundation.

## What it is not

- Not a software product, platform, service, or framework.
- Not an agent runtime. Writing an agent document does not create an executable agent, start a background task, run a scanner, or deploy anything.
- Not a substitute for engineering judgment. Checklists catch omissions; they do not make decisions.
- Not a mandate to run every workflow on every task. The process scales with risk (see the risk tiers in `principles/engineering-standards.md`).

## How the documents fit together

```
CLAUDE.md                 always-on rules; points to everything else
  │
  ├── principles/         the standards every decision is judged against
  ├── workflows/          what to do, in order, for each phase
  │     └── names the agents/ to use in each step
  ├── agents/             how each specialist role thinks, works, and reports
  ├── templates/          the shape of the documents workflows produce
  ├── checklists/         a final pass to catch omissions
  └── prompts/            what you paste into Claude Code to start a task;
                          each prompt references the workflows and principles
```

Paths such as `workflows/06-implementation.md` are relative to the foundation folder. Paths starting with `docs/` refer to the project's own documents.

A prompt starts a task. The prompt names the workflows. Workflows name the agent roles and the templates. Agents apply the principles. Checklists close each phase.

## Agent roles vs. Claude Code subagents

The files in `agents/` are role instructions. They can be used in three ways:

1. **Single session, role switching.** Claude Code performs the role itself, in a separate, clearly labeled pass. This works everywhere. For independent review, start the review pass from the diff, not from the implementer's summary, and preferably in a fresh session.
2. **Delegation through available tools.** If the environment supports delegating to subagents, paste the role's instruction block (section 12 of each agent file) into the delegated task.
3. **Configured subagents.** Claude Code supports project-defined subagents using its own file conventions (currently Markdown files with frontmatter under `.claude/agents/`; check the Claude Code documentation for the current format). The agent documents can be converted into that format later. This foundation does not create that configuration.

Whichever you use, Claude Code must use only the capabilities actually present in the environment and must say which it used.

## Using it with Claude Code

1. Copy `AI-ENGINEERING-FOUNDATION/` into the root of the target repository.
2. Copy `AI-ENGINEERING-FOUNDATION/CLAUDE.md` to the repository root as `CLAUDE.md`. If the repository already has one, merge: keep project-specific content and add the foundation rules.
3. Open Claude Code in the repository.
4. Pick a prompt from `prompts/`, replace its placeholders, and send it.

## What to copy into each project

| Copy | Why |
| --- | --- |
| Whole `AI-ENGINEERING-FOUNDATION/` folder | Simplest; prompts and workflows reference each other. Recommended. |
| `CLAUDE.md` at repository root | Required. Claude Code reads it automatically. |
| Minimum viable set | `CLAUDE.md`, `principles/`, `workflows/`, `agents/`. Prompts can be pasted from this master copy. |

Project-specific outputs (specification, architecture, ADRs, status, reports) go in the project's `docs/` folder, created from `templates/`. Do not edit the copied foundation to record project facts.

## Which prompt to use

| Situation | Prompt |
| --- | --- |
| Starting from an idea | `prompts/new-project.md` |
| First time in an existing codebase | `prompts/existing-repository.md` |
| Resuming previous work | `prompts/continue-project.md` |
| Building a feature | `prompts/implement-feature.md` |
| Fixing a defect | `prompts/investigate-bug.md` |
| Improving structure without changing behavior | `prompts/refactor-code.md` |
| Designing or changing a schema | `prompts/design-database.md` |
| Designing or changing an API | `prompts/design-api.md` |
| Security assessment | `prompts/security-review.md` |
| Reviewing a change | `prompts/code-review.md` |
| Running and assessing tests | `prompts/test-and-verify.md` |
| Investigating speed or resource use | `prompts/performance-review.md` |
| Updating docs | `prompts/documentation.md` |
| Deciding whether a release can ship | `prompts/production-readiness.md` |

## Updating the foundation

Keep one master copy (this repository). Improve it here, then copy updates into projects.

- **Definitions live in one place.** Risk tiers, evidence labels, and severity levels are defined only in `principles/engineering-standards.md`. Approval requirements are defined in `CLAUDE.md`. Other documents reference them; do not restate them differently.
- **Change names everywhere at once.** If you rename or move a file, search all documents for references and update them in the same change.
- **Keep the role boundaries distinct.** When adding responsibility to one agent, check it does not duplicate another agent's responsibility.
- **Keep it neutral.** Stack-specific guidance belongs in the project's own `CLAUDE.md`, not here.
- **Version it.** Tag releases of this repository so projects can record which foundation version they copied.

## Deviations from the original specification

- A short `README.md` at the repository root points to this folder so the repository is navigable on GitHub. It is not part of the foundation and need not be copied.
- `CLAUDE.md` includes a "Foundation location" line so references resolve after the folder is copied into another repository.
