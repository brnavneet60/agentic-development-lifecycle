---
description: Offline curated material and index of online reference sources.
---

Prefer `offline/` first. Use online entries only when resolve-reference escalates.

## Offline

- `e2e-requirement` — Source E2E requirement defining technical design sections (`doc`, offline) → `docs/e2e-requirement.txt`
- `output-standards` — Required TDD sections, language rules, evidence and quality bar (`doc`, offline) → `OUTPUT-STANDARDS.md`
- `knowledgebase` — **Primary design brain** — *Building Applications with AI Agents: Designing and Implementing Multiagent Systems* (`local_file`, offline) → [`knowledgebase.md`](./knowledgebase.md)
- `trusted-sources` — Allowed source classes for benchmarks, pricing, and papers (`local_file`, offline)
- `design-patterns-stub` — Offline stub for multi-agent pattern decision notes (`local_file`, offline)
- `model-selection-stub` — Offline stub for benchmark and cost considerations (`local_file`, offline)
- `context-engineering-stub` — Offline stub for context-management principles (`local_file`, offline)

## Online (fetch via fetch-online)

- `langgraph-multi-agent` — LangGraph multi-agent concepts (`web_url`) — when component/pattern design needs primary docs
- `langchain-docs` — LangChain / LangGraph docs home (`web_url`)
- `crewai-docs` — CrewAI documentation (`web_url`)
- `autogen-docs` — Microsoft AutoGen documentation (`web_url`)
- `semantic-kernel-docs` — Semantic Kernel documentation (`web_url`)
- `openai-pricing` / `anthropic-pricing` / `google-ai-pricing` — live model pricing (`web_url`)
- `artificial-analysis` / `lmarena` / `hf-open-llm-leaderboard` — benchmarks (`web_url`)
- `langchain-context-engineering` — context engineering guidance (`web_url`)
- `otel-ai-agent-observability` — OTel AI agent observability (`web_url`)
- `nvidia-agent-evaluation` — agent evaluation guidance (`web_url`)
- `langchain-loop-engineering` — loop engineering (`web_url`)

Full locators: `config/harness.config.yaml` → `references`.
