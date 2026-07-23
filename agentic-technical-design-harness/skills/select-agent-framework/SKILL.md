---
name: select-agent-framework
description: >
  Recommend production vs prototype frameworks with rejected alternates. Use as Step 13 before final artifact.
---

# Select agent framework

## Purpose

Framework choice at Accept quality — knowledgebase Ch 1 framing + cloud-native maturity.

## Instructions

1. Prefer **LangGraph** (or equivalent inspectable graph) for production control, checkpoints, HITL.  
2. CrewAI / OpenAI Agents SDK OK for **prototypes only** — do not promote prototype framework to prod without re-eval.  
3. AutoGen when dialogue-heavy research patterns dominate — not default for gated financial/support graphs.  
4. Document rejected alternates with reasons.  
5. Match framework to topology from Step 2.

## Output

`frameworks.yaml` with production_choice, prototype_options, rejected[].
