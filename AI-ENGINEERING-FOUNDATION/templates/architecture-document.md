# Architecture: [PROJECT NAME]

| | |
| --- | --- |
| Status | [Draft / Approved] |
| Last updated | [YYYY-MM-DD] |
| Specification | [LINK TO docs/project-specification.md] |

## 1. System overview

[What the system does and its main parts, in one paragraph. Include a simple diagram if it helps.]

```
[DIAGRAM: USERS → COMPONENTS → DATA STORES → EXTERNAL SERVICES]
```

## 2. Requirements and constraints that drive the architecture

| Driver | Source (FR/NFR/BR/constraint ID) | Architectural consequence |
| --- | --- | --- |
| [DRIVER] | [ID] | [CONSEQUENCE] |

## 3. Architecture decisions

| Decision | ADR | Status |
| --- | --- | --- |
| [DECISION] | [docs/adr/NNNN-title.md] | [Proposed / Accepted] |

## 4. Component responsibilities

| Component | Responsibility (one sentence) | Owns data | Depends on |
| --- | --- | --- | --- |
| [COMPONENT] | [RESPONSIBILITY] | [DATA] | [DEPENDENCIES] |

## 5. Data flow

### [PRIMARY WORKFLOW NAME]
1. [STEP: WHICH COMPONENT DOES WHAT WITH WHICH DATA]

## 6. Trust boundaries

| Boundary | Crosses from → to | Controls at boundary |
| --- | --- | --- |
| [BOUNDARY] | [FROM → TO] | [AUTHENTICATION / VALIDATION / ENCRYPTION] |

## 7. External integrations

| Service | Purpose | Protocol | Failure behavior | Owner of credentials |
| --- | --- | --- | --- | --- |
| [SERVICE] | [PURPOSE] | [PROTOCOL] | [WHAT HAPPENS WHEN IT FAILS] | [WHO] |

## 8. Failure modes

| Failure | Detection | Impact | Handling |
| --- | --- | --- | --- |
| [FAILURE] | [HOW WE KNOW] | [BLAST RADIUS] | [RESPONSE] |

## 9. Operational considerations

- Environments: [LIST]
- Deployment model: [DESCRIPTION]
- Observability: [LOGS / METRICS / HEALTH CHECKS]
- Backup and recovery: [APPROACH]
- Expected scale: [CURRENT AND NEAR-TERM]

## 10. Alternatives considered

| Alternative | Why not chosen |
| --- | --- |
| [ALTERNATIVE] | [REASON] |

## 11. Unresolved decisions

| Decision | Options | Needed by | Owner |
| --- | --- | --- | --- |
| [DECISION] | [OPTIONS] | [MILESTONE] | [WHO] |
