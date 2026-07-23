---
name: design-components-patterns
description: >
  Design agency ladder, sliced MVP, end-state topology, and evolve triggers for multi-agent systems.
  Use as Step 2 after clarify-requirements. Prefer knowledgebase.md; never default to Day-1 full multi-agent.
---

# Design components & patterns

## Purpose

E2E component selection with OUTPUT-STANDARDS quality: workflows vs agents, slices, parsimony, policy-gate ownership.

## Preconditions

Resolve `knowledgebase` first (Ch 1, 2, 5, 8). Also `design-patterns-stub` / online framework docs as needed.

## Instructions

1. **Agency ladder** (code → workflow → RAG → agent) per path — irreversible/money paths use **non-LM workflow/policy-gate**.  
2. **Sliced MVP** with in-scope / out-of-scope / architecture-at-slice / **exit gates** (defaults in OUTPUT-STANDARDS §7).  
3. **PDM epic map**: epic → slice → gate → KPI + ticket template.  
4. **Prompt governance** per slice (pack id, owner, cadence, promote rule).  
5. **Single → multi-agent timing**: start as simple as reliable; try hierarchical/semantic tool grouping before splitting; introduce manager/specialists only on **triggers** (tool-selection errors for N windows, second domain, or Product mandate).  
6. **Critic** (if any): gated on write-proposal error after prompt iterations — not Day-1.  
7. Draw **end-state** topology separately; label clearly **not Day-1**.  
8. Specify **policy-gate** contract + ownership (Platform runtime · Risk/Product rules · AI eng schema) when irreversible actions exist.  
9. Decision discipline for each major choice.  
10. **Checkpoint** with user.

## Output

`components-patterns.yaml` including: agency_ladder, slices[], epics[], prompt_governance[], evolve_triggers, end_state_topology, policy_gate.
