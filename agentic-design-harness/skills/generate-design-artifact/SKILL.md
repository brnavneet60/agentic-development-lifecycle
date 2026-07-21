---
name: generate-design-artifact
description: Compile all E2E design steps into final leadership-ready HLD markdown. Step 10.
metadata:
  harness: agentic-design-harness
  step: 10
  version: "1.3.0"
---

# Generate Design Artifact

## Purpose

Produce the final High-Level Design markdown combining Steps 1–9 for a **leadership audience** (industry leaders, senior architects, product managers).

**Mandatory:** read `../../agentic-design-harness-hld/OUTPUT-STANDARDS.md` (v1.1+) before writing.

## Audience rules

- Business language in the main body.
- Every major decision includes business reasoning, trade-off, and why chosen.
- No harness pattern codes (`P1`, `P2`, …) in the main body.
- Do **not** scatter source URLs through the executive narrative — put them in **References & Evidence Register**.
- Technical detail goes in Appendix B (engineering mapping) or a companion technical doc.
- Label unknowns as `Assumption — planning default`; never invent stakeholder-confirmed policy.

## Prerequisites

- All step outputs (flow, pattern, kpis, models, tools, memory/knowledge, framework, guardrails/security, observability/value/loops)
- `templates/agentic-design-artifact-template.md`
- `OUTPUT-STANDARDS.md` v1.1+

## Required sections (minimum)

| Section | Source |
|---------|--------|
| Executive summary | All — business-first |
| Business domain and current problem | Step 1 |
| Decision register | Steps 2–9 |
| Operating model (plain language) | Step 2 |
| Business scenarios | Step 1 |
| KPI framework + traffic/region/criticality | Steps 1, 3 |
| Solution overview + safety-first ordering | Step 2 |
| Data contracts | Steps 1, 5 |
| Model strategy, cost caps, tools (API vs MCP + SLA), memory TTL | Steps 4–6 |
| Security, threat model, identity/authZ, rollback | Step 8 |
| Evaluation strategy + exit criteria | Steps 8, 9 |
| Delivery phases, timeline, effort, cost ranges | All |
| Team and skills | All |
| Prompt governance | Step 8/9 |
| Reliability / observability | Step 9 |
| Evolution and feedback | Step 9 |
| Risks with owners/triggers | All |
| Open decisions **+ recommended defaults** | All |
| Next steps | — |
| References & Evidence Register | Trusted sources + any Primary case evidence |
| Appendix A — Interview Coverage Matrix | Step 1 Blocks A–H (+ note Steps 5–8 gaps) |
| Appendix B — Engineering mapping | Steps 2, 5–9 |

## Write path

```
agents-output/agentic-design-harness/<flow.slug>/<flow.slug>.md
```

## Generation algorithm

```
FUNCTION generateArtifact(slug, step_outputs):
  LOAD OUTPUT-STANDARDS.md
  LOAD templates/agentic-design-artifact-template.md

  WRITE leadership sections 1–21 using step_outputs
  FOR EACH open_decision:
    IF stakeholder_answer missing:
      WRITE recommended_default WITH label "Assumption — planning default"
      INCLUDE reasoning

  WRITE Evidence Register:
    FOR EACH major_decision OR kpi_target:
      TAG evidence_type IN {Primary, Secondary, Assumption}
      IF Primary OR Secondary:
        REQUIRE external https URL
          (industry case study | white paper | peer-reviewed paper |
           standards body | vendor engineering write-up)
        IF claim came from offline curated pack:
          RESOLVE and CITE original source_url from curation map
          NEVER cite harness path (references/*.md, TRUSTED-SOURCES.md, etc.)
      IF Assumption:
        LABEL "Assumption — planning default" (URL optional)

  WRITE Interview Coverage Matrix:
    FOR EACH capture-business-flow question in Blocks A–H:
      MAP to section OR mark ASSUMPTION/MISSING

  WRITE Appendix B engineering mapping (router, safety order, state, observability)

  WRITE agents-output/agentic-design-harness/<slug>/<slug>.md
  RUN write-design-journal AFTER generation
```

## Quality checks

```
READ OUTPUT-STANDARDS.md quality bar checklist

REQUIRE:
  - Evidence Register present
  - Interview Coverage Matrix present
  - Open decisions include recommended defaults
  - Threat model + eval gates for mission-critical flows
  - Traffic/region either measured or assumed with TBC gate

IF any open_questions[] non-empty:
  INCLUDE "Open Decisions" AND "Recommended defaults"

IF compliance conflict unresolved:
  FLAG in Risks — do not mark artifact "approved"

VERIFY:
  - no harness pattern codes in main body
  - no harness .md / skill paths used as Evidence Register citations
  - every Primary/Secondary row has external https URL
  - no URL dump in executive summary
  - journal entry written
```

## Revisions

If regenerating after feedback:

1. Update the artifact.
2. Write `journal/entries/revision-YYYYMMDD-<label>.yaml` (mandatory).
3. Update `journal/INDEX.yaml`.

Present file path to user when complete.
