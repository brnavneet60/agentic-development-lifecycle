# Agentic Technical Design Harness — Output Standards

**Version:** 1.0.0  
**Date:** 2026-07-23  
**Quality baseline:** Accept-level NLD TDD (architecture seams + platform/PDM density)  
**Audience:** Product/PDM · Platform Architect · Solution / AI eng  
**Source:** `docs/e2e-requirement.txt` · `references/knowledgebase.md`

Every TDD run must meet this bar — not a thinner “first draft” shape.

---

## 1. Artifact role

| Stage | Doc | This harness produces |
|-------|-----|------------------------|
| FLD | Executive HLD (`agentic-design-harness`) | Input when available |
| **NLD** | **Technical Design Document** | **This output** |
| DLD | Deep/LLD + manifests | Downstream — out of scope |

The TDD is **not** production code and **not** an executive-only narrative.

---

## 2. Mandatory design brain

1. Load `references/knowledgebase.md` (resolve-reference id: `knowledgebase`) on every run.  
2. Apply book principles: workflows vs agents, parsimony, autonomy slider, Knowledge≠Memory, tool-level eval, HITL human factors, layered protection.  
3. In Evidence Register cite **book title + chapter** (Secondary) — never the local path alone.  
4. Also cite external `https://` primary/secondary sources for claims, peers, pricing, standards.

---

## 3. Hard boundaries (non-negotiable)

| Rule | Requirement |
|------|-------------|
| **Sequence ≠ end-state** | Build order is **sliced MVP** with exit gates. Full multi-agent topology is **target/end-state**, not Day-1 wiring — unless Product explicitly rejects slices in writing. |
| **Money / irreversible actions** | LM may **propose** only. A **non-LM policy-gate** (or equivalent deterministic authorizer) **authorizes**. A separate **executor** **executes**. Specialists never hold write credentials. |
| **Ask, don't assume** | Missing compliance, volumes, vendors, thresholds → open questions. Planning defaults labeled `Assumption — planning default`. |
| **Named models** | Concrete model names + API ids + dated pricing — not tier labels alone. |
| **Platform density** | AuthZ write matrix (with Authorize column), K8s workloads + resilience (HPA, PDB, circuit breakers, shard notes), full Evidence URLs. |
| **PDM density** | Epic → slice → exit gate → KPI table + prompt-pack ownership cadence. |

---

## 4. Language rules

### Do

- Ground every major decision in the **business use case**.
- For each decision: **justification**, **alternates**, **recommendation**.
- Separate **facts** / **assumptions** / **open questions**.
- Prefer mature cloud-native options with explicit tech evaluation.
- Date-stamp volatile facts (pricing, models, GA).
- Include HLD→TDD appendix map when an executive HLD was input.
- Document accepted HLD delivery deviations (e.g. sliced vs one-shot Phase 1) as planning defaults with Product validation called out.

### Do not

- Invent compliance, volumes, or integrations.
- Cite harness-internal paths as sole evidence.
- Skip alternates / rejection reasons.
- Ship Day-1 full multi-agent by default “because HLD lists specialists.”
- Let the model be the final authorizer of money movement or other irreversible side effects.
- Abbreviate peer Evidence URLs when full https links are available.

---

## 5. Required sections (minimum)

| # | Section | Must include |
|---|---------|--------------|
| 0 | Meta / SoT header | Harness, date, slug, input HLD path, knowledgebase id, status, audience |
| 1 | Executive technical summary | Agency model, delivery slices, autonomy, framework, named model ladder |
| 2 | Clarified requirements | Facts, assumptions, open Qs, closed decisions from design |
| 3 | Components & patterns | Agency ladder; **slices + exit gates**; PDM epic map; prompt governance; multi-agent **evolve triggers**; end-state topology labeled; policy-gate ownership |
| 4 | Model selection | Dense table: API id, why, benchmarks, $/MTok dated, alternates, routing ladder |
| 5 | Tools & MCP | Inventory + REST vs MCP decision + write tools only on executor |
| 6 | Memory | **Knowledge ≠ Memory** planes + TTL |
| 7 | Context management | Principles + no silent truncate of critical evidence |
| 8 | Value KPIs | Biz + tech including **tool recall** and **parameter accuracy** |
| 9 | Observability | OTel (+ optional UX) + semantic signals |
| 10 | Evaluation | Offline/online + slice-scoped gates + tool metrics thresholds |
| 11 | Continuous improvement | Loops + kill switches + autonomy promotion |
| 12 | Guardrails | Autonomy slider + controls + **HITL failure modes** |
| 13 | Identity & access | Paths + **AuthZ matrix with Authorize column** + model never writes |
| 14 | Agent frameworks | Prod vs prototype framing + rejected alternates |
| 15 | Design trade-offs | Scalability, modularity, cost, complexity |
| 16 | K8s / cloud-native | Namespaces, workloads (incl. policy-gate), HPA, PDB, CB, shard, GitOps, NetworkPolicy |
| 17 | Decision register | Chosen vs alternates vs business mapping |
| 18 | Evidence Register | Book chapters + full https peer/standards/pricing rows |
| App A | HLD → TDD map | When HLD input exists |
| App B | Implementation build order | Slice-aligned engineering steps |

