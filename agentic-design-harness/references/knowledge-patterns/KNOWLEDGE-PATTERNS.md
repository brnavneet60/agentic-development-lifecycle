# Knowledge Base Patterns

| Strategy | Best For | Trade-offs |
|----------|----------|------------|
| **None** | Tool-only agents, all data live from APIs | Simple; no stale docs |
| **Vector RAG** | Policy PDFs, manuals, tickets | Chunk quality matters; hallucination risk |
| **GraphRAG** | Entity-heavy domains (accounts, products, dependencies) | Higher build cost |
| **Ontology + SPARQL** | Rules, traps, typed relationships (platform CRDs) | Needs ontology maintenance |
| **Hybrid** | Enterprise production | Best accuracy; most ops |

## RAG Design Checklist

- [ ] Chunk size / overlap strategy
- [ ] Embedding model aligned with Step 4
- [ ] Re-index trigger (git push, schedule)
- [ ] Citation in agent responses required?

## Context / Token Optimization

| Technique | When |
|-----------|------|
| Retrieve don't stuff | Large corpora |
| Summarize history | Long sessions |
| Prompt caching | Repeated system prompts (API providers) |
| Compaction | Multi-turn over 50k tokens |

## Ask Don't Assume

If user has not described KB contents, **ask** before selecting RAG.
