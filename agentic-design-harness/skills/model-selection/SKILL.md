---
name: model-selection
description: Benchmark-aware model selection — score models by task types from business flow, KPI profile, compliance constraints, plus compute/cost estimates and online architecture recommendations. Use as Step 4.
compatibility: Offline. Read references/model-catalog, benchmark-matrix, compute-sizing, cost-model.
metadata:
  harness: agentic-design-harness
  step: 4
  version: "1.0.0"
---

# Model Selection (Benchmark-Aware, Multi-Model)

## Purpose

E2E section **2a** — select **all** models required for the solution, not one LLM only:

| Role | Examples |
|------|----------|
| Primary reasoning | Frontier / strong tier |
| Economy / routing | Small classifier |
| Embeddings | For RAG (if Step 6 requires) |
| Vision / multimodal | If K08 high |
| Guardrail classifier | T4 micro model |

**Rules:**
- Use **trusted sources** only — see `references/trusted-sources/TRUSTED-SOURCES.md`; use WebSearch for vendor docs / benchmark sites when offline catalog is stale
- **Ask the user** if workload tokens/day, GPU budget, or approved vendors are unknown
- Map **open-weight vs enterprise** with cost for self-host (GPU) vs API (tokens)

## Prerequisites

- Flow (Step 1) — must include `task_profile`, `scenarios`, `regulatory_compliance`, `region_network`
- Pattern (Step 2)
- KPI profile (Step 3)
- Read:
  - `references/benchmark-matrix/BENCHMARK-MATRIX.yaml`
  - `references/model-catalog/MODEL-CATALOG.yaml`
  - `references/compute-sizing/COMPUTE-SIZING.md`
  - `references/cost-model/COST-MODEL.yaml`

---

## Selection Pipeline

### Phase A — Compliance Pre-Filter

Apply filters from `BENCHMARK-MATRIX.yaml` → `compliance_filters` **before** scoring.

```
FUNCTION applyComplianceFilters(flow, candidates):

  IF flow.regulatory_compliance.approved_vendors == "self_hosted_only"
     OR flow.region_network.network_topology == "air_gapped":
    candidates = candidates WHERE hosting includes self_hosted
    IF candidates.empty: ERROR "No compliant model — revisit constraints"

  IF flow.regulatory_compliance.model_logging_prohibited:
    ELIMINATE api models UNLESS enterprise zero-retention confirmed
    NOTE in output: "Verify ZDR / enterprise agreement"

  IF flow.regulatory_compliance.data_classification IN [phi, pci, regulated]:
    PENALIZE api models score × 0.6 UNLESS private_endpoints_only
    BOOST self_hosted models score × 1.15

  IF flow.region_network.data_residency_required:
    FOR EACH api model: NOTE "Requires regional deployment (Azure OpenAI EU, Bedrock EU, etc.)"
    IF no regional option: PENALIZE api × 0.5

  RETURN candidates
```

### Phase B — Benchmark Score (from business flow)

Derive task weights from flow steps and scenarios:

```
FUNCTION computeTaskWeights(flow):
  task_weights = {}

  FOR EACH step IN flow.steps:
    FOR EACH task_type IN step.task_types:
      task_weights[task_type] += 1

  // Boost tasks appearing in rainy day scenarios (agent must handle edges)
  FOR EACH scenario IN flow.scenarios.rainy_day:
    IF scenario.severity IN [high, critical]:
      INFER affected_task_types from scenario.desired_agent_behavior
      FOR EACH t: task_weights[t] += 0.5

  NORMALIZE task_weights to sum = 1.0
  RETURN task_weights
```

```
FUNCTION benchmarkScore(model_id, task_weights):
  score = 0
  FOR EACH (task_type, weight) IN task_weights:
    task_score = BENCHMARK-MATRIX.task_types[task_type].model_scores[model_id]
    IF task_score is null: task_score = 0.3  // unknown — conservative
    score += weight × task_score
  RETURN score
```

Present benchmark rationale table to user:

| Task Type | Weight | Top Model | Score |
|-----------|--------|-----------|-------|
| tool_use | 0.35 | gpt-4.1 | 0.95 |
| reasoning | 0.30 | claude-sonnet-4 | 0.92 |
| ... | | | |

Include **benchmarks referenced** per task type (from matrix `benchmarks` field).

### Phase C — KPI Score (from Step 3)

```
FUNCTION kpiScore(model, kpi_profile):
  RETURN Σ (kpi_profile.normalized_weight[k] × model.kpi_affinity[k])
```

Apply tier floor (unchanged from v0.1):

