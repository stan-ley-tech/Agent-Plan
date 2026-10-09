# Prompt: Existing Repository

Use the first time you bring the foundation into an existing codebase.

```text
Task: Understand this existing repository and produce a project-specific
development plan. Do not change application code in this task.

Repository: [REPOSITORY URL, OR "THE CURRENTLY OPEN REPOSITORY"]
My goal for this project: [GOAL, e.g. "add billing", "stabilize and maintain", "take over development"]
Known context: [ANYTHING YOU ALREADY KNOW, OR "NONE"]

Context to read first:
- CLAUDE.md (and any existing project instructions it was merged with)
- AI-ENGINEERING-FOUNDATION/principles/engineering-standards.md
- AI-ENGINEERING-FOUNDATION/agents/engineering-orchestrator.md
- AI-ENGINEERING-FOUNDATION/agents/software-architect.md

If a URL is given, clone it locally. Do not push anything.

Process:
1. Existing instructions. Find and read any existing CLAUDE.md, AGENTS.md,
   CONTRIBUTING, README, docs/, ADRs, and CI configuration. Existing project
   rules take precedence over the foundation where they conflict; report
   any conflicts.
2. Inventory. Languages, frameworks, dependencies, entry points, modules,
   data stores, external integrations, build and test commands.
3. Architecture assessment (agents/software-architect.md). Map the actual
   structure from source code, citing files. Note where documentation and
   code disagree.
4. Current state. Run the build and tests if possible; report actual results.
   Note test coverage, failing tests, outdated or vulnerable dependencies
   (run the audit tool if available), obvious security concerns, and
   technical debt. Label each item with an evidence label.
5. Risks. Identify the riskiest areas: authentication, data handling,
   migrations, untested critical paths.
6. Plan. Propose a development plan for my goal: priorities, first milestone,
   approval checkpoints, and which foundation workflows apply.
7. Project records. Propose docs/project-status.md (templates/project-status.md)
   and, if missing, docs/architecture.md capturing the current architecture.
   Create them only after I confirm.

Quality and safety:
- Do not overwrite, reformat, or restructure existing work.
- Do not adopt foundation conventions that contradict established project
  conventions without asking.
- Never print secrets you encounter; report their location only.

Deliverables:
- Current-state report: inventory, architecture summary with file references,
  build/test results, risks, conflicts with existing instructions.
- Proposed development plan.

Verification:
- Every statement about the code cites files or command output.
- Build and test claims include the commands and their actual results.

Ask before creating or modifying any file, and before any action beyond
reading and running local, non-destructive commands.
```
