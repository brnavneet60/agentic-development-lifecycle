# Agentic AI Design Artifact

**Flow:** {{flow.display_name}}  
**Domain:** {{flow.domain.industry}}  
**Date:** {{date}}  
**Harness Version:** 1.0.0  
**Author:** {{author}}

---

## 1. Executive Summary

{{3-5 sentences: domain problem, pattern, primary model with benchmark rationale, tools/MCP approach, framework, hosting, cost/compute range, key guardrails}}

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
| Pattern ID | {{pattern.id}} |
| Pattern Name | {{pattern.name}} |
| Complexity | {{pattern.complexity}} |
| HITL overlay | {{pattern.overlays.hitl}} |
| Sync / Async | {{pattern.execution.sync_async}} |
| Orchestration | {{pattern.execution.orchestration}} |
| Agent communication | {{pattern.execution.communication}} |
| Rationale | {{pattern.rationale}} |

### 8.1 Resilience

| Attribute | Value |
|-----------|-------|
| Circuit breaker on tools | {{pattern.resilience.circuit_breaker_on_tools}} |
| Retry policy | {{pattern.resilience.retry_policy}} |
| LLM timeout (ms) | {{pattern.resilience.timeouts.llm_call_ms}} |
| Tool timeout (ms) | {{pattern.resilience.timeouts.tool_call_ms}} |
| End-to-end SLA (ms) | {{pattern.resilience.timeouts.end_to_end_ms}} |

### 8.2 Agent Topology

```
{{ascii_topology_diagram}}
```

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
**Trusted sources:** {{pricing_verified_date}} — see `references/trusted-sources/TRUSTED-SOURCES.md`

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

## 21. Loop Engineering

| Loop | Enabled | Details |
|------|---------|---------|
| Human feedback | | |
| HITL approval gates | | |
| Eval / golden suite | | |
| Continuous improvement | cadence, owner | |
| Cost feedback | | |

---

## 22. Online Architecture Recommendations

- Model router: {{yes/no — strategy}}
- Prompt caching: {{yes/no}}
- Fallback chain: Primary → Fallback → Economy
- Guardrails: {{for rainy day / compliance}}
- Observability: OTel + cost dashboard

---

## 23. Risks, Assumptions & Open Questions

| Risk | Mitigation |
|------|------------|
| Benchmark proxy ≠ your data | Run eval on SD1–SDn and RD1–RDn scenarios |
| Peak traffic underestimated | Load test at peak_factor × avg |
| Compliance gap | Legal review of vendor DPAs |
| KB staleness | Re-index triggers defined |

### Open Questions for Stakeholders

- {{open_question}}

### Eval Checklist (Pre-Production)

- [ ] Execute each **sunny day** scenario — pass threshold: {{}}%
- [ ] Execute each **rainy day** scenario — correct escalation behavior
- [ ] Measure actual tokens/flow vs estimate
- [ ] Compliance sign-off for selected hosting
- [ ] Tool write operations reviewed

---

## 24. Next Steps

- [ ] POC with primary model on SD1
- [ ] Stress-test RD scenarios
- [ ] Procurement / GPU sizing validation
- [ ] If Kagent selected → run **kagent-design-harness** on this artifact
- [ ] Implement observability dashboards and value KPI baselines

---

## Appendix — Glossary

| Term | Definition |
|------|------------|
| Sunny day | Typical happy-path scenario |
| Rainy day | Edge case, failure, or abuse scenario |
| Composite score | Blended benchmark + KPI + compliance score |
| MCP | Model Context Protocol — standardized tool interface for agents |
