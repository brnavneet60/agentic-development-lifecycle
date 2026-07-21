# Agentic AI Design Harness — E2E v1.3

An **offline harness** for end-to-end agentic AI solution design from business flows. Built on [Agent Harnesses](https://agentharnesses.io) and [Agent Skills](https://agentskills.io).

## Documentation (handoff package)

| Document | Path |
|----------|------|
| Handoff (start here) | `../../agentic-design-harness-hld/HANDOFF-agentic-design-harness.md` |
| Reproduction guide | `../../agentic-design-harness-hld/REPRODUCIBILITY.md` |
| Output standards (v1.1) | `../../agentic-design-harness-hld/OUTPUT-STANDARDS.md` |
| Requirements | `../../agentic-design-harness-hld/e2e-agentic-design-harness.txt` |
| E2E HLD (approved) | `../../agentic-design-harness-hld/hld-e2e-agentic-design-harness-v1.md` |
| Maturity roadmap | `../../agentic-design-harness-hld/harness-maturity-roadmap-v1.2.md` |

## What it does

Given a business use case, the harness runs a **10-step workflow** (plus Step 0 context + journal) and produces a leadership-ready design document:

```
agents-output/agentic-design-harness/<use-case-slug>/<use-case-slug>.md
```

| Step | Output |
|------|--------|
| 1 | Business flow, scenarios, compliance, process nuances |
| 2 | Design pattern (plain language + technical mapping) |
| 3 | Weighted KPI profile |
| 4 | Multi-model map, benchmarks, hosting, cost |
| 5 | Tools inventory, MCP vs API |
| 6 | Memory, knowledge, context strategy |
| 7 | Agent framework |
| 8 | Guardrails and security |
| 9 | Observability, value KPIs, feedback loops |
| 10 | Final design artifact |

**Checkpoint gates** after Steps 1, 3, 6, 8, and 9.

## Quick start

```
Using agentic-design-harness v1.3, read HARNESS.md and
../../agentic-design-harness-hld/OUTPUT-STANDARDS.md (v1.1).

Design end-to-end agentic AI for: [your business use case]

Produce agents-output/agentic-design-harness/<slug>/<slug>.md with Evidence Register,
Interview Coverage Matrix, and open-decision planning defaults.
Journal every step and every revision.
```

## Structure

```
agentic-design-harness/
├── HARNESS.md
├── harness-sources.yaml      # v1.2 — online/offline sources + curation jobs
├── harness-context.yaml      # per-skill context policy
├── harness-journal.yaml      # journal + isolation
├── harness-parallel.yaml     # optional parallel waves
├── skills/                   # 14 skills (see skills/SKILLS.md)
├── references/
│   └── curation-sources/CURATION-SOURCES.md
└── templates/
    └── agentic-design-artifact-template.md
```

Load all four YAML configs at bootstrap (Step 0).

## Pilot reference

`../../agents-output/agentic-design-harness/lyft-charge-earnings-dispute/lyft-charge-earnings-dispute.md`

## Downstream

```
agentic-design-harness  →  agents-output/agentic-design-harness/<slug>/<slug>.md
         │
         ▼
kagent-design-harness →  agents-output/kagent-design-harness/<slug>/…
```

## Disclaimer

Model pricing, benchmarks, and GPU sizing are **indicative**. Verify against trusted sources before procurement.
