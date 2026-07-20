# Tools Integration Patterns

## MCP vs Direct API

| Factor | MCP | REST/OpenAPI Tool |
|--------|-----|-------------------|
| Discoverability | Tool schema exposed to agent | You define schema |
| Kagent platform | Native ToolServer CRD | Wrap as MCP recommended |
| Reuse across agents | High | Medium |
| Latency | Extra hop | Direct |
| Auth | MCP server holds secrets | Agent runtime holds secrets |

## When to Build MCP

- Tool used by **multiple agents**
- Need **central audit** of tool calls
- Deploying on **Kagent / K8s** with GitOps for tool servers

## When API Is Enough

- Single agent, single integration
- Prototype / POC phase
- Serverless without MCP infra

## Build vs Buy

| Situation | Recommendation |
|-----------|----------------|
| Official MCP exists | **Buy** (deploy RemoteMCPServer) |
| OpenAPI only | **Build** thin MCP wrapper or native tool |
| No API | **Human-in-the-loop** or RPA — flag scope risk |

## Security Defaults

- Read-only tools by default; write tools require explicit approval in design
- Secrets never in prompts — vault / K8s secrets only
- Log tool I/O with PII redaction
