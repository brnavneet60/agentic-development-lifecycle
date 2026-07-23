---
name: design-observability
description: >
  Design OTel-aligned metrics, logs, and traces including semantic agent signals. Use as Step 8 with evaluation.
---

# Design observability

## Purpose

Observability at Accept quality — infra + semantic signals (knowledgebase Ch 10).

## Instructions

1. Prefer OpenTelemetry data plane (GenAI semantic conventions); optional LangSmith/etc. as UX complement — not sole plane.  
2. Signal catalog: traces (graph/LLM/tool/HITL), metrics (errors, tokens, cost, queue), logs (redacted), semantic quality samples.  
3. Alerts for p95, tool bursts, budget, PII scrub failure, HITL backlog/fatigue.  
4. Stack evaluation: chosen vs alternates with reasons.  
5. Escalate to `otel-ai-agent-observability` as needed.

## Output

`observability.yaml` with signals[], stack_decision, alerts[].
