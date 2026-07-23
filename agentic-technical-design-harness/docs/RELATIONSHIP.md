# Relationship to agentic-design-harness

| Harness | Audience | Artifact |
|---------|----------|----------|
| `agentic-design-harness` | Leaders / PMs / architects | Executive HLD |
| `agentic-technical-design-harness` (this) | Architects / platform / eng | Technical Design Document (TDD) |

Typical flow:

1. Executive requirement summary (or executive HLD) is the **input**.
2. This harness produces a deep technical design covering components, models, tools, memory, context, KPIs, observability, eval, loops, guardrails, identity, and frameworks — with K8s/cloud-native defaults.
3. Downstream implementation harnesses (e.g. kagent / platform) consume the TDD.
