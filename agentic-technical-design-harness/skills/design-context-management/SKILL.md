---
name: design-context-management
description: >
  Design context engineering for token economics, quality, latency, reliability, and scalability (selective, explicit, structured, tiered hot/warm/cold). Use as Step 6 after or with memory design.
---

# Design context management

## Purpose

E2E: context management — token economics, response quality, latency, reliability, scalability.

## Core principles

1. Selective over quantity
2. Explicit over implicit
3. Structured over unstructured
4. Tiered storage — hot / warm / cold
5. Observability and tracing of context packs

## Instructions

1. Read offline `context-management` stub; escalate to `langchain-context-engineering` when needed.
2. Define context packing rules per agent/step; budgets and truncation policy.
3. Map hot/warm/cold tiers to memory design.
4. **Checkpoint** models + tools + memory + context with the user.

## Output

`context-management.yaml`.

