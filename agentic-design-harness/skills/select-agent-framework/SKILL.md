---
name: select-agent-framework
description: Select agent development framework(s) — LangGraph, CrewAI, Kagent, etc. Step 7 of agentic-design-harness E2E.
metadata:
  harness: agentic-design-harness
  step: 7
  version: "1.0.0"
---

# Select Agent Framework

## Purpose

Map E2E section **2f** — which runtime/framework implements the design. One or more may apply (e.g. LangGraph for logic + Kagent for K8s ops).

## Inputs

- `pattern`, `tools`, `memory`, `knowledge`
- `flow.regulatory_compliance`, `flow.region_network`
- Target deployment hint (if user stated): cloud K8s, serverless, SaaS only

## Load Reference

`references/agent-frameworks/AGENT-FRAMEWORKS.md`

## Evaluation Criteria

| Criterion | Weight |
|-----------|--------|
| Pattern fit (graph, crew, CRD-native) | High |
| MCP / tool ecosystem | High |
| K8s / GitOps alignment | Medium (if platform path) |
| Team familiarity | Medium |
| Observability hooks | Medium |
| License / vendor lock-in | Low–Medium |

## Framework Shortlist

| Framework | Best For |
|-----------|----------|
| **Kagent** | K8s-native agents, MCP, A2A, GitOps, platform already on Kagent |
| **LangGraph** | Explicit state machines, checkpoints, complex branching |
| **CrewAI** | Role-based teams, rapid prototyping |
| **Semantic Kernel** | .NET / enterprise Microsoft stack |
| **AutoGen** | Multi-agent research, conversational grids |
| **Custom + LiteLLM** | Maximum control, framework-less |

## Output

```yaml
framework:
  primary: "<name>"
  secondary: ["<optional>"]
  rationale: "<why fits pattern + constraints>"
  deployment_target: kubernetes | vm | serverless | saas_runtime
  kagent_platform_path: true | false  # if true → kagent-platform-harness next
  trade_offs:
    gain: ["<benefits>"]
    lose: ["<costs>"]
  open_questions: []
```

## Next Skill

`design-guardrails-security`
