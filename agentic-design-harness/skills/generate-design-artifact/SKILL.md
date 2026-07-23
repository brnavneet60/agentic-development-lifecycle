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

**Mandatory:** read `../OUTPUT-STANDARDS.md` (v1.2+) before writing.

## Audience rules

- Business language in the main body.
- Every major decision includes business reasoning, trade-off, and why chosen.
- No harness pattern codes (`P1`, `P2`, …) in the main body.
- Do **not** scatter source URLs through the executive narrative — put them in **References & Evidence Register**.
- Technical detail goes in Appendix B (engineering mapping) only — not a separate required companion doc.
- Label unknowns as `Assumption — planning default`; never invent stakeholder-confirmed policy.

## Prerequisites

- All step outputs (flow, pattern, kpis, models, tools, memory/knowledge, framework, guardrails/security, observability/value/loops)
- `templates/agentic-design-artifact-template.md`
- `OUTPUT-STANDARDS.md` v1.2+ (harness root)

## Required sections (minimum)

| Section | Source |
|---------|--------|
| Executive summary | All — business-first |
| Business domain and current problem | Step 1 |
| Decision register | Steps 2–9 |
| Operating model (plain language) | Step 2 |
| Business scenarios | Step 1 |
| KPI framework + traffic/region/criticality | Steps 1, 3 |
| Solution overview + safety-first ordering | Step 2 — **diagram first**, then prose |
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
  LOAD ../OUTPUT-STANDARDS.md   # harness root
  LOAD templates/agentic-design-artifact-template.md

  WRITE Solution Overview:
    FIRST: block diagram OR agentic flow diagram (mermaid preferred; ASCII acceptable)
      SHOW: intake → safety → supervisor/router → specialists → optional critic → approval → action → notify/learn
    THEN: plain-language architecture prose
    THEN: safety-first + least-power ordering
    THEN: measurable autonomy / confidence definition
    THEN: supervisor topology (one vs separate instances) — must match diagram + Appendix B

  IF operating_model includes critic_or_quality_node:
    WRITE critic_spec:
      trigger, pass_fail_criteria, fail_path, model_class, latency_cost_note

  WRITE leadership sections remaining using step_outputs
  FOR EACH open_decision:
    IF stakeholder_answer missing:
      WRITE recommended_default WITH label "Assumption — planning default"
      INCLUDE reasoning

  WRITE Evidence Register:
    FOR EACH major_decision OR kpi_target OR named_risk_example:
      TAG evidence_type IN {Primary, Secondary, Assumption}
      IF Primary OR Secondary:
        REQUIRE external https URL
        IF claim came from offline curated pack OR knowledgebase:
          RESOLVE and CITE original source_url (O'Reilly / case study URL)
          NEVER cite harness path (references/*.md, knowledgebase.md, etc.)
      IF Assumption:
        LABEL "Assumption — planning default" (URL optional)
    REQUIRE: investment/outcome claims led by Primary business cases;
             Secondary books only for pattern vocabulary

  IF mission_critical money writes:
    INCLUDE tool_parameter_accuracy (or equivalent) IN pilot exit criteria

  WRITE Interview Coverage Matrix:
    FOR EACH capture-business-flow question in Blocks A–H:
      MAP to section OR mark ASSUMPTION/MISSING

  WRITE Appendix B engineering mapping
    (supervisor topology, specialists, critic, safety order, state, observability)

  WRITE artifact to configured output path
  RUN write-design-journal AFTER generation
```

## Quality checks

```
READ OUTPUT-STANDARDS.md quality bar checklist (v1.2+)

REQUIRE:
  - Solution Overview starts with a diagram (not prose-only)
  - Evidence Register present; named Risk companies evidenced
  - Interview Coverage Matrix present
  - Open decisions include recommended defaults
  - Threat model + eval gates for mission-critical flows
  - Traffic/region either measured or assumed with TBC gate
  - Critic specified if named; autonomy measurable; topology consistent
  - Money-write tool accuracy in exit criteria when applicable

IF any open_questions[] non-empty:
  INCLUDE "Open Decisions" AND "Recommended defaults"

IF compliance conflict unresolved:
  FLAG in Risks — do not mark artifact "approved"

VERIFY:
  - no harness pattern codes in main body
  - no harness .md / skill / knowledgebase paths used as Evidence citations
  - every Primary/Secondary row has external https URL
  - no URL dump in executive summary
  - journal entry written
```

## Revisions

If regenerating after feedback:

1. Update the artifact.
2. Write `journal/entries/revision-YYYYMMDD-<label>.yaml` (mandatory).
3. Update `journal/INDEX.yaml`.
4. If mainly framing/clarity (not new discovery), state that in the executive summary.

Present file path to user when complete.
