# Agentic AI Design Artifact

**Flow:** {{flow.display_name}}  
**Domain:** {{flow.domain.industry}}  
**Date:** {{date}}  
**Harness Version:** 1.3.0  
**Artifact type:** Executive High-Level Design (leadership audience)  
**Author:** {{author}}

---

## 1. Executive Summary

{{3-5 sentences in business language for leadership audience: business problem, operating impact, recommended architecture in plain words, expected value outcomes, and top risks/controls}}

---

## 2. Domain, Goal & Current Challenges

| Attribute | Value |
|-----------|-------|
| Industry / domain | {{flow.domain.industry}} |
| Sub-domain | {{flow.domain.sub_domain}} |
| Problem today | {{flow.domain.problem_statement}} |
| Goal | {{flow.domain.goal}} |

### Pain Points

- {{pain_point}}

### Current Challenges

- {{challenge}}

---

## 2A. Business Problem Statement

{{Clearly describe the business domain, who experiences the problem, why the current process is costly/slow/risky, and why leadership should care. Avoid generic chatbot wording.}}

---

## 3. Actors & Business Flow

### 3.1 Actors

| Actor | Type | Role |
|-------|------|------|
| {{name}} | {{type}} | {{role}} |

### 3.2 Trigger

{{flow.trigger}}

### 3.3 Steps

| Step | Actor | Action | Task Types | Systems | Approval? |
|------|-------|--------|------------|---------|-----------|
| S1 | | | | | |

### 3.4 Success Criteria

- {{criterion}}

### 3.5 Failure Modes (must never happen)

- {{failure_mode}}

---

## 4. Scenarios

### 4.1 Sunny Day (Happy Path)

| ID | Name | Frequency | Expected Outcome |
|----|------|-----------|------------------|
| SD1 | | | |

{{narrative per scenario}}

### 4.2 Rainy Day (Edge / Failure)

| ID | Name | Frequency | Severity | Desired Agent Behavior | Human Required? |
|----|------|-----------|----------|------------------------|-----------------|
| RD1 | | | | | |

---

## 5. Region, Network, Regulatory & Compliance

| Attribute | Value |
|-----------|-------|
| Region(s) | {{flow.region_network.regions}} |
| Data residency required | {{flow.region_network.data_residency_required}} |
| Residency region(s) | {{flow.region_network.residency_regions}} |
| Network topology | {{flow.region_network.network_topology}} |
| Egress restrictions | {{flow.region_network.egress_restrictions}} |
| Data classification | {{flow.regulatory_compliance.data_classification}} |
| Regulatory frameworks | {{flow.regulatory_compliance.frameworks}} |
| Audit trail | {{flow.regulatory_compliance.requirements.audit_trail}} |
| Approved vendors | {{flow.regulatory_compliance.approved_vendors}} |

### Compliance Impact on Design

{{how GDPR/HIPAA/PCI etc. affect hosting, model choice, memory retention, and tool access}}

---

## 6. Traffic Profile

| Attribute | Value |
|-----------|-------|
| Daily interactions (avg) | {{flow.traffic.daily_interactions}} |
| Peak hour volume | {{flow.traffic.peak_hour_volume}} |
| Peak concurrent | {{flow.traffic.peak_concurrent}} |
| Peak factor | {{flow.traffic.peak_factor}}× |
| 6-month growth estimate | {{flow.traffic.growth_6mo}} |
| Latency expectation | {{flow.traffic.latency_expectation}} |

---

## 7. Process Nuances

| Attribute | Value |
|-----------|-------|
| Process KPIs (business) | {{process_nuances.business_kpis}} |
| Third-party vendors | {{process_nuances.third_party_vendors}} |
| Criticality map (low/med/high) | {{process_nuances.criticality}} |
| Latency-sensitive steps | {{process_nuances.low_latency_steps}} / {{process_nuances.high_latency_tolerance_steps}} |
| Existing documentation | {{process_nuances.documentation}} |
| Existing knowledge base | {{process_nuances.knowledge_base}} |
| External users / customers | {{process_nuances.external_users}} |

---

## 8. Design Pattern

