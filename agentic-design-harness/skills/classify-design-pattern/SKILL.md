---
name: classify-design-pattern
description: Select the best agentic AI design pattern and sketch agent topology from a structured business flow. Use as Step 2 after capture-business-flow.
compatibility: Offline. Read references/design-patterns/DESIGN-PATTERNS.md.
metadata:
  harness: agentic-design-harness
  step: 2
  version: "1.0.0"
---

# Classify Design Pattern

## Purpose

E2E section **2e** — pattern, agent count, **sync vs async**, inter-agent communication, orchestration, resilience (circuit breaker, retries, timeouts).

## Prerequisites

- Completed output from `capture-business-flow`
- Read `references/design-patterns/DESIGN-PATTERNS.md`

## Instructions

### 1. Apply Decision Logic

Evaluate `flow.signals_for_pattern`, **rainy day scenarios**, and step characteristics:

```
// Rainy day influences
IF any rainy_day.severity == critical AND requires_human:
  SET overlay.hitl = true

IF rainy_day scenarios include system_timeout OR downstream_failure:
  SUGGEST retry + fallback pattern; prefer P3 or P2 with circuit breaker

IF count(rainy_day) > count(sunny_day) * 0.5:
  WARN "High edge-case ratio — consider P5 HITL or stronger guardrails"
```

```
PRIORITY ORDER (first match wins unless overridden):

1. IF any step.requires_approval == true
   → Pattern P5: Human-in-the-Loop

2. ELSE IF flow.signals.has_parallel_branches == true
   → Pattern P4: Parallel Fan-out / Fan-in

3. ELSE IF flow.signals.needs_knowledge_retrieval == true
   AND retrieval is core to >40% of steps
   → Pattern P6: RAG-Augmented Agent

4. ELSE IF flow.signals.is_event_driven == true
   → Pattern P7: Event-Driven / Async

5. ELSE IF flow.signals.agent_count_estimate > 1
   OR steps need dynamic routing between specialists
   → Pattern P2: Supervisor-Orchestrator

6. ELSE IF flow has fixed sequential stages
   AND each stage has distinct responsibility
   → Pattern P3: Sequential Pipeline

7. ELSE
   → Pattern P1: ReAct Single Agent
```

### 2. Complexity Checks

```
IF pattern == P1 AND tool_count_estimate > 8:
  WARN "Consider P2 Supervisor — tool surface is large"

IF pattern == P1 AND reasoning_depth across steps > 5 hops:
  SUGGEST upgrade to P2 or P3

IF pattern involves financial/legal actions AND pattern != P5:
  SUGGEST add HITL gate (P5 overlay)
```

### 3. Sketch Topology

Produce an ASCII diagram, e.g.:

```
P2 Supervisor example:

  User Request
       │
       ▼
  ┌─────────────┐
  │ Supervisor  │──routes──▶ Specialist A (lookup)
  │   Agent     │──routes──▶ Specialist B (draft)
  └─────────────┘──routes──▶ Specialist C (notify)
       │
       ▼
  Aggregated Response
```

### 4. Output

```yaml
pattern:
  id: P1 | P2 | P3 | P4 | P5 | P6 | P7
  name: "<pattern name>"
  rationale: "<2-3 sentences why this pattern>"
  complexity: low | medium | high
  agent_topology:
    agents:
      - role: "<e.g. supervisor>"
        responsibility: "<what it does>"
    estimated_llm_calls_per_flow: <range>
  overlays:
    hitl: true | false
  execution:
    sync_async: sync | async | hybrid
    orchestration: supervisor | pipeline | event_bus | peer_to_peer | none
    communication: a2a | shared_state | message_queue | direct_call
  resilience:
    circuit_breaker_on_tools: true | false
    retry_policy: "<e.g. 3x exponential backoff on tool timeout>"
    timeouts:
      llm_call_ms: <int>
      tool_call_ms: <int>
      end_to_end_ms: <int or null>
  alternatives_considered:
    - pattern: "<id>"
      rejected_because: "<reason>"
```

### 5. Confirm

Ask user: **"Does this pattern and topology fit your intent?"**

Proceed to `define-kpis` after confirmation.

## Negative Scenarios

| Scenario | Response |
|----------|----------|
| Flow fits multiple patterns equally | Present top 2 with trade-offs; let user choose |
| User wants microservices not agents | Clarify this harness designs agentic layer, not service decomposition |
| Pattern seems over-engineered | Offer simpler pattern with documented trade-off |
