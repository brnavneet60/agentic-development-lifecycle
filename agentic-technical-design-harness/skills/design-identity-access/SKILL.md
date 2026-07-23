---
name: design-identity-access
description: >
  Design workload identity and an AuthZ matrix that includes an Authorize column and forbids model-held write credentials. Use as Step 12 with guardrails.
---

# Design identity & access management

## Purpose

E2E identity with platform-evaluable AuthZ density (OUTPUT-STANDARDS quality bar).

## Instructions

1. Prefer K8s workload identity (IRSA/Workload Identity / SPIFFE) — no static API keys in pods.  
2. Document paths: user→API, workload→SoR, A2A, agent→MCP, agent→LLM, human approver.  
3. Build **AuthZ matrix** with columns at least: Read · Propose · **Authorize** · Execute · Escalate · Notify.  
4. Rules: specialists Propose only; policy-gate Authorizes; executor Executes if authorized; **Model Never authorizes or executes**.  
5. MCP future path: gateway RBAC — do not assume protocol authZ is solved.  
6. **Checkpoint** with user before artifact.

## Output

`identity-access.yaml` with paths[] and authz_matrix[].
