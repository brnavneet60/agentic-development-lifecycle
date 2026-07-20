---
name: capture-business-flow
description: Structured interview to capture domain, actors, sunny/rainy day scenarios, challenges, goals, region, network, regulatory and compliance constraints, then structure the business flow. Use as Step 1 when designing agentic AI from a business process.
compatibility: Offline. No external APIs.
metadata:
  harness: agentic-design-harness
  step: 1
  version: "1.0.0"
---

# Capture Business Flow

## Purpose

Run a **structured discovery interview** before designing anything. Convert answers into a rich flow document that downstream skills use for pattern selection, KPI weighting, and **benchmark-aware model selection**.

Do **not** infer or invent answers. Ask the user explicitly for each section below.

## Interview Protocol

Conduct the interview in **seven blocks** (A–G + H). Present one block at a time; allow the user to answer in batch if they prefer.

Pause after Block H for full confirmation before proceeding to `classify-design-pattern`.

---

### Block A — Domain & Goal

Ask:

1. **Domain** — What industry/domain is this? (e.g. telecom billing, healthcare claims, e-commerce fulfillment, internal IT ops)
2. **Problem statement** — What is broken, slow, or manual today?
3. **Goal** — What outcome do you want the agentic solution to achieve? (measurable if possible)
4. **What you want to solve** — Top 1–3 pain points this agent must address
5. **Current challenges** — What have you tried? What failed? Constraints from legacy systems, team skills, timeline?

```
VALIDATE:
  IF domain is empty: ASK — do not proceed
  IF goal is vague ("make it better"): ASK for measurable outcome
  IF no pain points listed: ASK "What happens if you do nothing?"
```

---

### Block B — Actors & Systems

Ask:

6. **Actors** — Who/what participates? (human roles, external parties, upstream/downstream systems)
7. **Trigger** — What event or request starts the flow?
8. **Systems touched** — CRM, ERP, databases, APIs, messaging, ticketing, etc.
9. **Human touchpoints** — Where do humans intervene today? Where must they stay in the loop?

For each actor capture: `name`, `type` (human | system | external), `role_in_flow`.

---

### Block C — Sunny Day Scenarios (Happy Path)

Ask:

10. **Sunny day scenarios** — Describe 1–3 typical successful flows end-to-end.
    - What does the user/request look like?
    - What steps happen?
    - What is the ideal outcome?
    - How often does this occur? (% of total volume or daily count)

For each scenario capture:

```yaml
- id: SD1
  name: "<short name>"
  description: "<narrative>"
  frequency: "<e.g. 70% of requests, 200/day>"
  expected_outcome: "<success definition>"
  estimated_steps: <int>
```

```
VALIDATE:
  IF sunny_day_scenarios.count < 1: ERROR "Need at least one happy-path scenario"
  RECOMMEND 2-3 scenarios for representative coverage
```

---

### Block D — Rainy Day Scenarios (Edge, Failure, Abuse)

Ask:

11. **Rainy day scenarios** — What can go wrong? Include:
    - Missing or incomplete data
    - Ambiguous user intent
    - System timeouts / downstream failures
    - Policy exceptions
    - Fraud or abuse attempts
    - Regulatory edge cases
    - Escalation to human

For each scenario capture:

```yaml
- id: RD1
  name: "<short name>"
  description: "<what goes wrong>"
  frequency: "<e.g. 15% of requests>"
  severity: low | medium | high | critical
  current_handling: "<how handled today>"
  desired_agent_behavior: "<escalate / retry / refuse / partial completion>"
  requires_human: true | false
```

```
VALIDATE:
  IF rainy_day_scenarios.count < 1: WARN "No edge cases — agent may be under-specified"
  IF any severity == critical AND requires_human == false: FLAG for HITL review in Step 2
```

---

### Block E — Traffic & Operations

Ask:

12. **Volume** — Average daily/monthly interactions through this flow
13. **Peak traffic** — Peak hour volume, peak concurrent users/sessions
14. **Peak factor** — How much higher is peak vs average? (e.g. 10× at month-end)
15. **Growth** — Expected volume in 6–12 months
16. **Latency expectation** — Real-time chat, minutes, batch overnight?
17. **Availability** — Dev/POC vs production SLA (99%, 99.9%, etc.)