```
min_tier from K01, K02, K06, K09 + pattern bump for P2/P5/P6/P7
ELIMINATE models below min_tier
ELIMINATE if K08 >= 3 AND model.multimodal == false
PENALIZE if context insufficient
```

### Phase D — Composite Score

From `BENCHMARK-MATRIX.yaml` → `selection_blend`:

```
composite = (0.55 × benchmark_score)
          + (0.35 × kpi_score)
          + (0.10 × compliance_fit)

compliance_fit:
  1.0 if model passes all filters with no penalties
  0.7 if regional deployment required but available
  0.4 if api used under strict residency with private endpoint
  0.0 if eliminated
```

### Phase E — Rainy Day Capability Check

For each `rainy_day` scenario, verify selected primary model meets thresholds from `rainy_day_capability_map`:

```
IF scenario.type == "ambiguous_intent":
  REQUIRE benchmarkScore(primary, [conversation, classification]) >= 0.75
  IF NOT: WARN "Consider stronger conversation model or clarification sub-agent"

IF scenario.severity == critical AND scenario.requires_human:
  ENSURE pattern includes HITL; model selection is for draft-only role
```

---

## Per-Step Model Recommendations

For each flow step, compute benchmark score for that step's `task_types` only:

```yaml
per_step_models:
  - step_id: S1
    action: "Classify dispute type"
    task_types: [classification]
    recommended_model: gpt-4o-mini
    benchmark_score: 0.82
    rationale: "High-volume triage; classification benchmark leader in T3"
  - step_id: S4
    action: "Draft resolution"
    task_types: [reasoning, generation]
    recommended_model: claude-sonnet-4
    benchmark_score: 0.91
```

Flow-level **primary** = highest composite score across full task weight profile.
**Economy** = best composite among T3/T4 for highest-weight low-complexity task types.

---

## Output Structure

```yaml
model_recommendations:
  selection_method: "benchmark-aware composite (55% benchmark + 35% KPI + 10% compliance)"
  task_profile_used:
    primary_task_types: [tool_use, reasoning]
    task_weights: { tool_use: 0.4, reasoning: 0.35, generation: 0.25 }
  benchmarks_referenced:
    - task: tool_use
      benchmarks: [BFCL, τ-bench]
    - task: reasoning
      benchmarks: [GPQA, MMLU-Pro]
  compliance_notes:
    - "<e.g. GDPR — deploy Claude via AWS Bedrock eu-west-1>"
  primary:
    model_id: ""
    composite_score: 0.0
    benchmark_score: 0.0
    kpi_score: 0.0
    rationale: ""
  fallback: { ... }
  economy: { ... }
  orchestrator_model: { ... }  # P2 only
  per_step_models: [ ... ]
  rainy_day_coverage:
    - scenario_id: RD1
      covered: true | false
      gap: "<if false, what's missing>"
```

---

## Hosting, Compute, Cost, Online Recs

(Unchanged logic from v0.1 — apply after model selection)

- Hosting decision from KPI + `region_network` + `regulatory_compliance`
- Self-hosted compute from `COMPUTE-SIZING.md` using `traffic.peak_concurrent` and `peak_factor`
- API cost from `COST-MODEL.yaml` using `traffic.daily_interactions` and rainy day call overhead (+10% if >20% rainy day volume)
- Online recommendations: router, cache, fallback, guardrails

**Traffic sizing note:** Use `peak_factor` from flow:

```
peak_daily = daily_interactions × peak_factor
cost_sensitivity_scenarios: [average_day, peak_day]
```

---

## Present Summary

Show three tables:

**1. Benchmark fit by task type**

**2. Model ranking (composite score)**

| Rank | Model | Benchmark | KPI | Compliance | Composite |
|------|-------|-----------|-----|------------|-----------|

**3. Per-step model map** (if steps > 2)

Ask: **"Accept model recommendations, or adjust task weights / compliance assumptions?"**

Proceed to `generate-design-artifact`.

## Negative Scenarios

| Scenario | Response |
|----------|----------|
| No task_types tagged on steps | Re-run step tagging from capture-business-flow |
| All API models eliminated by compliance | Recommend self-hosted primary; list compliant options |
| Benchmark scores tie within 0.03 | Present tie-breaker: cost (K06), latency (K03), vendor preference |
| Multimodal required but best text model selected | Force multimodal candidate to primary |

## Disclaimer (always include)

> Benchmark scores are **design-time proxies** from `BENCHMARK-MATRIX.yaml`. They are not a substitute for evaluation on your sunny/rainy day scenarios. Phase 2 should run customer eval before production.
