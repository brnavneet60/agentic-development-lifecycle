# Agentic Technical Design Harness

An [Agent Harness](https://agentharnesses.io/home) that turns a **High-Level / executive requirement summary** into a production-oriented **Technical Design Document (TDD)** for agentic AI systems — cloud-native and intended to run on **Kubernetes**.

It is built for [Agent Skills](https://agentskills.io/home)–compatible clients (for example Cursor). Open this folder as the harness root, then ask the agent to run the design workflow.

---

## What this harness does

You bring a business or product requirement (or an executive HLD). The harness acts as an **Agentic AI Technical Architect** and walks a gated, multi-step design process. It prefers an offline **knowledge base** first, then escalates to live primary sources when pricing, versions, or evidence must be current.

It does **not** generate production application code or deploy manifests. It produces a **Next-Level Design (NLD)** that Platform, Product, and engineering can use to plan build slices, evaluate stack choices, and hand off to implementation.

---

## What output it creates

A single markdown **Technical Design Document** covering, at minimum:

| Area | What you get |
|------|----------------|
| **Component selection & patterns** | Agency ladder (code → workflow → RAG → agent), single vs multi-agent, orchestration, hand-offs, sliced MVP with exit gates |
| **Agent frameworks** | Production vs prototype recommendation (e.g. LangGraph vs lighter SDKs) with rejected alternates |
| **Model selection** | Named models / API ids, dated cost notes, routing ladder (economy → specialist → escalation) |
| **Tools & MCP** | Tool inventory, REST vs MCP, least-privilege write binding |
| **Memory & context** | Knowledge vs memory planes, retention, token/context strategy |
| **KPIs & value** | Business and technical metrics (including tool recall / parameter accuracy) |
| **Observability** | Metrics, logs, traces (OpenTelemetry-aligned) |
| **Evaluation** | Offline golden sets, online/canary gates, adversarial checks |
| **Continuous improvement** | Feedback loops, kill switches, autonomy promotion |
| **Guardrails** | Autonomy slider (Manual / Ask / Agent), PII, injection, budgets, HITL failure modes |
| **Identity & access** | Workload identity, AuthZ matrix (including authorize vs execute) |
| **Trade-offs & K8s view** | Scalability, modularity, cost; namespaces, workloads, GitOps/canary intent |
| **Decision & evidence registers** | Chosen vs alternates, citations to primary docs / standards / papers |

Default deliverable path (relative to the workspace where the agent runs):

```text
agents-output/agentic-technical-design-harness/<use-case-slug>/<use-case-slug>-technical-design.md
```

---

## How to run (any Cursor / Skills-compatible agent)

1. Clone or download this repository (or this harness directory).
2. Open the **harness root** in your AI client (the folder that contains `HARNESS.md`).
3. Point the agent at this prompt (adapt the requirement):

```text
Using agentic-technical-design-harness, read OUTPUT-STANDARDS.md, HARNESS.md,
and references/knowledgebase.md. Then produce a technical design for:
[paste or attach your High-Level requirement summary].

Run Steps 1–14 with checkpoint confirmations. Deliver only if the
OUTPUT-STANDARDS P0 quality checklist passes.
```

4. Confirm checkpoints when the agent pauses (requirements, topology, models/tools/memory, eval/loops, guardrails/identity).

---

## Design principles (enforced)

| Principle | Meaning |
|-----------|---------|
| Ask, don't assume | Gaps become questions; planning defaults are labeled |
| Knowledgebase-first | Use `references/knowledgebase.md` before live fetch |
| Sequence ≠ end-state | Sliced MVP first; full multi-agent topology is target state |
| Propose → authorize → execute | Non-LLM policy gate for irreversible / money actions |
| Evidence-backed | Full `https://` citations (and book title + chapter for the knowledge base) |
| Accept-quality or don't deliver | Pass `OUTPUT-STANDARDS.md` P0 checklist before publish |

---

## Layout

| Path | Role |
|------|------|
| `HARNESS.md` | Role, workflow, routing |
| `OUTPUT-STANDARDS.md` | Required sections and quality bar |
| `config/harness.config.yaml` | References, deliverers, skill metadata |
| `skills/` | Built-in + domain skills (Steps 1–14) |
| `references/knowledgebase.md` | Primary offline design brain |
| `references/` | Offline stubs + online source index |
| `outputs/templates/default.md` | TDD template |
| `docs/e2e-requirement.txt` | Original E2E section requirements |
| `docs/RELATIONSHIP.md` | How this relates to an executive HLD harness |

---

## Workflow (Steps 1–14)

| Step | Skill |
|------|-------|
| 1 | `clarify-requirements` |
| 2 | `design-components-patterns` |
| 3 | `select-models` |
| 4 | `design-tools-mcp` |
| 5 | `design-memory` |
| 6 | `design-context-management` |
| 7 | `define-value-kpis` |
| 8 | `design-observability` |
| 9 | `design-evaluation` |
| 10 | `design-continuous-improvement` |
| 11 | `design-guardrails` |
| 12 | `design-identity-access` |
| 13 | `select-agent-framework` |
| 14 | `generate-technical-design` |

Built-ins used throughout: `resolve-reference`, `fetch-online`, `deliver-output`.

---

## Extending

Edit `config/harness.config.yaml` to add references or deliverers, then update `references/REFERENCES.md` and `outputs/OUTPUTS.md` to match.

---

## Specs

- [Agent Harnesses](https://agentharnesses.io/home)
- [Agent Skills](https://agentskills.io/home)
