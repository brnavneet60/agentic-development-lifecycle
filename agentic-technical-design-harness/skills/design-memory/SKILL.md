---
name: design-memory
description: >
  Design Knowledge vs Memory planes, STM/LTM, procedural packs, and audit retention. Use as Step 5 with context management.
---

# Design memory

## Purpose

E2E memory with **Knowledge ≠ Memory** separation (knowledgebase Ch 6) — Accept quality.

## Instructions

1. Separate planes: **Knowledge** (published policies/docs) vs **STM** vs **episodic LTM** vs **procedural** (prompts) vs **audit**.  
2. Per agent: which planes are required and why (business case).  
3. Evaluate store tech (cloud-native maturity). GraphRAG only when multihop justified.  
4. TTL/retention + PII hooks (link guardrails).  
5. Token optimization: summaries over raw dumps; never dual-SoT between knowledge and episodic stores.  
6. Decision discipline per store.

## Output

`memory.yaml` with planes[] and per_agent_map[].
