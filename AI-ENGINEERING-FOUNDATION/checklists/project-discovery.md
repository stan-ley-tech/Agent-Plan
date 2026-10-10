# Checklist: Project Discovery

Gate for `workflows/01-project-discovery.md`. Use at the end of discovery, before requirements or implementation work.

**Rules:** tick `[x]` only when you can point to evidence (file path, command output, or report section). Mark items that do not apply `N/A — reason`. Anything left unticked must appear under Final Status. A checklist does not replace judgment.

## Required — Repository

- [ ] Repository identified (path or URL, branch, commit)
- [ ] Existing instructions read (`CLAUDE.md`, `AGENTS.md`, README, CONTRIBUTING, `docs/`)
- [ ] Structure inspected
- [ ] Entry points identified (servers, routes, CLIs, workers, scheduled jobs, consumers)
- [ ] Build/run process identified
- [ ] Configuration sources identified
- [ ] Environment variables identified (secret *locations* only, never values)
- [ ] Dependencies identified from manifests and lockfiles

## Required — Architecture

- [ ] Architecture understood from the code, not only from documentation
- [ ] Major components identified
- [ ] Service boundaries identified
- [ ] Data flow understood (at least one primary workflow traced end to end)
- [ ] External integrations identified

## Conditional — Data (if the project persists data)

- [ ] Database identified (engine, version)
- [ ] Schemas/models inspected
- [ ] Migrations inspected
- [ ] Important queries identified

## Conditional — APIs (if the project exposes or calls interfaces)

- [ ] API entry points identified
- [ ] External APIs identified
- [ ] Authentication mechanisms identified
- [ ] Contracts understood (request, response, error conventions)

## Required — Testing

- [ ] Existing tests identified
- [ ] Test execution understood (commands)
- [ ] Baseline run and results recorded, or reason it could not be run
- [ ] Known gaps identified (untested critical paths)

## Conditional — Operations (if the project is deployed)

- [ ] Deployment process identified
- [ ] Infrastructure identified from evidence (not assumed)
- [ ] Logging identified
- [ ] Monitoring identified
- [ ] Backup/recovery identified where applicable

## Required — Risks

- [ ] Technical debt identified
- [ ] Security concerns identified (including any committed secrets — reported, not printed)
- [ ] Documentation compared with code; contradictions listed
- [ ] Unknowns documented as open questions
- [ ] Assumptions documented and labeled

## Conditional — Track B (new project, no code)

- [ ] Idea, intended users, and desired outcome recorded as stated
- [ ] Existing material and systems to integrate with collected
- [ ] Constraints recorded (budget, timeline, technology, hosting, regulation)
- [ ] Expected data sensitivity recorded
- [ ] Unknowns and feasibility risks recorded

## Verification

- [ ] Every claim about the system cites a file or command output
- [ ] Findings carry evidence labels (Verified / Likely / Unverified concern / Open question)
- [ ] Areas not inspected are listed
- [ ] Version control shows no changes to code or configuration

## Final Discovery Gate

- [ ] Initial risk tier assigned and justified
- [ ] Next workflow recommended
- [ ] **The system is sufficiently understood for the stated goal, and the user has reviewed the discovery report. Implementation must not begin until this is ticked.**

**Final Status**

```text
Gate passed: YES / NO
Unticked items and reasons:
Blocking unknowns:
Evidence location (report):
```
