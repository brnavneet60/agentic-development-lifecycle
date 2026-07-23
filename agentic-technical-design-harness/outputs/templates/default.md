# Technical Design Document — {{title}}

**Harness:** agentic-technical-design-harness  
**Version:** {{version}}  
**Date:** {{date}}  
**Slug:** `{{slug}}`  
**Status:** Draft — must pass OUTPUT-STANDARDS quality bar before publish  
**Audience:** Product/PDM · Platform Architect · Solution / AI eng  

| Artifact | Role |
|----------|------|
| **This file** | Authoritative NLD TDD for this use case |
| Executive HLD (if any) | Upstream FLD input |
| `references/knowledgebase.md` | Primary design brain (id: `knowledgebase`) |

**Design stage:** NLD (between executive FLD and future DLD). Not production code.

---

## 0. Hard boundaries

| Rule | Application to this design |
|------|----------------------------|
| Sequence ≠ end-state | Build order = slices below; topology diagram = target/end-state |
| Propose → authorize → execute | LM proposes; non-LM policy-gate authorizes; executor executes |
| Ask, don't assume | Open questions listed; defaults labeled Assumption |

---

## 1. Executive technical summary

{{Agency model · sliced delivery · autonomy defaults · framework · named model ladder · K8s posture · top risks}}

---

## 2. Clarified requirements & open questions

### 2.1 Confirmed facts

| ID | Fact | Source |
|----|------|--------|

### 2.2 Assumptions (planning defaults)

| ID | Assumption | Needs user approval? |
|----|------------|----------------------|

### 2.3 Open questions (blocking vs non-blocking)

| ID | Question | Blocking? |
|----|----------|-----------|

### 2.4 Closed design decisions (this TDD)

| ID | Resolution |
|----|------------|

---

## 3. Component selection & design patterns

### 3.1 Workflows vs agents ladder (knowledgebase Ch 1)

| Path | Choice (code / workflow / RAG / agent) | Why |
|------|----------------------------------------|-----|

### 3.2 Sliced MVP — build order

| Slice | In scope | Out of scope | Architecture at slice | Exit gates |
|-------|----------|--------------|----------------------|------------|

### 3.2b PDM roadmap (epic → slice → gate → KPI)

| Epic ID | Epic | Slice | Exit gate summary | Primary KPI |
|---------|------|-------|-------------------|-------------|

Ticket template: `Epic` → `Slice` → `Acceptance = exit gates` → `Eval suite id` → `Rollback`.

### 3.2c Prompt governance

| Slice | Prompt pack | Owner | Change cadence | Promote rule |
|-------|-------------|-------|----------------|--------------|

### 3.3 Single → multi-agent timing (knowledgebase Ch 8)

| Stage | Architecture | Trigger to evolve |
|-------|--------------|-------------------|

Manager / critic must be **trigger-gated**, not Day-1 default.

### 3.4 Target-state topology (end-state — not Day-1)

| Component | Role | Skills | Stateful? | Knowledge? |
|-----------|------|--------|-----------|------------|

```mermaid
flowchart TD
  %% End-state only — see §3.2 for build order
```

### 3.5 Policy-gate (or equivalent non-LM authorizer)

| Field | Spec |
|-------|------|
| Input | Signed ActionIntent (or domain equivalent) |
| Checks | Thresholds, fraud, scope, idempotency, approver if required |
| Output | AuthorizationDecision |
| Deployable | Separate from agent workers when irreversible actions exist |
| Ownership | Platform runtime · Risk/Product rules · AI eng schema |

### 3.6 Decision summary

| Choice | Business mapping | Justification | Alternates | Recommendation |
|--------|------------------|---------------|------------|----------------|

---

## 4. Model selection

> Named models required. Label Assumption if vendor DPA pending. Set `pricing_verified_date`.

| Agent / component | Recommended model (API id) | Why | Benchmarks / fit | Cost (dated) | Alternates |
|-------------------|----------------------------|-----|------------------|--------------|------------|

### Routing / cost policy

1. Economy default → mid-tier → frontier on triggers.  
2. Soft/hard per-interaction cost caps (Assumption if unknown).

`pricing_verified_date:` {{date}}

---

## 5. Tools & MCP

| Consumer | Tool | Interface | Auth scope | SLA | Build vs buy |
|----------|------|-----------|------------|-----|--------------|