---

### Block F — Region, Network, Regulatory & Compliance

Ask:

18. **Region(s)** — Where do users and data reside? (e.g. EU, US, APAC, multi-region)
19. **Data residency** — Must data stay in a specific country/region?
20. **Network** — Internet-only, private cloud, on-prem, air-gapped, hybrid? Any egress restrictions?
21. **Data classification** — Public, internal, PII, PHI, PCI, trade secrets?
22. **Regulatory frameworks** — GDPR, HIPAA, PCI-DSS, SOX, DORA, industry-specific?
23. **Compliance requirements** — Audit trail, retention, right-to-erasure, model logging prohibitions?
24. **Approved vendors** — Are OpenAI/Anthropic/Google allowed, or only self-hosted/on-prem?

```
VALIDATE:
  IF regulated frameworks listed AND approved_vendors == "self-hosted only":
    SET flow.constraints.hosting = SELF_HOSTED_MANDATORY
  IF air_gapped OR no_egress:
    SET flow.constraints.network = AIR_GAPPED
  IF multi_region:
    FLAG data_residency per region in output
```

---

### Block H — Process Nuances (E2E Goals)

Ask (do **not** assume):

25. **How is it done today?** — Manual steps, spreadsheets, call center scripts, existing automation?
26. **Resources used** — People, systems, documents, external services per stage
27. **Business KPIs** — How is the *process* measured today? (CSAT, AHT, error rate, revenue, SLA breach %)
28. **Third-party interfaces** — Payment gateways, regulators, partners, SaaS APIs — list each
29. **Criticality map** — Which steps are low / medium / high criticality if they fail?
30. **Latency map** — Which steps need sub-second, seconds, minutes, or batch?
31. **Existing documentation** — Runbooks, Confluence, policy PDFs, training materials, APIs specs?
32. **Existing knowledge base** — Wiki, vector DB, ontology, ticket history — or none?
33. **External users** — Do customers or partners outside the org interact with this flow?

```yaml
process_nuances:
  current_state: "<narrative>"
  resources_by_stage:
    - stage: S1
      people: []
      systems: []
      documents: []
  business_kpis_today:
    - name: "<e.g. first-contact-resolution>"
      target: "<value or unknown>"
      owner: "<team>"
  third_party_interfaces:
    - name: ""
      type: api | portal | file | manual
      sla: ""
  criticality:
    - step_id: S1
      level: low | medium | high
      impact_if_fail: ""
  latency:
    - step_id: S1
      requirement: realtime | seconds | minutes | batch
  documentation_available:
    - type: runbook | policy | api_spec | training
      location: ""
      quality: poor | partial | good
  knowledge_base_existing: true | false
  knowledge_base_detail: "<if true: type, coverage, freshness>"
  external_users: true | false
  external_user_types: ["customer", "partner"]
```

```
VALIDATE:
  IF business_kpis_today empty: ASK "How will you know the agent succeeded?"
  IF third_party_interfaces unknown AND flow touches payments/compliance: ASK again
  IF documentation_available empty AND needs_knowledge_retrieval likely: FLAG for Step 6
```

---

### Block G — Flow Steps (Synthesize)

After Blocks A–H, synthesize an **ordered step list** from sunny day scenarios (and note which rainy day scenarios attach to which step).

Ask: **"Here is the step sequence I derived — correct? Anything missing?"**

---

## Structured Output

Emit this complete structure:

