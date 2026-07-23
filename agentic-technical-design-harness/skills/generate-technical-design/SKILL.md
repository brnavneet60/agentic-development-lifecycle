---
name: generate-technical-design
description: >
  Compile Steps 1–13 into a Technical Design Document that meets OUTPUT-STANDARDS.
  Use as final Step 14 after checkpoint gates; refuse to deliver if the P0 checklist fails.
---

# Generate technical design

## Purpose

Produce an Accept-quality NLD Technical Design Document for the current use case.

## Preconditions

1. Read `OUTPUT-STANDARDS.md`.  
2. Read `references/knowledgebase.md` (id `knowledgebase`).  
3. Read `outputs/templates/default.md`.  
4. Steps 1–13 outputs available (or regenerable summaries).

## Instructions

1. Render the full template — **every** required section and appendix that applies.  
2. Enforce hard boundaries:
   - Sequence (slices) ≠ end-state topology  
   - Propose → authorize (non-LM gate) → execute  
   - Named models with dated pricing  
3. Include PDM epic map, prompt governance, AuthZ matrix with Authorize column, K8s resilience density.  
4. Evidence Register: knowledgebase book chapters **and** full https peer/standards/pricing URLs.  
5. Run OUTPUT-STANDARDS P0 checklist. **If any P0 item fails, fix before deliver-output.**  
6. Activate `deliver-output` to the configured deliverer path (default under `agents-output/agentic-technical-design-harness/<slug>/`).

## Anti-patterns (do not ship)

- Day-1 full multi-agent as default build order  
- LM as money/irreversible authorizer  
- Tier-only model tables  
- Missing tool recall / param accuracy  
- Thin K8s or AuthZ sections  
- Harness-internal paths as sole evidence  
