---
name: design-observability-value-loops
description: Observability (metrics, logs, traces), business value KPIs, feedback/loop engineering. Step 9 of agentic-design-harness E2E.
metadata:
  harness: agentic-design-harness
  step: 9
  version: "1.0.0"
---

# Design Observability, Value & Loops

## Purpose

E2E sections **2i Observability**, **2j Value reporting**, and **2k Loop engineering**.

## Observability

Define per layer:

| Layer | What to capture |
|-------|-----------------|
| **Metrics** | Latency p50/p95, token usage, tool error rate, cost per flow |
| **Logs** | Structured agent steps, tool I/O (redacted), decisions |
| **Traces** | OpenTelemetry spans: LLM call → tool → sub-agent |

Ask: existing stack? (Prometheus, Grafana, Langfuse, Datadog, Elastic)

## Value Reporting (Business KPIs)

Map **process KPIs from Step 1** to **measurable agent KPIs**:

```yaml
value_kpis:
  - business_kpi: "<from process_nuances>"
    agent_metric: "<e.g. auto-resolution rate>"
    measurement: "<how to calculate>"
    data_source: "<logs, CRM, survey>"
    dashboard: "<Grafana panel id or TBD>"
    target: "<goal>"
```

Ask: who consumes dashboards? exec vs ops vs product?

## Loop Engineering

| Loop Type | Purpose |
|-----------|---------|
| **Human feedback** | Thumbs up/down, corrections → improve prompts |
| **HITL approval** | High-risk actions (ties to pattern P5) |
| **Eval loop** | Offline golden set, regression on model change |
| **Continuous improvement** | Weekly review of failed traces |
| **Cost feedback** | Alert when spend exceeds budget |

```yaml
loops:
  human_feedback: true | false
  hitl_gates: [<step or tool ids>]
  eval_suite:
    required: true | false
    golden_cases_count: <int or 0>
  continuous_improvement:
    cadence: weekly | monthly | per_release
    owner: "<team>"
  cost_feedback: true | false
```

## Checkpoint

Ask: **"Are observability and success metrics complete before generating the artifact?"**

## Next Skill

`generate-design-artifact`
