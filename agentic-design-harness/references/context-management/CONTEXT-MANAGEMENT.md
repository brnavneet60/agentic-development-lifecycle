# Context Management

How the harness selects, filters, validates, and compresses source data per skill — without breaking prompt caching.

**Config files:**

| File | Defines |
|------|---------|
| `harness-sources.yaml` | What sources exist (online/offline) |
| `harness-context.yaml` | How sources are used per skill |

**Skill:** `skills/manage-design-context/SKILL.md` — runs before every step.

---

## Architecture

```
harness-sources.yaml          harness-context.yaml
   (what exists)                 (how to use)
         │                              │
         └──────────┬───────────────────┘
                    ▼
         manage-design-context (per step)
                    │
      ┌─────────────┼─────────────┐
      ▼             ▼             ▼
   SELECT        FILTER       VALIDATE
      │             │             │
      └─────────────┼─────────────┘
                    ▼
              COMPRESS
                    │
      ┌─────────────┴─────────────┐
      ▼                           ▼
 stable_prefix              dynamic_suffix
 (prompt cache safe)         (compressed, fresh fetches)
      │                           │
      └─────────────┬─────────────┘
                    ▼
            skill execution
                    ▼
         context/steps/NN-manifest.yaml
```

---

## Skill ↔ source mapping

Defined in `harness-context.yaml` → `skills.<skill-name>.sources`:

| Field | Purpose |
|-------|---------|
| `role` | `required`, `primary`, `fallback`, `refresh`, `supplement`, `optional` |
| `cache_tier` | `stable_prefix` or `dynamic_suffix` |
| `freshness.max_age_days` | When offline is considered stale |
| `freshness.if_stale` | `lookup_online` → fetch from `created_from` |
| `use_when` | Only fetch online when triggers fire (stale, live pricing, user refresh) |
| `only_if` | Conditional fetch (e.g. `needs_knowledge_retrieval`) |
| `filters` | `max_results`, `min_relevance`, `tags`, `max_age_days` |
| `compression` | Strategy + token budget for this source |

Example — model selection with stale catalog refresh:

```yaml
model-selection:
  requires_live_pricing: true
  sources:
    - id: ref-model-catalog-curated
      role: primary
      freshness:
        max_age_days: 30
        if_stale: lookup_online
      fallback: ref-model-catalog
    - id: web-vendor-pricing
      role: refresh
      cache_tier: dynamic_suffix
      use_when: [ref-model-catalog_stale, ref-model-catalog-curated_stale]
```

---

## Selection order (global)

1. Offline if **fresh**
2. Offline **curated** (`*-curated`) over harness **builtin** if both fresh
3. If offline **stale** → `lookup_online` via `created_from`
4. Online sources in step binding when `use_when` triggers fire
5. Never use unverified content without flagging

---

## Filtering

| Filter | Applies to | Effect |
|--------|------------|--------|
| `max_age_days` | Any fetched content | Drop older than N days |
| `min_relevance` | MCP RAG chunks | Drop below threshold (e.g. 0.6) |
| `tags` | MCP RAG | Scope query to tag set |
| `top_k` / `max_results` | MCP, web | Limit volume |
| `authority_filter` | All | Prefer authoritative over advisory |
| `dedupe_by: content_hash` | All | Remove duplicate content |

---

## Validation

| Rule | When | On fail |
|------|------|---------|
| `source_must_be_in_step_binding` | Fetch | Reject |
| `pricing_must_have_verified_date` | model-selection | Trigger live pricing lookup |
| `rag_chunks_must_have_relevance_score` | mcp-document-rag | Drop chunk |
| `constraints_never_contradicted` | All steps | Ask user |
| `must_have_source_id_and_fetched_at` | All content | Reject |

Every step writes `context/steps/NN-manifest.yaml` with validation results.

---

## Compression

### Preserve always (never drop)

- `flow.regulatory_compliance`, `flow.constraints`
- `project_constraints`, `failure_modes`, `open_questions`
- `compliance_notes`, `user_confirmed_decisions`, `source_provenance`

### Strategies

| Strategy | Use | Typical savings |
|----------|-----|-----------------|
| `structured_yaml_extract` | Prior step YAML | 40–60% |
| `key_facts_bullets` | RAG / web prose | 50–70% |
| `retrieve_pointer` | Large prior steps | 80–90% (store path, load on demand) |
| `session_rollup` | After Steps 3, 6 | Replaces multiple step files with one summary |

### Token budgets

| Zone | Default max |
|------|-------------|
| Stable prefix | 6,000 tokens |
| Dynamic suffix | 8,000 tokens |
| Per-step total | 12,000 tokens |

---

## Prompt caching safety

Providers cache identical **prefixes**. Layout rules:

```
┌─────────────────────────────────────┐
│  STABLE PREFIX (cached)              │
│  - harness instructions             │
│  - skill template                   │
│  - offline cache_stable sources     │
│  - project constraints              │
│  - LOSSLESS compression only        │
├─────────────────────────────────────┤
│  DYNAMIC SUFFIX (not cached)        │
│  - prior step outputs (compressed)  │
│  - live fetches (pricing, RAG)      │
│  - user answers this session        │
│  - session rollups                  │
│  - FULL compression allowed         │
└─────────────────────────────────────┘
```

**Do:**

- Keep stable block **order fixed** across steps in a session
- Append new fetches to **end** of dynamic suffix
- Put user interview answers in dynamic suffix only
- Use deterministic YAML field ordering in stable prefix

**Do not:**

- Insert live pricing or RAG results into stable prefix
- Reorder stable prefix blocks between steps
- Summarize or bullet-compress stable prefix content
- Prepend volatile content mid-dynamic-suffix

Sources marked `cache_stable` in `harness-context.yaml` → `prompt_caching.cache_stable_sources`.

---

## Session rollup checkpoints

After Steps **3** and **6**, write:

```
agents-output/<slug>/context/context-summary-through-3.yaml
agents-output/<slug>/context/context-summary-through-6.yaml
```

Later steps load rollup instead of full step 1–3 or 1–6 YAML → smaller dynamic suffix, stable prefix unchanged.

---

## Lookup new content

| Trigger | Action |
|---------|--------|
| Offline `created_at` + age > `max_age_days` | Fetch `created_from` online source |
| `requires_live_pricing: true` | Always fetch `web-vendor-pricing` |
| User requests refresh | Force online lookup; tag `live_fetch` |
| Validation: missing verified date | Re-fetch pricing |
| Curated file missing | Fetch online parent; optional curation job |

Live fetch always lands in **dynamic_suffix** with `fetched_at` and `source_id` tags.

---

## Per-step manifest example

```yaml
step: 4
skill: model-selection
assembled_at: "2026-07-16T10:00:00Z"
prompt_caching_enabled: true
stable_prefix:
  sources: [ref-benchmark-matrix, ref-model-catalog, ref-cost-model]
  total_tokens: 4200
dynamic_suffix:
  sources:
    - id: web-vendor-pricing
      fetched_at: "2026-07-16T10:00:05Z"
      fresh: true
      compressed: structured_yaml_extract
      tokens: 1800
freshness_actions:
  - source_id: ref-model-catalog-curated
    action: lookup_online
    reason: stale_32_days
validation_results:
  - rule: pricing_must_have_verified_date
    pass: true
compression_applied:
  - target: prior_step_inputs
    strategy: structured_yaml_extract
    tokens_before: 6000
    tokens_after: 3200
```
