---
name: manage-design-context
description: Select, filter, validate, and compress sources per skill before execution. Enforces freshness rules, prompt-cache-safe layout, and writes context manifest. Run at start of every harness step (including Step 0 bootstrap).
compatibility: Reads harness-sources.yaml + harness-context.yaml. Offline-first with conditional online lookup.
metadata:
  harness: agentic-design-harness
  step: 0
  version: "1.0.0"
  runs_before_every_step: true
---

# Manage Design Context

## Purpose

Bridge between **source config** (`harness-sources.yaml`) and **skill execution**. Before each skill runs:

1. **Select** sources for this step (priority, fallback, freshness)
2. **Filter** fetched data (age, relevance, authority, dedupe)
3. **Validate** content and constraints
4. **Compress** to fit token budget without losing critical facts
5. **Layout** stable prefix vs dynamic suffix for **prompt caching**
6. **Write** context manifest for audit

---

## Prerequisites

- `harness-sources.yaml` (source registry)
- `harness-context.yaml` (this policy)
- Prior step outputs in `{project_root}/context/steps/` (if any)
- Optional: `{project_root}/constraints.yaml`

---

## Step 0 — Bootstrap (once per harness run)

```
FUNCTION bootstrapContext(project_slug):

  LOAD harness-sources.yaml
  LOAD harness-context.yaml
  LOAD harness-journal.yaml
  LOAD harness-parallel.yaml
  RESOLVE paths.project_root = {project_root}/

  CREATE directories:
    - context/steps/
    - context-state/
    - curation-state/
    - journal/entries/
    - journal/payloads/
    - parallel/tasks/
    - parallel/merges/

  INIT journal/INDEX.yaml IF NOT EXISTS

  EMIT bootstrap summary:
    - online sources enabled
    - offline sources available
    - prompt_caching.enabled
    - cache_stable_sources list

  PROCEED to capture-business-flow (Step 1)
```

---

## Per-Step Pipeline (runs before EVERY skill)

```
FUNCTION assembleContext(skill_name, prior_outputs):

  policy = harness-context.skills[skill_name]
  caching = harness-context.prompt_caching

  // ─── 1. SELECT SOURCES ───────────────────────────────────────────

  selected = []

  FOR EACH source_policy IN policy.sources (in order):

    source = resolveSource(source_policy.id)    // from harness-sources.yaml

    IF source.mode == offline:
      freshness = checkFreshness(source)
      // freshness: compare now - created_at vs max_age_days / stale_after_days

      IF freshness == fresh:
        selected.add({ source, tier: source_policy.cache_tier, content: loadFile(source.path) })

      ELSE IF freshness == stale AND source.created_from:
        IF source_policy.freshness.if_stale == lookup_online:
          online = fetchOnline(source.created_from, source_policy.filters)
          selected.add({ source: source.created_from, tier: dynamic_suffix, content: online, tag: live_fetch })
          LOG freshness_action: "stale offline → online lookup"
          // optional: queue curation_job to refresh offline for next run

      ELSE IF source_policy.role == fallback:
        selected.add({ source, tier: source_policy.cache_tier, content: loadFile, warn: stale })

      ELSE IF source_policy.only_if conditions not met:
        SKIP

    ELSE IF source.mode == online:
      IF NOT source.enabled: SKIP with warning
      IF source_policy.use_when:
        EVALUATE use_when triggers (stale sibling, user_requests_refresh, requires_live_pricing)
        IF NOT triggered: SKIP
      content = fetchOnline(source, source_policy.filters)
      selected.add({ source, tier: dynamic_suffix, content, fetched_at: now() })

  // Apply global selection.order (curated over builtin, etc.)
  selected = applySelectionOrder(selected)

  // ─── 2. FILTER ─────────────────────────────────────────────────────

  FOR EACH item IN selected:
    IF item.fetched_at AND max_age_days set:
      IF age(item) > max_age_days: DROP item; LOG "too old"

    IF item.source.type == mcp AND rag chunks:
      DROP chunks WHERE relevance < min_relevance

    IF deduplication enabled:
      DEDUPE by content_hash; keep highest authority

  // ─── 3. VALIDATE ───────────────────────────────────────────────────

  results = []

  FOR EACH rule IN harness-context.validation.on_fetch + policy.validation:
    results.add(runRule(rule, selected))

  FOR EACH rule IN harness-context.validation.on_content:
    results.add(runRule(rule, selected))

  IF constraints_never_contradicted FAILS:
    FLAG conflict; ASK user — do not proceed silently

  IF pricing_must_have_verified_date FAILS AND step == model-selection:
    TRIGGER lookup_new_content for web-vendor-pricing

  IF any required source missing:
    IF fallback defined: use fallback
    ELSE: ASK user or SKIP with explicit warning in manifest

  // ─── 4. COMPRESS ───────────────────────────────────────────────────

  stable_blocks = []
  dynamic_blocks = []

  FOR EACH item IN selected:
    IF item.tier == stable_prefix:
      IF caching.enabled:
        // LOSSLESS only in stable prefix — never summarize
        content = compress(item.content, strategy=structured_yaml_extract OR none)
      stable_blocks.add(item)

    ELSE:  // dynamic_suffix
      budget = policy.compression.token_budget OR default
      content = compress(item.content,
        strategy = policy.compression.strategy,
        preserve = harness-context.compression.preserve_always,
        max_tokens = budget)
      dynamic_blocks.add(item)

  // Compress prior step inputs (dynamic suffix only)
  IF policy.inputs_from_steps:
    // ISOLATION: load journal rollup — not full step YAML files
    IF harness-journal.enabled:
      prior = loadJournalIsolatedContext(step, policy.inputs_from_steps)
      // prior = { index, latest_rollup summaries, pointers }
    ELSE:
      prior = loadPriorSteps(policy.inputs_from_steps)
    IF policy.compression.prior_step_inputs == session_rollup:
      prior = load("{project_root}/context/context-summary-through-N.yaml")
    prior_compressed = compress(prior,
      strategy = policy.compression.prior_step_inputs,
      preserve = preserve_always)
    dynamic_blocks.prepend({ type: prior_step_inputs, content: prior_compressed })

  ENFORCE token_budgets:
    stable_prefix_total <= caching.stable_prefix_max
    dynamic_suffix_total <= caching.dynamic_suffix_max

  // ─── 5. PROMPT CACHE LAYOUT ────────────────────────────────────────

  prompt_layout = {
    stable_prefix: concat(stable_blocks)   // FIXED ORDER — never reorder
    dynamic_suffix: concat(dynamic_blocks) // append-only
  }

  RULES (if caching.enabled):
    - NEVER insert dynamic content into stable_prefix
    - NEVER reorder stable_prefix blocks between steps in same session
    - dynamic_suffix: new fetches append at end; do not prepend mid-suffix
    - formatting: deterministic YAML key order in stable blocks

  // ─── 6. WRITE MANIFEST ─────────────────────────────────────────────

  WRITE context/steps/{step}-manifest.yaml:
    step, skill, assembled_at
    stable_prefix: { sources, tokens }
    dynamic_suffix: { sources, fetched_at, fresh, compressed, tokens }
    freshness_actions, validation_results, compression_applied, dropped_content

  RETURN prompt_layout TO skill executor
```

