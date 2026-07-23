# Agentic Design Harness — Output Standards

**Version:** 1.2  
**Date:** 2026-07-23  
**Audience for final artifact:** Industry leaders, senior architects, product managers, CTO  
**Learned from:** Lyft charge/earnings pilot + architect reviews (2026-07-21 1450 / 1536) + CTO v2 review (2026-07-23 1700)

---

## 1. Primary audience rule

The final design document is a **business-facing High-Level Design**, not a harness execution log.

Write for readers who care about:

- business problem and operating impact,
- decision rationale and trade-offs,
- phased delivery and investment,
- risk, compliance, and value realization,
- evidence that claims and KPI targets can be audited.

---

## 2. Language rules

### Do

- Use plain business language first; explain technical choices through business outcomes.
- Include a **Decision Register**: each major choice must state business reasoning, trade-off, and why chosen.
- Separate **facts** from **assumptions** when stakeholder data is missing. Label assumptions explicitly: `Assumption — planning default`.
- Include phased build plan with timeline, effort, team, and cost ranges (low / likely / high).
- Include evolution path and feedback mechanisms (business, ops, engineering).
- Include a dedicated **References & Evidence Register** (section or appendix) with Primary / Secondary / Assumption tags.
- Cite **external** evidence only: industry case studies, vendor engineering write-ups, standards bodies (NIST, OWASP), white papers, or peer-reviewed research — always with a resolvable **https://** URL.
- Lead **investment / outcome** claims with **Primary** business case evidence. Use pattern books / Secondary sources for vocabulary and operating-model framing — not as the sole justification to fund.

### Do not

- Use internal harness pattern codes (`P1`, `P2`, etc.) in the main body.
- Cite harness-internal paths as evidence (`references/*.md`, `knowledgebase.md`, `TRUSTED-SOURCES.md`, skill files, journal YAML). Those files are **lookup indexes**, not citable evidence.
- When an offline curated pack or local knowledge base informed a claim, cite the pack’s original `source_url` (the web URL it was curated from) — never the local markdown filename alone.
- Name a company, product, or “style” caution in Risks without a matching Evidence Register row (or rephrase without the name).
- Dump source URLs throughout the executive narrative (put them in the Evidence Register).
- Dump implementation jargon (framework names, MCP, checkpoint stores) without business translation.
- Present monitoring-only quality plans without offline eval, canary gates, and acceptance criteria.
- Leave open decisions unanswered without **recommended planning defaults** labeled as assumptions.
- Oversell a revision as deeper business discovery when it only upgraded framing/diagrams — state that honesty in the executive summary when applicable.

Technical detail belongs in **Appendix B (Engineering mapping)** — not the executive narrative. A separate `<slug>-technical.md` companion is **not** required for harness completion.

---

## 3. Required sections (minimum)

| # | Section | Purpose |
|---|---------|---------|
| 1 | Executive summary | Business problem, recommended approach, value, controls; version honesty if revision |
| 2 | Business domain and current problem | Clear domain boundary and pain points |
| 3 | Stakeholders and users | Who benefits and who owns outcomes |
| 4 | Target business flow | End-to-end process in business terms |
| 5 | Decision register | Major choices with business rationale |
| 6 | Operating model | Capabilities in plain language; optional roles (e.g. critic) must be specified if named |
| 7 | Business scenarios | Happy path + risk/exception scenarios |
| 8 | KPI framework | Leadership metrics with baseline method |
| 8A | Traffic / region / criticality | Measured or **assumed** band; mark TBC if unknown |
| 9 | Solution overview | **Must open with a diagram** (block or agentic flow), then plain-language architecture |
| 9A | Autonomy / confidence | Measurable definition of when auto-resolve vs human gate |
| 10 | Data contracts | Read inputs and write outputs per integration |
| 11 | Model / cost / tools / memory | Model mix, cost caps, API vs MCP, retention TTLs |
| 12 | Security and guardrails | Threat model, identity/authZ, rollback |
| 13 | Evaluation strategy | Offline golden sets, canary, adversarial, exit criteria **including tool-accuracy for money writes** |
| 14 | Delivery approach | Phases, timeline, effort, cost ranges |
| 15 | Team and skills | Roles required to build and operate |
| 16 | Prompt governance | Template, checklist, ownership (Phase 1 for mission-critical) |
| 17 | Reliability / observability | Metrics, alerts, safe failure behavior |
| 18 | Evolution and feedback | How the capability improves over time |
| 19 | Risks with ownership | Mitigations, owners, triggers — named examples must be evidenced |
| 20 | Open decisions | What leadership must confirm |
| 20A | Recommended defaults | Planning assumptions for each open decision |
| 21 | Next steps | Concrete actions |
| 22 | References & Evidence Register | Decision → evidence type → source link |
| App A | Interview coverage matrix | Harness Step 1 Blocks A–H → section or ASSUMPTION |
| App B | Engineering mapping | Supervisor topology (one vs separate), specialists, critic, safety order, state, observability |

