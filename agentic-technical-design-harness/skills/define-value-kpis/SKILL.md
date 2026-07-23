---
name: define-value-kpis
description: >
  Define business and technical KPIs including tool recall and parameter accuracy, wired to eval and dashboards. Use as Step 7.
---

# Define value measure KPIs

## Purpose

KPI catalog at Accept quality — leadership metrics **and** eng quality gates.

## Instructions

1. Business KPIs (resolution, TTR, escalation, CSAT, cost/dispute, leakage) with owners and methods.  
2. **Required tech KPIs:** tool recall, tool parameter accuracy, tokens/interaction, p95 latency, tool error rate.  
3. HITL ops KPIs when Ask/Manual exists (backlog, override rate).  
4. Wire each KPI to observability (§9) and evaluation exit gates (§10).  
5. Decision discipline for metric/storage choices.

## Output

`kpis.yaml` with business[], technical[], hitl_ops[].
