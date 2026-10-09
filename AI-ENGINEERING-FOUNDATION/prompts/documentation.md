# Prompt: Documentation

```text
Task: Bring documentation in line with the actual implementation for the
scope below.

Scope: [CHANGE / FEATURE / WHOLE REPOSITORY]
Audience: [DEVELOPERS / OPERATORS / API CONSUMERS / END USERS]
Documents to focus on: [SPECIFIC FILES, OR "ALL AFFECTED"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/documentation-engineer.md
- AI-ENGINEERING-FOUNDATION/workflows/10-documentation.md

Process:
1. Identify affected documents: README, setup, configuration reference, API
   reference, architecture, ADRs, runbooks, troubleshooting, changelog,
   docs/project-status.md.
2. For each, read the code, configuration, and scripts it describes.
3. List discrepancies between documentation and actual behavior.
4. Update documentation to match actual behavior. Remove content describing
   behavior that no longer exists.
5. Run documented setup and usage commands where safe; record results.
6. Check links and file paths.

Quality and safety:
- Do not document unimplemented features or unsupported behavior as existing.
  Label planned items as planned, or omit them.
- One fact in one place; link instead of duplicating.
- Do not restate what the code makes obvious.
- Use placeholders in examples; never real secrets, hosts, or personal data.
- Do not change code to match documentation; report mismatches.

Deliverables:
- Updated documents; a list of discrepancies found and how each was resolved;
  commands verified; items that could not be verified.

Verification:
- Every changed statement was checked against code or by running it.

Ask me when code and specification disagree and the intended behavior is
unclear.
```
