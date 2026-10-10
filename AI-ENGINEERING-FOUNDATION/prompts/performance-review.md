# Prompt: Performance Review

> **How to use:** fill in the context fields in section 4 and paste the block into your AI coding agent. If the foundation folder is not in the repository, paste this entire file instead.
> **Workflows:** investigation per `agents/performance-engineer.md`; any approved change follows 06 → 07 (with before/after measurement) → 08.

## 1. Purpose

Establish whether a real performance problem exists, find its dominant cause through measurement, and recommend (or, if authorized, make) the smallest change that fixes it — proven by before/after numbers.

## 2. When to Use

Use for reported slowness, timeouts, high CPU or memory, connection exhaustion, high cost, or before release when NFRs set performance targets.

Use something else when:

- The problem is incorrect results → `investigate-bug.md`.
- The problem is a schema design flaw → `design-database.md`.

## 3. Required Context

| Field | Provide | Notes |
| --- | --- | --- |
| Symptom | Which operation, how slow or heavy, under what load | e.g. "order list takes 8s with 50k orders". |
| Target | The performance requirement, if one exists | "None stated" is acceptable. |
| Environment | Where observed; data volume | |
| Measurements | Profiles, traces, metrics, logs, query plans | If available. |
| Authorization to change | Whether the AI may implement fixes | Default: recommend only. |

## 4. Instructions to the AI

```text
Read CLAUDE.md, then follow AI-ENGINEERING-FOUNDATION/prompts/performance-review.md
(sections 5–8) acting as the Performance Engineer
(agents/performance-engineer.md).

Symptom: [SYMPTOM]
Target: [REQUIREMENT, OR "NONE STATED"]
Environment: [WHERE; DATA VOLUME]
Measurements: [AVAILABLE DATA, OR "NONE"]
Authorization to change: [RECOMMEND ONLY / MAY IMPLEMENT]

Rules:
- Establish the problem and measure before optimizing. If measurement is not
  possible, say so and label findings accordingly.
- Label every finding Verified (measured), Likely, or Unverified concern.
- Target the dominant measured cost. No speculative or premature optimization.
- Prefer algorithmic and query fixes over caching or new infrastructure;
  caching needs a measured need and an invalidation strategy.
- Do not trade correctness or readability for unmeasured gains.
- Do not load-test production or shared environments.
- Any improvement claim needs before/after numbers under the same conditions.
```

## 5. Execution Sequence

1. **Establish the problem** as a measurable symptom and target.
2. **Inspect** the code path end to end: entry point, data access, network calls, serialization.
3. **Measure the baseline** with available tools (profiler, timing, query plans, benchmarks at realistic volume).
4. **Identify bottlenecks**, examining as relevant:
   - database queries (N+1, missing indexes, unbounded result sets, plans);
   - network calls (sequential calls, missing timeouts, chatty integrations);
   - CPU and memory behavior (hot loops, allocations, leaks);
   - algorithmic complexity;
   - concurrency (contention, locks, pool sizing);
   - caching (absent where clearly needed, or present and ineffective).
5. **Test hypotheses** against measurements; identify the dominant cost.
6. **Recommend** the smallest effective change with expected impact.
7. **If authorized, implement** (Workflow 06), run relevant tests, and **measure again** under the same conditions.
8. **Report.**

## 6. Expected Output

- Symptom and target.
- Measurement method, environment, and baseline results.
- Findings ranked by measured impact, each with evidence label and location.
- Recommendations with expected effect and trade-offs.
- If implemented: changed files, test results, before/after measurements under comparable conditions.
- Unverified concerns listed separately.

## 7. Completion Criteria

- The problem is defined measurably and a baseline is recorded (or the inability to measure is stated).
- The dominant cost is identified with evidence.
- Recommendations target that cost.
- If implemented: before/after numbers show the improvement, and correctness tests pass.

## 8. Stop / Escalation Conditions

Stop and ask when:

- The problem cannot be reproduced or measured, and any change would be speculative.
- Measuring requires production access or production-scale real data.
- The fix requires new infrastructure (cache, queue, service) or a significant dependency → Workflow 03.
- The fix would change behavior or correctness.
- The performance problem is also a denial-of-service risk → involve the Security Engineer.