| Attribute | Value |
|-----------|-------|
| Operating model (plain language) | {{pattern.business_name}} |
| Technical pattern reference (optional) | {{pattern.id}} |
| Pattern Name | {{pattern.name}} |
| Complexity | {{pattern.complexity}} |
| HITL overlay | {{pattern.overlays.hitl}} |
| Sync / Async | {{pattern.execution.sync_async}} |
| Orchestration | {{pattern.execution.orchestration}} |
| Agent communication | {{pattern.execution.communication}} |
| Business rationale | {{pattern.business_rationale}} |
| Technical rationale | {{pattern.rationale}} |

### 8.1 Resilience

| Attribute | Value |
|-----------|-------|
| Circuit breaker on tools | {{pattern.resilience.circuit_breaker_on_tools}} |
| Retry policy | {{pattern.resilience.retry_policy}} |
| LLM timeout (ms) | {{pattern.resilience.timeouts.llm_call_ms}} |
| Tool timeout (ms) | {{pattern.resilience.timeouts.tool_call_ms}} |
| End-to-end SLA (ms) | {{pattern.resilience.timeouts.end_to_end_ms}} |

### 8.2 Solution Overview (diagram first — required)

> **Harness rule:** Solution Overview **must open with a diagram** (block flow or agentic flow). Prose follows the diagram.

```mermaid
{{solution_overview_diagram}}
```

**Diagram intent (one sentence):** {{diagram_caption}}

#### Plain-language architecture

{{pattern.business_architecture_narrative}}

#### Safety-first ordering

1. {{safety_step_1}}
2. {{safety_step_2}}
3. {{safety_step_3}}
4. {{safety_step_4}}

#### Autonomy / confidence (measurable)

| Signal | Auto-resolve allowed when | Else |
|--------|---------------------------|------|
| Amount / consequence | {{amount_rule}} | Human approval |
| Confidence / quality score | {{confidence_definition}} | Human approval or clarify |
| Policy ambiguity | Never auto-resolve | Human approval |

#### Critic / quality node (required if named in operating model)

| Attribute | Value |
|-----------|-------|
| Trigger | {{critic.trigger}} |
| Pass criteria | {{critic.pass}} |
| Fail path | {{critic.fail}} |
| Model class | {{critic.model_class}} |
| Latency / cost note | {{critic.cost_note}} |

#### Supervisor topology

| Choice | Value |
|--------|-------|
| One shared vs separate instances | {{supervisor.topology}} |
| Rationale | {{supervisor.rationale}} |

---

## 9. KPI Profile

| KPI | Weight (1-5) | Normalized | Rationale |
|-----|--------------|------------|-----------|
| K01 Quality | | | |
| K02 Reasoning | | | |
| K03 Latency | | | |
| K04 Throughput | | | |
| K05 Context | | | |
| K06 Cost | | | |
| K07 Privacy | | | |
| K08 Multimodal | | | |
| K09 Tool Use | | | |
| K10 Availability | | | |

**Hosting bias:** {{kpi_profile.derived.hosting_bias}}

---

## 10. Model Recommendations (Benchmark-Aware)

**Selection method:** 55% benchmark fit + 35% KPI + 10% compliance  
**Pricing / benchmark verification date:** {{pricing_verified_date}}  
Cite vendor pricing and independent leaderboards by URL in §25 (e.g. Artificial Analysis, LMArena, Hugging Face Open LLM Leaderboard) — do not cite harness markdown as evidence.

### 10.1 Task Profile & Weights

| Task Type | Weight | Benchmarks Referenced |
|-----------|--------|----------------------|
| tool_use | | BFCL, τ-bench |
| reasoning | | GPQA, MMLU-Pro |

### 10.2 Model Ranking

| Rank | Model | Benchmark | KPI | Compliance | Composite |
|------|-------|-----------|-----|------------|-----------|
| 1 | | | | | |

| Role | Model | Tier | Hosting | Composite Score |
|------|-------|------|---------|-----------------|
| Primary | | | | |
| Fallback | | | | |
| Economy | | | | |
| Embedding (if RAG) | | | | |
| Orchestrator (if multi-agent) | | | | |

### 10.3 Per-Step Model Map

