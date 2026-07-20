# Agent Framework Selection Guide

| Framework | Strengths | Weaknesses | Fit Signals |
|-----------|-----------|------------|-------------|
| **Kagent** | K8s CRDs, MCP, A2A, GitOps, Istio mesh | K8s required | Platform on agentic-ai-platform |
| **LangGraph** | Graph state, checkpoints, human-in-loop | Learning curve | Complex branching, P2/P3/P5 |
| **CrewAI** | Fast multi-agent prototypes | Less K8s-native | POC, role-based teams |
| **Semantic Kernel** | .NET enterprise | Python secondary | Microsoft stack |
| **AutoGen** | Research multi-agent | Ops maturity varies | Experimentation |
| **Custom + LiteLLM** | Full control | You own everything | Unique constraints |

## Combined Stacks

| Pattern | Common Stack |
|---------|--------------|
| K8s production | Kagent + ontology SPARQL + Argo CD |
| Rapid POC | CrewAI or LangGraph + OpenAPI tools |
| Enterprise .NET | Semantic Kernel + Azure OpenAI |

## Downstream

If **Kagent** selected → next harness: `kagent-platform-harness/`