Template: `outputs/templates/default.md`

---

## 6. Generation contract (Step 14)

1. Read this file, `references/knowledgebase.md`, and `outputs/templates/default.md`.  
2. Compile Steps 1–13; fill **every** required section.  
3. Run the §8 quality checklist — do not deliver if any P0 item fails.  
4. Evidence Register: Primary/Secondary need resolvable sources (https and/or book title+chapter).  
5. Activate `deliver-output`.

Default deliverer path:

```
agents-output/agentic-technical-design-harness/<slug>/<slug>-technical-design.md
```

Revisions: write `<slug>-technical-design-vN.md` (or `-consolidated`) when iterating; do not silently overwrite Accept artifacts without a revision note.

---

## 7. Default planning numbers (label as assumptions; Product may override)

| Item | Default |
|------|---------|
| Slice exit — policy consistency | ≥ 95% |
| Slice exit — tool recall | ≥ 90% |
| Slice exit — param accuracy (IDs) | ≥ 98% |
| Write proposals — amount/reason param accuracy | ≥ 98% |
| Manager evolve trigger | Tool-selection error above configured threshold for **2 consecutive** eval windows (set numeric X in eval config; document X even if Assumption) |
| Critic enable | Only if write-proposal error stays above target after **2** prompt iterations |
| Model cost soft/hard per interaction | Soft ~$0.15 / hard ~$0.40 (Assumption) |

---

## 8. Quality bar before calling artifact "done" (P0)

### Architecture & seams

- [ ] Knowledgebase loaded and applied (agency ladder present)
- [ ] Sliced MVP with in/out scope + exit gates (not Day-1 full multi-agent by default)
- [ ] End-state topology explicitly labeled **not** Day-1 build order
- [ ] Multi-agent / manager / critic are **trigger-gated**, not automatic early complexity
- [ ] Non-LM **policy-gate** (or equivalent) for irreversible/money actions + ownership
- [ ] Propose → authorize → execute separation; model never holds write creds
- [ ] Autonomy slider (Manual / Ask / Agent) + HITL failure modes
- [ ] Knowledge ≠ Memory

### PDM & operability

- [ ] Epic → slice → exit gate → KPI table + ticket template
- [ ] Prompt-pack ownership + change cadence per slice
- [ ] Decision register complete

### Platform density

- [ ] Named models + API ids + `pricing_verified_date` + alternates
- [ ] AuthZ matrix includes **Authorize** column
- [ ] K8s view includes workloads, HPA, PDB, circuit breakers, checkpoint hotspot mitigations
- [ ] Tools: MCP vs API decided; write tools bound to executor only

### Eval & evidence

- [ ] Tool recall + parameter accuracy in KPIs and eval exit criteria
- [ ] Evidence Register: book chapters + **full** https peer/standards/pricing URLs
- [ ] Facts vs assumptions vs open questions; blocking Qs listed
- [ ] HLD map appendix when HLD was input; delivery deviations documented

### Anti-patterns (fail if present)

- [ ] Dual conflicting living TDDs for same slug without SoT declaration
- [ ] LM as money/irreversible authorizer
- [ ] Tier-only model section (“economy/frontier”) without names
- [ ] Abbreviated “peer cases” without URLs
- [ ] Silent truncate of critical evidence allowed

---

## 9. Quality exemplar

Treat a completed TDD that passes the §8 P0 checklist as the structural exemplar for the next run: same seams and density, **not** domain copy-paste from another use case.
