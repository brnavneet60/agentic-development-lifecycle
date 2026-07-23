---
name: design-guardrails
description: >
  Design autonomy slider, layered controls, and HITL failure-mode mitigations. Use as Step 11 with identity design.
---

# Design guardrails

## Purpose

E2E guardrails at Accept quality: Manual/Ask/Agent, OWASP-aligned controls, HITL human factors (knowledgebase Ch 3, 12, 13).

## Instructions

1. Define **autonomy slider** defaults per action class (explain vs write vs high-risk).  
2. Map threats → admission / request / runtime controls (PII, injection, allowlists, token/cost, NetworkPolicy).  
3. Mandate architectural separation: specialists **cannot execute** irreversible writes; **policy-gate** authorizes.  
4. Document **HITL failure modes**: automation bias, alert fatigue, skill decay, misaligned incentives — with mitigations.  
5. Link to `design-identity-access`.  
6. Decision discipline per control layer.

## Output

`guardrails.yaml` with autonomy_modes, controls[], hitl_failure_modes[].