Template: `templates/agentic-design-artifact-template.md`

---

## 4. How the harness must generate output

### Generation contract (Step 10)

1. Read `OUTPUT-STANDARDS.md` (this file) and the artifact template.
2. Compile Steps 1–9 into the configured output path for this harness/use case.
3. Fill **every required section** above. Prefer `Assumption — planning default` over inventing stakeholder facts.
4. For open decisions: list the question **and** a recommended default with reasoning (do not leave blank placeholders).
5. Build the Evidence Register for major design claims and KPI anchors:
   - Every Primary/Secondary row must include an external `https://` URL.
   - If the claim came via offline curation or `references/knowledgebase/`, resolve and cite the original `source_url` — do **not** cite local `.md` paths.
   - Assumptions may omit URLs but must say so explicitly.
   - Any named company/product in Risks must appear in the Evidence Register (or remove the name).
6. Build the Interview Coverage Matrix for Step 1 Blocks A–H (and note Gaps for Steps 5–8 interviews).
7. Keep main body leadership-friendly; put dense technical mapping in Appendix B.
7a. **Solution Overview must start with a diagram** (mermaid preferred): intake → safety → supervisor/router → specialists → (optional critic) → approval → action → learn. Narrative follows the diagram.
7b. If a **critic / quality node** is part of the operating model, specify: trigger, pass/fail criteria, fail path, model class, latency/cost note.
7c. Define **confidence / autonomy** in measurable terms (rules, judge score, or amount thresholds) — not vague “low confidence.”
7d. State **supervisor topology**: one shared supervisor vs separate instances per channel/persona (rider vs driver), and keep diagram + Appendix B consistent.
7e. Mission-critical money flows: pilot exit criteria must include **tool parameter accuracy** (or equivalent) for write actions.
8. Run `write-design-journal` after generation **and after every revision**.

### Knowledge base usage

- Optional offline pack: `references/knowledgebase/knowledgebase.md` (Albada) — configured in `harness-sources.yaml` as `knowledgebase`.
- Use for multiagent pattern vocabulary (manager coordination, autonomy slider, least power, eval-as-spec).
- Evidence Register cites O'Reilly / companion GitHub URLs from `CURATION-SOURCES.md` — never `knowledgebase.md`.

### Revision contract (mandatory journaling)

Whenever the design is revised from new feedback or new information:

1. Write `journal/entries/revision-YYYYMMDD-<label>.yaml` with:
   - `trigger` (feedback file or change source)
   - `summary` of what changed
   - `decisions[]` with rationale
   - `delta_sections_added_or_expanded`
   - pointers to artifact + review
2. Update `journal/INDEX.yaml` (status, updated_at, entries list, reviews list).
3. Do **not** silently overwrite the artifact without a revision journal entry.
4. If the revision is primarily framing/clarity (not new discovery), say so in the executive summary to avoid version inflation.

---

## 5. Output file naming

Output location is **configurable** via `paths.project_root` (YAML) or the activation prompt. The harness does not require any shared testing folder.

Default layout if unset:

```
runs/<use-case-slug>/<use-case-slug>.md
```

Journal entries and step context live alongside the artifact under `{project_root}`.

Engineering detail for implementers lives in **Appendix B** of that file. Do not treat a separate technical companion as part of the default Definition of Done.

---

## 6. Quality bar before calling artifact "done"

- [ ] Business domain and problem statement are specific
- [ ] Every major decision has business reasoning
- [ ] Phased delivery includes timeline + effort + cost ranges
- [ ] Team roles and skills are listed
- [ ] Threat model, authZ, and eval gates present for mission-critical flows
- [ ] Evolution and feedback loops defined
- [ ] Open decisions listed **with** recommended planning defaults
- [ ] References & Evidence Register present (Primary / Secondary / Assumption)
- [ ] Every Primary/Secondary citation has an external https URL (no harness `.md` paths as evidence)
- [ ] Offline-curated / knowledgebase claims cite original `source_url`, not local pack path
- [ ] Named companies in Risks appear in Evidence Register (or names removed)
- [ ] Interview Coverage Matrix present
- [ ] Traffic/region/compliance either measured or assumed with TBC gates
- [ ] Solution Overview opens with a block or agentic-flow diagram (before prose)
- [ ] Critic (if named) has trigger, pass/fail, fail path, model class
- [ ] Autonomy/confidence defined measurably; supervisor topology consistent (diagram ↔ appendix)
- [ ] Money-write tool accuracy in pilot exit criteria
- [ ] Investment claims led by Primary business evidence (Secondary books = framing)
- [ ] No harness-internal pattern codes in main body
- [ ] Revision journaled if this is not the first generation
