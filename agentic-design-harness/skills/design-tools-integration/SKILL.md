---
name: design-tools-integration
description: Inventory tools, decide MCP vs REST/API, identify build vs buy. Step 5 of agentic-design-harness E2E.
metadata:
  harness: agentic-design-harness
  step: 5
  version: "1.0.0"
---

# Design Tools Integration

## Purpose

From flow steps and pattern topology, define **what tools** agents need and **how** they integrate (MCP, OpenAPI, custom SDK).

**Ask the user** when tool ownership, API availability, or auth is unknown.

## Inputs

- `flow` from Step 1 (systems, third_party_interfaces)
- `pattern` from Step 2 (agent roles)
- `task_profile` from Step 1

## Interview Questions

1. For each system in the flow — is there an **existing API**? OpenAPI spec? Rate limits?
2. Does the org already run **MCP servers** for any system?
3. Which tools are **read-only** vs **write/mutate**? (write → HITL consideration)
4. Are tools **shared** across agents or per-agent?
5. Latency SLA per integration?

## Decision Matrix

| Signal | Prefer |
|--------|--------|
| Kagent / K8s platform target | **MCP ToolServer** or RemoteMCPServer |
| Standard SaaS with official MCP | **RemoteMCPServer** or community MCP |
| Legacy SOAP / proprietary | **Custom API wrapper** → expose as MCP |
| Simple HTTP CRUD | **OpenAPI tool** (framework-native) |
| Batch file / SFTP | **Custom tool** + async job pattern |

Load `references/tools-patterns/TOOLS-PATTERNS.md` for MCP vs API trade-offs.

## Output

```yaml
tools:
  inventory:
    - id: T1
      name: "<e.g. CRM lookup>"
      agent_refs: [supervisor, lookup_agent]
      system: "<CRM>"
      operation: read | write | read_write
      integration:
        type: mcp | openapi | custom_sdk | manual_hitl
        existing: true | false
        build_effort: none | low | medium | high
      auth: oauth | api_key | mTLS | service_account
      latency_sla_ms: <int or null>
      pii_exposed: true | false
  summary:
    total_tools: <int>
    mcp_count: <int>
    api_count: <int>
    to_build: [<tool ids>]
  open_questions:
    - "<what still needs user input>"
```

## Validation

```
IF any write tool AND pattern != P5 AND amount/risk high:
  RECOMMEND HITL gate on that tool
IF to_build.length > 3 AND timeline tight:
  WARN scope risk — prioritize MVP tool set
IF mcp_count > 0 AND target_platform == kagent:
  NOTE "Map to ToolServer CR in kagent-platform-harness"
```

## Next Skill

`design-memory-knowledge`
