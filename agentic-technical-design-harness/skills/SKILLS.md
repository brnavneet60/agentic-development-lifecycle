---
description: Atomic capabilities for the technical design harness role.
---

Built-in (configuration-driven):

- `resolve-reference/` — map reference ids to offline/online locators
- `fetch-online/` — live web, git, or MCP fetch when offline is insufficient
- `deliver-output/` — render and publish artifacts per outputs.deliverers

Domain (execute in order; see HARNESS.md):

| # | Skill | Checkpoint? |
|---|-------|-------------|
| 1 | `clarify-requirements/` | Yes |
| 2 | `design-components-patterns/` | Yes |
| 3 | `select-models/` | No |
| 4 | `design-tools-mcp/` | No |
| 5 | `design-memory/` | No |
| 6 | `design-context-management/` | Yes |
| 7 | `define-value-kpis/` | No |
| 8 | `design-observability/` | No |
| 9 | `design-evaluation/` | No |
| 10 | `design-continuous-improvement/` | Yes |
| 11 | `design-guardrails/` | No |
| 12 | `design-identity-access/` | Yes |
| 13 | `select-agent-framework/` | No |
| 14 | `generate-technical-design/` | No |

Activation: load `config/harness.config.yaml` at bootstrap. Prefer offline references; escalate with `fetch-online` when needed.
