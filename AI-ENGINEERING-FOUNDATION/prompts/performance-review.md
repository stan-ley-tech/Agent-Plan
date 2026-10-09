# Prompt: Performance Review

```text
Task: Investigate the performance concern below and recommend focused,
evidence-based changes.

Concern: [SYMPTOM, e.g. "order list takes 8s with 50k orders"]
Target: [PERFORMANCE REQUIREMENT, OR "NONE STATED"]
Environment: [WHERE OBSERVED; DATA VOLUME]
Available measurements: [PROFILES, LOGS, METRICS, QUERY PLANS, OR "NONE"]

Context to read first:
- CLAUDE.md
- AI-ENGINEERING-FOUNDATION/agents/performance-engineer.md
- AI-ENGINEERING-FOUNDATION/principles/code-quality.md
  (premature optimization)

Process:
1. Restate the concern as a measurable symptom and target.
2. Inspect the code path end to end: entry point, data access, external calls,
   serialization.
3. Measure before changing anything, using tools available locally:
   profiler, timing, query plans, benchmarks with realistic data volume.
   If measurement is not possible, say so.
4. Identify the dominant cost. Common causes: N+1 queries, missing indexes,
   unbounded queries, repeated work in loops, synchronous external calls,
   excessive serialization.
5. Form and test hypotheses.
6. Recommend the smallest effective change. Prefer algorithmic and query
   fixes over caches or new infrastructure.
7. If I authorize implementation, implement, then measure again under the
   same conditions and run the relevant tests.

Quality and safety:
- Label each finding Verified (measured), Likely, or Unverified concern.
- Do not run load tests against production or shared environments.
- Do not add caching, queues, or infrastructure without architectural review.
- Do not trade correctness or readability for unmeasured gains.

Deliverables:
- Symptom and target, measurements and method, findings ranked by measured
  impact, recommendations, unverified concerns listed separately; and
  before/after measurements if implemented.

Verification:
- Improvement claims include before/after numbers under comparable conditions.

Ask me before implementing, and if measuring requires production access or
production-scale data.
```