---

## Load Isolated Context (journal-based)

```
FUNCTION loadJournalIsolatedContext(current_step, required_steps):

  index = READ journal/INDEX.yaml
  rollup = latest rollup-through-NN where N < current_step AND checkpoint confirmed

  hot = {
    index_entries: index.entries WHERE step < current_step,
    rollup_summary: rollup.combined_summaries,
    decisions: rollup.all_decisions,
    open_questions: rollup.all_open_questions,
  }

  // Warm tier: load only if skill policy lists explicit field
  pointers = index.entries[].output_pointer

  NEVER LOAD:
    - journal/payloads/*           // cold tier
    - full step YAML unless pointer resolve requested

  RETURN hot
```

---

## Freshness Decision Table

| Offline state | `created_from` | Policy `if_stale` | Action |
|---------------|----------------|-------------------|--------|
| Fresh | any | — | Use offline file |
| Stale | set | `lookup_online` | Fetch from online parent → dynamic suffix |
| Stale | set | `lookup_online` + job | Fetch online + queue curation_job |
| Stale | null | — | Warn; use offline (builtin) |
| Missing | set | — | Fetch online parent |
| User requests refresh | any | — | Force online lookup; tag `live_fetch` |

---

## Compression vs Prompt Caching

| Zone | Compression allowed? | Strategies |
|------|---------------------|------------|
| **stable_prefix** | Lossless only | `none`, `structured_yaml_extract` |
| **dynamic_suffix** | Full | `key_facts_bullets`, `structured_yaml_extract`, `retrieve_pointer`, `session_rollup` |

**Never compress away:** `preserve_always` fields (constraints, compliance, failure_modes, open_questions, provenance).

**Session rollup** (after Steps 3 and 6): write `context-summary-through-N.yaml`; later steps load summary instead of full prior YAML → shrinks dynamic suffix without touching stable prefix.

---

## Lookup New Content

Triggered when:

- Offline source exceeds `max_age_days` / `stale_after_days`
- Step has `requires_live_pricing: true`
- Validation fails (`pricing_must_have_verified_date`)
- User says "refresh", "lookup latest", "use current pricing"
- Curated offline file missing but `created_from` online source enabled

```
FUNCTION lookupNewContent(offline_source_id):
  online_id = offline_source.created_from
  IF online_id is null: RETURN cannot_refresh
  content = fetchOnline(online_id, filters from skill policy)
  VALIDATE content
  APPEND to dynamic_suffix with tags: { live_fetch, fetched_at, source_id }
  OPTIONAL: run matching curation_job to update offline for next session
  LOG in freshness_actions
```

---

## Negative Scenarios

| Scenario | Response |
|----------|----------|
| Online source disabled but offline stale | Warn; use stale offline; flag in artifact |
| All chunks below relevance threshold | Ask user for narrower query or skip RAG |
| Compression would drop preserved field | Use `structured_yaml_extract` instead of bullets |
| Stable prefix exceeds max tokens | Split: move non-cache-stable refs to dynamic suffix |
| Prompt caching on + user answer mid-stable | User answers go to dynamic_suffix only |
| Constraint conflict in fetched data | Stop; ask user to resolve |

---

## Output

Pass to skill:

```yaml
context_package:
  skill: model-selection
  prompt_layout:
    stable_prefix: "<deterministic cached content>"
    dynamic_suffix: "<compressed dynamic content>"
  manifest_path: context/steps/04-manifest.yaml
  freshness_actions: [...]
  open_questions: [...]
```

Skill uses `context_package` — does not re-fetch sources independently.

---

## After Skill Completes

Hand off to `write-design-journal` to persist research log and isolate cold payloads.

If parallel wave active, subagent writes its own journal entry; parent runs `merge-parallel-research`.

---

## Next

After context assembled, execute the skill (e.g. `model-selection/SKILL.md`) using only `context_package`.
