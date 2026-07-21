# Agentic Design Harness

**Version:** 1.3.0  
**Audience of the artifact:** industry leaders, senior architects, product managers

Design-only harness that turns a business use case into an **executive High-Level Design (HLD)** — not production agent code, and not a deep LLD.

Built on [Agent Harnesses](https://agentharnesses.io) and [Agent Skills](https://agentskills.io).

---

## What you get

| | |
|--|--|
| **Primary output** | Leadership-ready design memo: problem, decisions, value, delivery, risk, evidence |
| **Path** | `agents-output/agentic-design-harness/<use-case-slug>/<use-case-slug>.md` |
| **Tone** | Business language first; engineering detail only in Appendix B |
| **Not the goal** | Framework dumps, pattern codes in the narrative, or implementation specs |

Contract: [`OUTPUT-STANDARDS.md`](./OUTPUT-STANDARDS.md)

---

## Quick start

In Cursor (or any Agent Skills runtime):

```
Using agentic-design-harness v1.3, read HARNESS.md and OUTPUT-STANDARDS.md.

Design end-to-end agentic AI for: [business use case]

Run Steps 0–10 with checkpoint confirmations after 1, 3, 6, 8, 9.
Write agents-output/agentic-design-harness/<slug>/<slug>.md per OUTPUT-STANDARDS
(Evidence Register with external https URLs, Interview Coverage Matrix,
open-decision planning defaults). Journal every step and every revision.
```

Bootstrap folders (from your KAIF workspace root):

```bash
HARNESS=agentic-design-harness
SLUG=your-use-case-slug
mkdir -p "agents-output/$HARNESS/$SLUG"/{context/steps,journal/entries,journal/payloads,parallel,curated}
```

---

## Workflow (10 design steps)

| Step | Skill | Produces (for the executive artifact) |
|------|-------|----------------------------------------|
| 0 | `manage-design-context` | Context package for the next skill |
| 1 | `capture-business-flow` | Domain, flow, sunny/rainy scenarios · **checkpoint** |
| 2 | `classify-design-pattern` | Operating model (plain language; codes stay internal) |
| 3 | `define-kpis` | Leadership KPI profile · **checkpoint** |
| 4 | `model-selection` | Model mix, cost band, hosting stance |
| 5 | `design-tools-integration` | Integrations and write/read boundaries |
| 6 | `design-memory-knowledge` | Retention, knowledge, context strategy · **checkpoint** |
| 7 | `select-agent-framework` | Framework recommendation (business rationale) |
| 8 | `design-guardrails-security` | Threat model, authZ, rollback · **checkpoint** |
| 9 | `design-observability-value-loops` | Eval gates, value loops · **checkpoint** |
| 10 | `generate-design-artifact` | Final `<slug>.md` |

After every step: `write-design-journal`. After every rewrite: revision journal entry.

Skills index: [`skills/SKILLS.md`](./skills/SKILLS.md) · Entry: [`HARNESS.md`](./HARNESS.md)

---

## Repository layout

```
agentic-design-harness/
├── README.md                 ← this file
├── HARNESS.md                ← runtime entry + philosophy
├── OUTPUT-STANDARDS.md       ← executive artifact contract (canonical)
├── docs/
│   └── e2e-requirements.txt  ← original E2E interview / design goals
├── harness-sources.yaml
├── harness-context.yaml
├── harness-journal.yaml
├── harness-parallel.yaml
├── skills/                   ← 14 skills
├── references/               ← offline catalogs (cite source_url in Evidence Register)
└── templates/
    └── agentic-design-artifact-template.md
```

Load the four `harness-*.yaml` files at bootstrap (Step 0).

---

## Output location

```
KAIF/agents-output/
└── agentic-design-harness/
    └── <use-case-slug>/
        ├── <use-case-slug>.md    # executive HLD
        └── journal/              # step + revision trail
```

Pilot example: `../../agents-output/agentic-design-harness/lyft-charge-earnings-dispute/`

---

## Downstream

```
agentic-design-harness
  → executive HLD (<slug>.md)
         │
         ▼
kagent-design-harness (or other implementation harness)
  → build / deploy on Kubernetes
```

This harness stops at design. Implementation is a separate harness.

---

## Evidence rules (summary)

- Evidence Register cites **external** `https://` sources (case studies, papers, NIST/OWASP, vendor eng docs).
- Never cite harness `references/*.md` as evidence — those are lookup indexes.
- If a claim came from an offline curated pack, cite the pack’s original web `source_url`.

---

## Disclaimer

Model pricing, benchmarks, and GPU sizing in reference catalogs are **indicative**. Verify against vendor pages before procurement.
