# Design Patterns — Offline Stub

Use when classifying single vs multi-agent topology, orchestration, and hand-offs.

## Decision prompts

1. Single agent sufficient if tool surface is small and flow is linear?
2. Supervisor / router needed when specialists and dynamic routing appear?
3. Sequential pipeline for fixed stages?
4. Parallel fan-out/fan-in for independent branches?
5. HITL overlay when approvals or high-severity rainy-day paths exist?
6. Event-driven / async when triggers are stream/message based?

## Must document

- Agent count, roles, skills
- Stateful vs stateless
- Knowledge-base needs and update pattern
- A2A communication / hand-off pattern
- Alternates rejected and why

## Escalate online

- `langgraph-multi-agent`, `crewai-docs`, `autogen-docs`, `semantic-kernel-docs`

Curate deeper offline packs later; cite original `source_url`s in the TDD Evidence Register.
