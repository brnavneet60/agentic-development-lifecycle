# Agentic Design Patterns — Phase 1 Catalog

## Decision Tree

```
START
  │
  ├─ Approval required at any step? ──YES──▶ P5 Human-in-the-Loop
  │
  ├─ Parallel independent branches? ──YES──▶ P4 Fan-out / Fan-in
  │
  ├─ Heavy knowledge retrieval (>40% steps)? ──YES──▶ P6 RAG-Augmented
  │
  ├─ Event/queue triggered? ──YES──▶ P7 Event-Driven
  │
  ├─ Multiple specialists / dynamic routing? ──YES──▶ P2 Supervisor
  │
  ├─ Fixed multi-stage pipeline? ──YES──▶ P3 Sequential Pipeline
  │
  └─ ELSE ──▶ P1 ReAct Single Agent
```

---

## P1 — ReAct Single Agent

**Description:** One agent loop: Reason → Act (tool call) → Observe → repeat until done.

```
User ──▶ ┌──────────────┐ ──tool calls──▶ [CRM] [Email] [DB]
         │ ReAct Agent  │
         └──────────────┘
                │
                ▼
            Response
```

| Attribute | Value |
|-----------|-------|
| Complexity | Low |
| LLM calls / flow | 3–5 |
| Best for | Single-domain tasks, ≤8 tools, linear logic |
| Risks | Tool sprawl; context window fills with long loops |

**Example flows:** FAQ bot with 3 tools, simple data lookup + email draft.

---

## P2 — Supervisor-Orchestrator

**Description:** A coordinator agent routes sub-tasks to specialist agents and aggregates results.

```
User ──▶ ┌─────────────┐
         │ Supervisor  │──▶ Research Agent ──▶ tools
         └─────────────┘──▶ Writer Agent   ──▶ tools
                │         └──▶ Review Agent  ──▶ tools
                ▼
           Final Output
```

| Attribute | Value |
|-----------|-------|
| Complexity | Medium |
| LLM calls / flow | 6–15 |
| Best for | Multi-domain tasks, dynamic routing |
| Model strategy | T3 supervisor + T2/T1 specialists |
| Risks | Orchestration latency; error propagation |

**Example flows:** Customer dispute resolution, multi-system onboarding.

---

## P3 — Sequential Pipeline

**Description:** Fixed DAG — each stage agent hands output to the next.

```
Input ──▶ [Extract] ──▶ [Classify] ──▶ [Act] ──▶ [Notify] ──▶ Output
```

| Attribute | Value |
|-----------|-------|
| Complexity | Medium |
| LLM calls / flow | 4–8 (one per stage) |
| Best for | Predictable multi-step workflows |
| Model strategy | T3 for early stages; T2 for decision stage |
| Risks | Rigid — hard to handle exceptions |

**Example flows:** Document intake → validation → routing → archival.

---

## P4 — Parallel Fan-out / Fan-in

**Description:** Independent sub-tasks run in parallel; aggregator merges results.

```
              ┌──▶ Agent A ──┐
Input ──▶ Fan-out ──▶ Agent B ──├──▶ Fan-in ──▶ Output
              └──▶ Agent C ──┘
```

| Attribute | Value |
|-----------|-------|
| Complexity | Medium |
| LLM calls / flow | 4–12 (parallel) |
| Best for | Research, comparison, multi-source analysis |
| Risks | Merge logic complexity; cost spikes |

**Example flows:** Competitive analysis, multi-vendor quote comparison.

---

## P5 — Human-in-the-Loop (HITL)

**Description:** Agent proposes actions; human approves before execution. Can overlay any pattern.

```
Agent ──▶ Proposed Action ──▶ [Approval Queue] ──▶ Human ──▶ Execute / Reject
```

| Attribute | Value |
|-----------|-------|
| Complexity | Medium–High |
| LLM calls / flow | 2–6 + human wait |
| Best for | Financial transactions, legal, privileged access |
| Risks | Latency; approval bottlenecks |

**Example flows:** Refund authorization, contract signing, production config changes.

---

## P6 — RAG-Augmented Agent

**Description:** Retrieval step feeds context into agent reasoning loop.

```
Query ──▶ [Retriever] ──▶ Vector DB / Docs
              │
              ▼
         ┌─────────┐
         │ Agent   │──▶ tools
         └─────────┘
              │
              ▼
          Response
```

| Attribute | Value |
|-----------|-------|
| Complexity | Medium–High |
| LLM calls / flow | 4–10 (+ embedding calls) |
| Best for | Policy Q&A, support, knowledge-heavy domains |
| Model strategy | T3 embedding model + T2 agent; T1 for complex synthesis |
| Risks | Retrieval quality; stale knowledge |

**Example flows:** Internal policy assistant, technical support with KB.

---

## P7 — Event-Driven / Async Agent

**Description:** Triggers from events/queues; long-running stateful workflows.

```
[Event Bus] ──▶ Trigger ──▶ Agent Worker ──▶ [State Store]
                    │              │
                    ▼              ▼
               Scheduler      Downstream Events
```

| Attribute | Value |
|-----------|-------|
| Complexity | High |
| LLM calls / flow | Variable |
| Best for | Monitoring, incident response, scheduled jobs |
| Risks | State management; idempotency; observability gaps |

**Example flows:** Alert triage, SLA breach escalation, batch report generation.

---

## Pattern Comparison Table

| Pattern | Agents | Dynamic Routing | Human Gate | Typical Tier |
|---------|--------|-----------------|------------|--------------|
| P1 ReAct | 1 | No | Optional | T2–T3 |
| P2 Supervisor | 2–5 | Yes | Optional | T2 (+ T3 orch) |
| P3 Pipeline | 2–5 | No | Optional | T2–T3 |
| P4 Fan-out | 2–5 | Partial | Optional | T2 |
| P5 HITL | 1+ | Varies | **Required** | T2 |
| P6 RAG | 1–2 | Optional | Optional | T2 + embed |
| P7 Event | 1+ | Yes | Optional | T2–T3 |