| Step | Action | Task Types | Recommended Model | Benchmark Score |
|------|--------|------------|-------------------|-----------------|
| S1 | | | | |

### 10.4 Rainy Day Coverage

| Scenario | Covered? | Gap / Mitigation |
|----------|----------|------------------|
| RD1 | ✓/✗ | |

> **Disclaimer:** Benchmark scores are design-time proxies. Validate with eval on your sunny/rainy scenarios before production.

---

## 11. Hosting Decision

| Attribute | Value |
|-----------|-------|
| Mode | {{hosting.mode}} |
| Rationale | {{hosting.rationale}} |

---

## 12. Infrastructure & Cost

### 12a. Self-Hosted (if applicable)

| Attribute | Value |
|-----------|-------|
| Model | |
| GPU config | |
| Replicas (avg / peak) | |
| Monthly infra (range) | $ |

### 12b. API Cost (if applicable)

| Scenario | Daily Volume | Monthly USD |
|----------|--------------|-------------|
| Average day | | |
| Peak day | | |

---

## 13. Tools & MCP Integration

| Tool | Type (MCP/API) | Build/Buy | Auth | Read/Write | Used By Step |
|------|----------------|-----------|------|------------|--------------|
| | | | | | |

**MCP strategy:** {{tools.mcp_strategy}}  
**Tool server deployment:** {{tools.deployment_notes}}

---

## 14. Memory Strategy

| Agent / Scope | Pattern | Store | Retention | Compliance Notes |
|---------------|---------|-------|-----------|------------------|
| | session / episodic / semantic | | | |

---

## 15. Knowledge Base & Context Management

| Attribute | Value |
|-----------|-------|
| Strategy | none / vector_rag / graphrag / ontology / hybrid |
| Existing corpus | {{knowledge.existing}} |
| Embedding model | {{knowledge.embedding_model}} |
| Chunk / index strategy | {{knowledge.index_strategy}} |
| Token optimization | compaction / caching / retrieve-only |
| Citations required | yes / no |

---

## 16. Agent Framework

| Attribute | Value |
|-----------|-------|
| Primary framework | {{framework.primary}} |
| Rationale | {{framework.rationale}} |
| Kagent platform path | {{framework.kagent_platform_path}} |
| Alternatives considered | {{framework.alternatives}} |

---

## 17. Guardrails

| Guardrail | Enabled | Mechanism |
|-----------|---------|-----------|
| Cost budget | | |
| PII redaction | | |
| Prompt injection defense | | |
| LLM load balancing | | |
| Acceptable use policy | | |

---

## 18. Security

| Area | Design |
|------|--------|
| Protocol (mTLS, HTTPS) | |
| Secrets management | |
| Certificates / tokens | |
| Data protection (at rest / in transit) | |
| Tool authorization | |

---

## 19. Observability

| Layer | Signals | Stack |
|-------|---------|-------|
| Metrics | latency, tokens, tool errors, cost/flow | |
| Logs | structured steps, redacted tool I/O | |
| Traces | OTel spans LLM → tool → sub-agent | |

**Dashboards:** {{observability.dashboards}}  
**Alerts:** {{observability.alerts}}

---

## 20. Value KPIs & Business Success Metrics

| Business KPI | Agent Metric | Measurement | Data Source | Target |
|--------------|--------------|-------------|-------------|--------|
| | | | | |

**Dashboard consumers:** {{value_kpis.consumers}}

---

## 20A. Delivery Approach, Timeline, Cost, and Effort

| Phase | Scope | Timeline | Outcome |
|-------|-------|----------|---------|
| Phase 0 | | | |
| Phase 1 | | | |
| Phase 2 | | | |

| Workstream | Best Case | Likely | Worst Case |
|-----------|-----------|--------|------------|
| Discovery / design | | | |
| Integration build | | | |
| Security / guardrails | | | |
| Evaluation / dashboards | | | |

| Cost Area | Low | Likely | High |
|-----------|-----|--------|------|
| Inference | | | |
| Integration / platform | | | |
| Evaluation / observability | | | |
| Delivery team | | | |

---

## 20B. Team and Skills Required

