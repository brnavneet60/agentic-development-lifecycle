---
name: generate-design-artifact
description: Compile all E2E design steps into final agentic-design-artifact.md. Step 10.
metadata:
  harness: agentic-design-harness
  step: 10
  version: "1.0.0"
---

# Generate Design Artifact

## Purpose

Produce the final HLD markdown combining Steps 1–9.

## Prerequisites

- All step outputs (flow, pattern, kpis, models, tools, memory/knowledge, framework, guardrails/security, observability/value/loops)
- `templates/agentic-design-artifact-template.md`

## Sections to Fill

| # | Section | Source Step |
|---|---------|-------------|
| 1 | Executive Summary | All |
| 2–6 | Business flow, scenarios, compliance, process nuances | 1 |
| 7 | Design pattern + resilience | 2 |
| 8 | KPI profile | 3 |
| 9–12 | Models, hosting, cost/compute | 4 |
| 13 | Tools & MCP | 5 |
| 14 | Memory & knowledge | 6 |
| 15 | Agent framework | 7 |
| 16 | Guardrails & security | 8 |
| 17 | Observability & value KPIs | 9 |
| 18 | Loop engineering | 9 |
| 19 | Risks, assumptions, open questions | All |
| 20 | Next steps (POC, kagent-platform-harness) | — |

## Write Path

```
agents-output/<flow.slug>/agentic-design-artifact.md
```

## Quality Checks

```
IF any open_questions[] non-empty across steps:
  INCLUDE section "Open Questions for Stakeholders"
IF framework.kagent_platform_path == true:
  NEXT STEP = "Run kagent-platform-harness on this artifact"
IF compliance conflict unresolved:
  FLAG in Risks — do not mark artifact "approved"
```

Present file path to user when complete.
