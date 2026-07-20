---
name: design-memory-knowledge
description: Design memory patterns, knowledge base, RAG/GraphRAG/ontology, context and token strategy. Step 6 of agentic-design-harness E2E.
metadata:
  harness: agentic-design-harness
  step: 6
  version: "1.0.0"
---

# Design Memory & Knowledge

## Purpose

Cover E2E sections **2c Memory** and **2d Knowledge base**. Do **not** assume RAG is needed — justify from flow.

## Inputs

- `flow.process_nuances` (documentation, existing KB)
- `flow.signals_for_pattern.needs_knowledge_retrieval`
- `pattern`, `tools`, `kpi_profile`

## Memory Interview

1. **Per agent** — short-term session only, or long-term user/org memory?
2. **What must be remembered** — preferences, case history, learned policies?
3. **Retention** — TTL, GDPR erasure, audit?
4. **Pattern** — episodic, semantic, procedural (see `references/memory-patterns/MEMORY-PATTERNS.md`)

## Knowledge Interview

1. **Existing KB?** — Type, coverage, freshness (from Block H)
2. **RAG vs GraphRAG vs ontology** — structured relationships needed?
3. **Ontology** — domain terms, policy rules, SHACL-style constraints? (e.g. kagent-ontology for platform agents)
4. **Embeddings** — which model, re-index frequency, chunk strategy?
5. **Context management** — summarization, compaction, sliding window?
6. **Token optimization** — what can be retrieved vs inlined vs summarized?

**Ask** if any answer is unknown.

## Decision Guide

| Need | Approach |
|------|----------|
| Policy/docs Q&A | **Vector RAG** |
| Multi-hop entity relations | **GraphRAG** or knowledge graph |
| Platform CRD / rule traps | **Ontology + SPARQL** (Kagent path) |
| Conversation continuity | **Session memory** + optional long-term store |
| High K05 context + cost pressure | **Compaction** + retrieval |

## Output

```yaml
memory:
  agents:
    - agent: "<name>"
      short_term: true | false
      long_term: true | false
      pattern: session | episodic | semantic | procedural
      store_candidate: redis | postgres | vector | kagent_memory_crd | none
      retention_policy: "<TTL, compliance>"

knowledge:
  required: true | false
  existing_kb:
    present: true | false
    type: wiki | confluence | tickets | vector_db | ontology | mixed
    gaps: ["<what is missing>"]
  strategy:
    primary: none | rag | graphrag | ontology | hybrid
    embedding_model: "<id or TBD — link to model-selection>"
    chunk_strategy: fixed | semantic | document_structure
    reindex_frequency: on_push | daily | weekly | manual
  context_management:
    max_context_tokens: <estimate>
    compaction: none | summarize_old | retrieve_only
    cache_prompt: true | false
  open_questions: []
```

## Checkpoint

Present summary. Ask: **"Is memory and knowledge strategy correct before framework selection?"**

## Next Skill

`select-agent-framework`
