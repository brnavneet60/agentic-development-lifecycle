# kaif-design

**GitHub:** [https://github.com/brnavneet60/kaif-design](https://github.com/brnavneet60/kaif-design)

Design harnesses for **KAIF** (Kubernetes Agentic AI Fabric) — the module that turns a business use case into evidence-backed agentic design **before** anyone builds or deploys on Kubernetes.

This repository does **not** ship production agents, cluster manifests, or runtime operators. It ships **repeatable design workflows** (prompt/skills harnesses) that produce leadership and technical design documents.

---

## Where this sits in KAIF

KAIF is organized as seven shippable modules across Development · Deployment · Evaluation. **kaif-design** is the design module:

| Module | Role |
|--------|------|
| **kaif-platform** | Cluster substrate, GitOps, observability spine |
| **kaif-design** (this repo) | Offline (+ later online) harnesses for pattern, model, tools, memory, security, eval, and trade-offs |
| **kaif-deploy** | Operators, packaging, rollout |
| **kaif-eval** | Eval spine across design / build / deploy / runtime |
| **kaif-guard** | Admission, request-time, and runtime guardrails |
| **kaif-value** | Cost, KPIs, exec reporting |
| **kaif-identity** | Workload and user identity, scopes, isolation |

**Working rule (KAIF):** a feature is “done” only when an agent has flowed through it on a real cluster with evidence. Design is the first gate — if the operating model and controls are wrong, faster coding only accelerates the wrong system.

---

## What this repository contains

```text
kaif-design/
├── README.md                          ← you are here
├── agentic-design-harness/            ← First-Level Design (FLD) — executive HLD
└── agentic-technical-design-harness/  ← Next/Deep design — technical TDD (K8s-oriented)
```

### 1. `agentic-design-harness` — executive High-Level Design

Produces a **leadership-ready High-Level Design (HLD)** from a business flow:

- Problem, decisions with business rationale, operating model, KPIs, delivery, risk, evidence
- Diagram-first Solution Overview
- Human checkpoints; journaled steps and revisions
- Configurable sources (trusted URLs + offline packs + local knowledge base)

**Audience:** executives, PMs, architects, risk/compliance.  
**Stops at:** design approval — not implementation.

See [`agentic-design-harness/README.md`](./agentic-design-harness/README.md) and [`OUTPUT-STANDARDS.md`](./agentic-design-harness/OUTPUT-STANDARDS.md) (v1.2).

### 2. `agentic-technical-design-harness` — Technical Design Document

Takes an executive HLD (or equivalent requirement summary) and produces a **Technical Design Document (TDD)** oriented to cloud-native / Kubernetes delivery:

- Agency ladder, topology, frameworks, models, tools/MCP, memory, eval, guardrails, identity, K8s view
- Knowledgebase-first research with primary-source evidence rules
- Checkpointed multi-step architect workflow

**Audience:** platform, product, and engineering leads planning build slices.  
**Stops at:** implementable design — not production code or deploy manifests.

See [`agentic-technical-design-harness/README.md`](./agentic-technical-design-harness/README.md).

### How the two harnesses connect

```text
Business use case
       │
       ▼
agentic-design-harness  →  executive HLD (FLD)
       │
       ▼
agentic-technical-design-harness  →  technical TDD (NLD → DLD handoff)
       │
       ▼
kaif-deploy / implementation path  →  build & run on Kubernetes
```

---

## What we have done so far

As of **2026-07-23**, this repo ships **two runnable design harnesses**:

| Harness | Purpose | Available today |
|---------|---------|-----------------|
| **`agentic-design-harness`** | Business → executive HLD (FLD) | Full 10-step skill workflow · four config files (sources, context, journal, parallel) · `OUTPUT-STANDARDS` v1.2 · artifact template · offline reference packs · local Albada knowledge base · trusted/curation URL maps · journal + revision skills |
| **`agentic-technical-design-harness`** | Executive HLD → technical TDD (NLD/DLD handoff) | Multi-step technical architect workflow · `OUTPUT-STANDARDS` · knowledgebase-first research · skills for components, models, tools, memory, eval, guardrails, identity, K8s view · checkpoint gates |

**Shared characteristics already in place:**

- Prompt / Agent Skills orchestration (Cursor and compatible tools)
- Ask-don’t-assume checkpoints
- Evidence discipline (external URLs; offline packs are lookup only)
- Design-only scope — no production agent code or cluster deploy from this repo

**Not available yet in this repo:** online design harness (live behavior feedback), automated bootstrap/validator CLI, curation job runner, or post-design eval CLI (that belongs with **kaif-eval**).

---

## Roadmap

Aligned with the KAIF execution plan (**kaif-design** in P1 offline → P3 online) and the harness maturity roadmaps.

### Near term (harden what we have)

| Priority | Work | Outcome |
|----------|------|---------|
| P0 | Bootstrap / config validator for both harnesses | Reproducible run start without ad-hoc setup |
| P0 | Journal rollup enforcement | Traceability without relying on chat memory |
| P1 | Tighten HLD → TDD handoff contract | Executive artifact feeds technical design cleanly |
| P1 | Offline pack depth + one curation job runner | Fresher models/pricing/patterns with provenance |

### Medium term (integrate the KAIF spine)

| Priority | Work | Outcome |
|----------|------|---------|
| P2 | Design-time checklist export for **kaif-eval** | Golden scenarios and gates from HLD/TDD |
| P2 | Explicit constraints engine (`constraints.yaml`) | Pre-flight before final artifact generation |
| P2 | Optional parallel research waves | Faster mid-pipeline research without losing journal merge |
| P3 | **Online** design harness slice | Compare design decisions against live behavior (KAIF P3) |

### Later (platform path)

| Priority | Work | Outcome |
|----------|------|---------|
| Downstream | Hand off TDD to **kaif-deploy** / implementation harnesses | Agents on real Kubernetes with evidence |
| Downstream | Wire value KPIs into **kaif-value** | Design targets become measurable dashboards |

---

## How to use this repo

1. Clone [kaif-design](https://github.com/brnavneet60/kaif-design).
2. Open the harness you need (`agentic-design-harness` or `agentic-technical-design-harness`) in Cursor or another Agent Skills–compatible tool.
3. Follow that harness’s README activation prompt; confirm checkpoints; journal revisions.
4. Write design outputs to a path you choose for the run (configurable per project).

---

## Principles we keep

- Ask; don’t invent compliance, volume, or integrations.
- Evidence over anecdote — external `https://` citations in registers.
- Business language for executive design; engineering depth for technical design.
- Progressive autonomy and least privilege for money-moving / irreversible actions.
- Design first — then code on the drawing board’s terms.

---

## License / disclaimer

Harness reference catalogs (pricing, benchmarks, sizing) are **indicative**. Verify against vendor and standards sources before procurement or production commitments.