```yaml
flow:
  name: "<slug>"
  display_name: "<Human Name>"

  domain:
    industry: "<e.g. telecommunications>"
    sub_domain: "<e.g. order-to-cash>"
    problem_statement: "<what is wrong today>"
    goal: "<measurable outcome>"
    pain_points:
      - "<pain 1>"
    current_challenges:
      - "<challenge 1>"

  actors:
    - name: "<actor>"
      type: human | system | external
      role: "<role in flow>"

  trigger: "<event>"
  steps:
    - id: S1
      actor: "<who>"
      action: "<what>"
      decision: true | false
      requires_approval: true | false
      systems: ["<system>"]
      task_types: ["<from task type taxonomy>"]  # see benchmark-matrix
      sunny_scenario_refs: [SD1]
      rainy_scenario_refs: [RD1]

  scenarios:
    sunny_day:
      - id: SD1
        name: ""
        description: ""
        frequency: ""
        expected_outcome: ""
    rainy_day:
      - id: RD1
        name: ""
        description: ""
        frequency: ""
        severity: low | medium | high | critical
        desired_agent_behavior: ""
        requires_human: true | false

  traffic:
    daily_interactions: <number or range>
    monthly_interactions: <number or range>
    peak_hour_volume: <number or unknown>
    peak_concurrent: <number or unknown>
    peak_factor: <float e.g. 10>
    growth_6mo: "<estimate>"
    latency_expectation: realtime | minutes | batch

  region_network:
    regions: ["EU", "US"]
    data_residency_required: true | false
    residency_regions: ["<where data must stay>"]
    network_topology: internet | private_cloud | on_prem | air_gapped | hybrid
    egress_restrictions: true | false

  regulatory_compliance:
    data_classification: public | internal | pii | phi | pci | regulated
    frameworks: ["GDPR", "PCI-DSS"]
    requirements:
      audit_trail: true | false
      retention_years: <n or null>
      pii_redaction: true | false
      model_logging_prohibited: true | false
    approved_vendors: any | openai | anthropic | google | self_hosted_only | private_endpoints_only

  data:
    sensitivity: public | internal | pii | regulated
    residency_required: true | false

  success_criteria:
    - "<criterion>"
  failure_modes:
    - "<what must never happen>"

  task_profile:
    # Derived: union of task_types across all steps — used by model-selection
    primary_task_types: ["reasoning", "tool_use"]
    secondary_task_types: ["classification"]
    multimodal_required: true | false

  signals_for_pattern:
    tool_count_estimate: <int>
    agent_count_estimate: <int>
    has_parallel_branches: true | false
    needs_knowledge_retrieval: true | false
    is_event_driven: true | false
    requires_human_approval: true | false
    rainy_day_severity_max: low | medium | high | critical
```

### Task Type Tagging (per step)

When synthesizing steps, tag each step with one or more task types from `references/benchmark-matrix/BENCHMARK-MATRIX.yaml`:

| Task Type | Use When Step Involves |
|-----------|------------------------|
| `classification` | Routing, intent, category assignment |
| `extraction` | Pull structured fields from documents/text |
| `reasoning` | Multi-step analysis, trade-offs, planning |
| `generation` | Draft emails, reports, summaries |
| `tool_use` | API/MCP calls, system integration |
| `rag_retrieval` | Search knowledge base, policy lookup |
| `code` | Write, review, or execute code |
| `multimodal_vision` | Images, PDFs, scans |
| `conversation` | Multi-turn dialogue with user |
| `planning` | Decompose goals, orchestrate sub-tasks |

---

## Confirmation Gate

Present a **summary table** to the user:

| Section | Captured? |
|---------|-----------|
| Domain & goal | ✓ |
| Actors | ✓ |
| Sunny day (n scenarios) | ✓ |
| Rainy day (n scenarios) | ✓ |
| Traffic & peak | ✓ |
| Region & network | ✓ |
| Regulatory & compliance | ✓ |
| Process nuances (KPIs, 3rd party, latency) | ✓ |
| Flow steps | ✓ |

Ask: **"Does this accurately represent your business flow and constraints? Any corrections?"**

Only proceed to `classify-design-pattern` after explicit confirmation.

## Negative Scenarios

| Scenario | Response |
|----------|----------|
| User gives only a one-liner | Run full interview Block A–F; do not skip |
| User wants code immediately | Phase 1 is design-only; complete interview first |
| Conflicting requirements (e.g. GDPR + send all data to US API) | Flag conflict; ask user to choose |
| User unsure of volume | Capture as "unknown"; note assumption in output |
| No compliance info for regulated domain | WARN and ask again before model selection |
