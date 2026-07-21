# Skills Index — E2E v1.2.0

Execute **in order**. Run `manage-design-context` **before** each step; `write-design-journal` **after** each step.

**Output standards:** `../../agentic-design-harness-hld/OUTPUT-STANDARDS.md`

| # | Skill | Checkpoint After? | Output |
|---|-------|-------------------|--------|
| 0 | [manage-design-context](./manage-design-context/SKILL.md) | No | Context package + manifest |
| 1 | [capture-business-flow](./capture-business-flow/SKILL.md) | **Yes** | Flow YAML + journal entry |
| 2 | [classify-design-pattern](./classify-design-pattern/SKILL.md) | No | Pattern YAML + journal entry |
| 3 | [define-kpis](./define-kpis/SKILL.md) | **Yes** | KPI YAML + rollup-through-03 |
| — | [merge-parallel-research](./merge-parallel-research/SKILL.md) | **Yes** | After wave-post-3 (if parallel enabled) |
| 4 | [model-selection](./model-selection/SKILL.md) | No | Models YAML + journal (or subagent) |
| 5 | [design-tools-integration](./design-tools-integration/SKILL.md) | No | Tools YAML + journal (or subagent) |
| 6 | [design-memory-knowledge](./design-memory-knowledge/SKILL.md) | **Yes** | Memory/KB YAML + rollup-through-06 |
| 7 | [select-agent-framework](./select-agent-framework/SKILL.md) | No | Framework YAML (+ refine after step 6) |
| 8 | [design-guardrails-security](./design-guardrails-security/SKILL.md) | **Yes** | Guardrails YAML + journal |
| 9 | [design-observability-value-loops](./design-observability-value-loops/SKILL.md) | **Yes** | Observability YAML + rollup-through-09 |
| 10 | [generate-design-artifact](./generate-design-artifact/SKILL.md) | No | Final `<slug>.md` + journal |
| * | [write-design-journal](./write-design-journal/SKILL.md) | — | Runs after every step above |

## Activation

Load `harness-sources.yaml`, `harness-context.yaml`, `harness-journal.yaml`, `harness-parallel.yaml` at bootstrap.

Before each skill: `manage-design-context` (loads journal rollup — not full prior YAML).  
After each skill: `write-design-journal` (isolates cold payloads; writes summary).  
After Step 3 checkpoint (if parallel enabled): launch wave-post-3 subagents → `merge-parallel-research`.

When user describes a business process or asks to "design agentic AI", load Step 0 then Step 1 — do not skip rainy-day, compliance, or documentation questions.
