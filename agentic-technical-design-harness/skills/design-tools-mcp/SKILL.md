---
name: design-tools-mcp
description: >
  Inventory tools with REST-first vs MCP decision, least-power schemas, and write tools bound only to the executor. Use as Step 4.
---

# Design tools & MCP

## Purpose

Tooling at Accept quality (knowledgebase Ch 4) — least power, modularity, MCP security caution.

## Instructions

1. Inventory tools per consumer with interface, auth scope, SLA, build vs buy.  
2. **Least power:** narrow tools + strict schemas; no arbitrary code/SQL unless sandboxed and justified.  
3. **Write / irreversible tools:** bind **only** to `action-executor` (or equivalent) — never to specialist LM tool lists.  
4. Phase 1 default: **REST/API** to systems of record + shared typed client library.  
5. MCP: defer until contracts stable; require gateway RBAC/mTLS/audit — do not assume MCP authZ is solved.  
6. Decision discipline for MCP vs API and build vs buy.

## Output

`tools-mcp.yaml` with inventory[], write_binding_rule, mcp_decision.
