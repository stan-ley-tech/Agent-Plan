# Workflow 10 — Documentation

## Purpose

Keep documentation consistent with what the code actually does after any change that affects setup, configuration, interfaces, architecture, or operations.

## When to invoke

- After implementation changes that affect users, developers, operators, or API consumers.
- When onboarding to a repository with missing or stale documentation.
- Before a release (as part of Workflow 12).

## Required inputs

- The change (diff) or area to document.
- The actual code, configuration, and scripts.
- Existing documentation.

## Relevant agents

- **Documentation Engineer** — leads.
- The role responsible for the changed area — consulted for accuracy.

## Steps

1. Identify affected documents: README, setup guide, configuration reference, API reference, architecture document, ADRs, runbooks, changelog, `docs/project-status.md`.
2. Read the code and configuration that each document describes.
3. Update each document to match actual behavior. Remove content for removed behavior.
4. Run documented commands where safe and practical; record results.
5. Label any planned or unimplemented behavior as such, or omit it.
6. Check links and file paths.
7. Update `docs/project-status.md` with the current state.

## Deliverables

- Updated documentation.
- List of discrepancies found and resolved, and steps not verified.

## Verification criteria

- Every changed statement was checked against code or by execution.
- No secrets, real hostnames, or personal data in examples.
- No duplicate copies of the same fact across documents.

## Completion criteria

- Affected documents reflect the current implementation.

## Escalation conditions

- Code and specification disagree and the correct behavior is unclear.
- Operational procedures cannot be verified without production access.

## Stop conditions

- Stop rather than document behavior you cannot confirm exists.
