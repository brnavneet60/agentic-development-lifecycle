---
name: select-models
description: >
  Select concrete named models with dated pricing, alternates, and a routing ladder. Use as Step 3 after component topology is set.
---

# Select models

## Purpose

Model selection at Accept density — named API ids, dated $/MTok, hybrid routing (knowledgebase Ch 1–2).

## Instructions

1. Map each agent/component → capabilities (reasoning, tools, multimodal, context).  
2. Consider enterprise + open-weight; trusted sources only.  
3. Benchmarks when relevant: MMLU, DocVQA, GPQA, MT-Bench, BFCL, SWE-bench Verified, HotpotQA, MMMU — plus **domain golden-set** as the real gate.  
4. **Required table columns:** agent · API id · why · benchmarks/fit · cost dated · alternates rejected.  
5. Fetch live pricing when possible; set `pricing_verified_date`. Never invent prices.  
6. Routing ladder: economy → mid → frontier with triggers; soft/hard cost caps (Assumption OK).  
7. If vendor DPA pending: still name default + alternate stacks; label `Assumption — planning default`.  
8. Decision discipline per choice.

## Output

`models.yaml` with pricing_verified_date, primary_stack, alternate_stack, per_agent[], routing_policy.