| Role | Count | Why Needed |
|------|-------|------------|
| Product manager | | |
| Architect | | |
| AI / agent engineer | | |
| Backend engineer | | |
| Data / eval engineer | | |
| Security engineer | | |
| Operations SME | | |

---

## 21. Loop Engineering

| Loop | Enabled | Details |
|------|---------|---------|
| Human feedback | | |
| HITL approval gates | | |
| Eval / golden suite | | |
| Continuous improvement | cadence, owner | |
| Cost feedback | | |

---

## 21A. Evolution and Feedback Mechanism

{{Explain how the agentic capability evolves over time: pilot → selective automation → broader scope → self-serve or scaled platform. Include business, operational, and engineering feedback loops plus governance cadence.}}

---

## 22. Online Architecture Recommendations

- Model router: {{yes/no — strategy}}
- Prompt caching: {{yes/no}}
- Fallback chain: Primary → Fallback → Economy
- Guardrails: {{for rainy day / compliance}}
- Observability: OTel + cost dashboard

---

## 23. Risks, Assumptions & Open Questions

| Risk | Mitigation | Owner | Trigger |
|------|------------|-------|---------|
| Benchmark proxy ≠ your data | Run eval on SD1–SDn and RD1–RDn scenarios | | |
| Peak traffic underestimated | Load test at peak_factor × avg | | |
| Compliance gap | Legal review of vendor DPAs | | |
| KB staleness | Re-index triggers defined | | |

### Open Decisions for Business Owners

- {{open_question}}

### Recommended defaults (Assumption — planning default)

| Decision | Assumed default | Reasoning | Validate with |
|----------|-----------------|-----------|---------------|
| {{q}} | {{default}} | {{why}} | {{owner}} |

### Eval Checklist (Pre-Production)

- [ ] Execute each **sunny day** scenario — pass threshold: {{}}%
- [ ] Execute each **rainy day** scenario — correct escalation behavior
- [ ] Measure actual tokens/flow vs estimate
- [ ] Compliance sign-off for selected hosting
- [ ] Tool write operations reviewed

---

## 24. Next Steps

- [ ] Validate assumed defaults with product / risk / compliance
- [ ] POC with primary model on SD1
- [ ] Stress-test RD scenarios
- [ ] Procurement / GPU sizing validation
- [ ] If Kagent selected → run **kagent-design-harness** on this artifact
- [ ] Implement observability dashboards and value KPI baselines

---

## 25. References & Evidence Register

> Tags: **Primary** | **Secondary** | **Assumption**  
> **Citation rule:** Primary/Secondary sources must be external credible URLs (industry case study, white paper, research paper, standards body, or vendor eng write-up).  
> Never cite harness paths (`references/*.md`, skill files). If research used an offline curated pack, cite the original web `source_url` the pack was curated from.

| Design choice / KPI | Evidence type | Source (https URL) |
|---------------------|---------------|--------------------|
| {{decision}} | Primary / Secondary / Assumption | {{https://...}} |

**Provenance:** State whether a live stakeholder interview was conducted, or that the flow was reconstructed from public patterns + assumptions.

---

## Appendix A — Interview Coverage Matrix

Map harness Step 1 Blocks A–H (and note Steps 5–8 interview gaps).

| Block | Topic | Blueprint section | Status (✅ / ⚠️ / ❌ / 🔶 Assumption) |
|-------|-------|-------------------|--------------------------------------|
| A | Domain / problem / goal | | |
| B | Actors / systems | | |
| C | Sunny scenarios | | |
| D | Rainy scenarios | | |
| E | Volume / latency | | |
| F | Region / compliance | | |
| H | Process nuances | | |
| G | Flow synthesis confirmed | | |

---

## Appendix B — Engineering Mapping

- Router / specialist topology
- Safety-first ordering
- Configurable vs specialized (by phase)
- Durable multi-turn state + retention
- Observability and evaluation integration

---

## Appendix — Glossary

| Term | Definition |
|------|------------|
| Sunny day | Typical happy-path scenario |
| Rainy day | Edge case, failure, or abuse scenario |
| Composite score | Blended benchmark + KPI + compliance score |
| MCP | Model Context Protocol — standardized tool interface for agents |
| Assumption — planning default | Unconfirmed default used for sizing; must be validated before build |
