---
name: define-kpis
description: Define and weight KPIs for agentic AI model selection — quality, latency, cost, privacy, throughput, context, reasoning, multimodal, tool use, availability. Use as Step 3.
compatibility: Offline. Read references/kpi-framework/KPI-FRAMEWORK.yaml.
metadata:
  harness: agentic-design-harness
  step: 3
  version: "1.0.0"
---

# Define KPIs

## Purpose

Build a weighted KPI profile that drives model tier and hosting mode selection.

## Prerequisites

- Flow from Step 1
- Pattern from Step 2
- Read `references/kpi-framework/KPI-FRAMEWORK.yaml`

## Instructions

### 1. Propose Default KPI Weights

Infer initial weights (1–5) from flow, pattern, and **regulatory/compliance** fields captured in Step 1. Present as a table:

| KPI | Name | Proposed Weight | Rationale |
|-----|------|-----------------|-----------|
| K01 | Quality / Accuracy | ? | from success_criteria strictness |
| K02 | Reasoning Depth | ? | from decision complexity |
| K03 | Latency | ? | from user-facing vs batch |
| K04 | Throughput | ? | from volume.daily_interactions |
| K05 | Context Length | ? | from document sizes |
| K06 | Cost Sensitivity | ? | from budget signals |
| K07 | Privacy / Data Residency | ? | from data.sensitivity |
| K08 | Multimodal | ? | from image/audio needs |
| K09 | Tool Use Complexity | ? | from systems count |
| K10 | Availability SLA | ? | from production vs dev |

### 2. Inference Rules

Use Step 1 structured fields — do not re-ask if already captured.

```
K07_privacy:
  flow.regulatory_compliance.data_classification == regulated → 5
  phi or pci → 5
  pii → 4
  internal → 2
  public → 1
  IF flow.region_network.data_residency_required: K07 = max(K07, 4)
  IF flow.regulatory_compliance.approved_vendors == self_hosted_only: K07 = 5

K04_throughput:
  USE flow.traffic.daily_interactions AND peak_factor
  >100K/day → 5
  10K–100K → 4
  1K–10K → 3
  100–1K → 2
  <100 → 1
  IF peak_factor >= 10: bump K04 by 1 (cap at 5)

K06_cost:
  IF user mentions "minimize cost" OR throughput >= 4 → 4 or 5
  IF user mentions "best quality regardless" → 1

K03_latency:
  flow.traffic.latency_expectation == realtime → 4–5
  minutes → 3
  batch → 1–2

K10_availability:
  production + rainy_day severity critical → 4–5
  dev/POC only → 1

K01_quality:
  IF any rainy_day.severity == critical: K01 = max(K01, 4)
  IF flow.domain.goal includes accuracy/regulated outcome: K01 >= 4

K09_tool_use:
  FROM flow.signals_for_pattern.tool_count_estimate
  >= 6 tools → 4; >= 10 → 5

K05_context:
  IF task_profile includes rag_retrieval OR extraction from long docs → 3–5
```

### 2b. Compliance → KPI Cross-Check

Present compliance summary alongside KPI table:

| Constraint | Source (Step 1) | KPI Impact |
|------------|-----------------|------------|
| GDPR + EU residency | region_network | K07 ↑, hosting bias |
| Self-hosted only | approved_vendors | K07 = 5 |
| Air-gapped | network_topology | K07 = 5, eliminate API |
| Audit trail required | regulatory_compliance | K10 ↑, note in artifact |

### 3. User Adjustment

Ask: **"Adjust any KPI weights (1=low priority, 5=critical)?"**

Recalculate normalized weights:

```
normalized_weight[kpi] = user_weight[kpi] / sum(all user_weights)
```

### 4. Derive Hosting Signals

```yaml
kpi_profile:
  weights:
    K01: { raw: 4, normalized: 0.12 }
    # ... all 10 KPIs
  derived:
    min_quality_tier: T1 | T2 | T3 | T4
    hosting_bias: self_hosted | api | hybrid
    context_tokens_required: <estimate>
    multimodal_required: true | false
```

### 5. Hosting Bias Logic

```
IF K07 >= 4 OR flow.data.residency_required: hosting_bias = self_hosted
ELSE IF K06 >= 4 AND K04 >= 3: hosting_bias = self_hosted  # volume economics
ELSE IF K01 >= 4 AND K02 >= 4: hosting_bias = api  # frontier quality
ELSE: hosting_bias = hybrid
```

### 6. Confirm

Present KPI profile. Ask: **"Confirm KPI profile before model selection?"**

Proceed to `model-selection` after confirmation.

## Negative Scenarios

| Scenario | Response |
|----------|----------|
| All KPIs rated 5 | Warn "conflicting optimization" — ask top 3 priorities |
| Privacy=5 but user wants GPT-4 API | Flag conflict; recommend self-hosted or private endpoint |
| No volume estimate | Use conservative default (weight 2) and note assumption |