**Write tools:** bound only to executor (never specialist LM tool lists).  
**MCP:** Phase decision + security caveat (knowledgebase Ch 4).

---

## 6. Memory

### Knowledge ≠ Memory

| Plane | Contents | Store | TTL |
|-------|----------|-------|-----|
| Knowledge | | | |
| STM | | | |
| Episodic LTM | | | |
| Procedural | | | |
| Audit | | | |

---

## 7. Context management

| Principle | How |
|-----------|-----|
| Selective over quantity | |
| Explicit over implicit | |
| Structured over unstructured | |
| Tiered hot/warm/cold | |
| Observability of packs | |
| No silent truncate of critical evidence | |

---

## 8. Value measure KPIs

| KPI | Type | How measured | Owner |
|-----|------|--------------|-------|

Must include **tool recall** and **tool parameter accuracy**.

---

## 9. Observability

| Signal | What | Backend | Alert |
|--------|------|---------|-------|

Stack evaluation (chosen vs alternates): {{...}}

---

## 10. Evaluation

### Offline / online / adversarial

{{golden sets, judges, canary, red team}}

### Exit criteria by slice

| Gate | Early slices | Write-enabled slices |
|------|--------------|----------------------|
| Policy consistency | ≥95% (default) | ≥95% |
| Tool recall | ≥90% | ≥90% |
| Param accuracy (IDs) | ≥98% | ≥98% |
| Param accuracy (amounts/actions) | n/a or N/A | ≥98% |
| Critical leakage / irreversible fail | n/a | 0 |

---

## 11. Continuous improvement (loop engineering)

| Loop | Trigger | Action | Owner | Kill switch |
|------|---------|--------|-------|-------------|

---

## 12. Guardrails

### Autonomy slider

| Mode | Behavior | Default use in this design |
|------|----------|----------------------------|
| Manual | | |
| Ask | | |
| Agent | | |

### Controls

| Control | Threat | Layer | Notes |
|---------|--------|-------|-------|

### HITL failure modes

| Risk | Mitigation |
|------|------------|
| Automation bias | |
| Alert fatigue | |
| Skill decay | |
| Misaligned incentives | |

---

## 13. Identity & access management

### Paths

| Path | Identity | AuthZ | Notes |
|------|----------|-------|-------|
| User → API | | | |
| Workload → SoR | | | |
| Agent ↔ Agent | | | |
| Agent ↔ MCP/tool | | | |
| Agent ↔ LLM | | | |
| Human approver | | | |

### AuthZ matrix (must include Authorize)

| Actor | Read | Propose | **Authorize** | Execute | Escalate | Notify |
|-------|------|---------|---------------|---------|----------|--------|
| Specialist / agent | | | **No** | **No** | | |
| policy-gate | | | **Yes** | No | | |
| action-executor | | | No | **Yes if authorized** | | |
| Model | via tools | request only | **Never** | **Never** | | |

---

## 14. Agent frameworks

| Layer | Framework | Why | Rejected alternates |
|-------|-----------|-----|---------------------|

Prod vs prototype framing required.

---

## 15. Design trade-offs

| Dimension | Choice | Trade-off | Mitigation |
|-----------|--------|-----------|------------|

---

## 16. Kubernetes / cloud-native deployment view

| Concern | Intent |
|---------|--------|
| Namespaces | |
| Workloads (incl. policy-gate when needed) | |
| Secrets / identity | |
| NetworkPolicy / egress | |
| Data stores + checkpoint hotspot mitigations | |
| GitOps / canary | |
| HPA | |
| Resilience (PDB, circuit breakers) | |
| Observability wiring | |

---

## 17. Decision register

| Decision | Chosen | Alternates | Why chosen | Business mapping |
|----------|--------|------------|------------|------------------|

---

## 18. References & Evidence Register

### 18.1 Knowledgebase (book title + chapter)

| Decision / claim | Type | Source | Notes |
|------------------|------|--------|-------|

### 18.2 External https sources

| Decision / claim | Type | Source (full https URL) | Notes |
|------------------|------|-------------------------|-------|

---

## Appendix A — HLD → TDD map (if HLD input)

| Exec HLD section | TDD section |
|------------------|-------------|

## Appendix B — Implementation build order

1. …

## Appendix C — Upstream delivery alignment (if HLD Phase wording conflicts with slices)

Document interpretation + recommended HLD patch + Product validation needed.
