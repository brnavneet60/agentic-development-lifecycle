---
name: design-guardrails-security
description: Cost, PII, prompt guardrails; protocols, secrets, TLS, data protection. Step 8 of agentic-design-harness E2E.
metadata:
  harness: agentic-design-harness
  step: 8
  version: "1.0.0"
---

# Design Guardrails & Security

## Purpose

E2E sections **2g Guardrails** and **2h Security**. Tie to compliance from Step 1.

## Guardrails Interview

1. **Cost** — per-request cap, daily budget, model downgrade rules?
2. **PII** — detect/redact/block? Which fields?
3. **Prompt injection** — untrusted user content in flow?
4. **Output policy** — blocked topics, tone, legal disclaimers?
5. **LLM load balancing** — multi-provider routing for resilience?
6. **Acceptable use** — what must the agent **refuse**?

## Security Interview

1. **Protocols** — mTLS service mesh, TLS 1.3 north-south, private endpoints?
2. **Secrets** — K8s secrets, Vault, cloud KMS — where do API keys live?
3. **Certificates** — ingress TLS termination point (Gateway vs app)?
4. **Token management** — OAuth for tools, short-lived tokens, rotation?
5. **Data protection** — encryption at rest, in transit, log redaction?

**Ask** for security team standards if user is unsure.

## Output

```yaml
guardrails:
  cost:
    per_request_usd_cap: <float or null>
    daily_budget_usd: <float or null>
    action_on_exceed: block | downgrade_model | alert_only
  pii:
    required: true | false
    detect: true | false
    redact_logs: true | false
    block_outbound: true | false
  prompt:
    injection_mitigation: input_sanitize | llama_guard | policy_model | none
  output:
    blocked_topics: []
    required_disclaimers: []
  load_balancing:
    enabled: true | false
    providers: []

security:
  network:
    mTLS_east_west: true | false
    tls_north_south: gateway | app | both
  secrets:
    store: kubernetes | vault | cloud_kms
    rotation_days: <int or null>
  auth:
    tool_auth: oauth | api_key | workload_identity
  data_protection:
    encrypt_at_rest: true | false
    encrypt_in_transit: true
    log_redaction: true | false
  compliance_mapping:
    - framework: GDPR
      controls: ["audit_trail", "erasure"]
```

## Next Skill

`design-observability-value-loops`
