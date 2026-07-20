# Design Journal & Parallel Execution

**Write + isolate** reduces context window. **Parallel subagents** run independent research after checkpoints.

| Config | Purpose |
|--------|---------|
| `harness-journal.yaml` | What to write, isolation tiers, rollups |
| `harness-parallel.yaml` | When to fan out, subagent contracts, merge rules |
| `templates/design-journal-entry.yaml` | Entry format |

| Skills | When |
|--------|------|
| `write-design-journal` | After every step |
| `merge-parallel-research` | After parallel wave completes |

---

## Write & isolate

### Problem

Carrying full research payloads step-to-step blows the context window.

### Solution

```
Each step → full output on disk (warm tier)
         → raw fetches on disk (cold tier)
         → summary + decisions in journal (hot tier)
Parent    → loads hot tier only (+ rollup at checkpoints)
```

### Directory layout

```
agents-output/<slug>/
  journal/
    INDEX.yaml                    # table of contents
    entries/
      step-04-model-selection.yaml
      wave-post-3-merge.yaml
    rollup-through-03.yaml        # after checkpoint 3
    rollup-through-06.yaml
    payloads/                     # COLD — never in parent context
      04-pricing-fetch.yaml
  context/steps/
    04-models.yaml                # WARM — load on demand
  parallel/
    tasks/
      task-model-research-status.yaml
    merges/
      wave-post-3-merge.yaml
```

### Isolation tiers

| Tier | Contents | Parent context? |
|------|----------|-----------------|
| **Hot** | `summary`, `decisions`, rollup | Yes |
| **Warm** | `context/steps/*.yaml` | Pointer only; load field on demand |
| **Cold** | Raw MCP chunks, web HTML | Never |

### Journal entry contents

| Section | Purpose |
|---------|---------|
| `research_log` | Sources queried, freshness actions, query pointers |
| `decisions` | Structured choices + rationale |
| `summary` | ≤800 tokens for downstream steps |
| `output_pointer` | Path to full step output |
| `payload_pointers` | Paths to cold-tier raw research |

### Checkpoint rollups

After user confirms gates at Steps **1, 3, 6, 9**:

- `rollup-through-03.yaml` replaces loading steps 1–3 individually
- `rollup-through-06.yaml` replaces steps 1–6
- Parent context shrinks ~40–60% vs monolithic carry-forward

---

## Parallel subagents

### When

| Wave | Trigger | Parallel tasks |
|------|---------|----------------|
| `wave-post-3` | After Step 3 checkpoint | Step 4 models + Step 5 tools + Step 7 framework draft |
| `wave-post-6` | After Step 6 (opt-in) | Step 8 guardrails draft |

### Isolation rules

Each subagent receives **only**:

- One skill prompt (`SKILL.md`)
- Journal rollup through checkpoint (summaries, not full YAML)
- Listed `isolated_inputs.fields`
- Its scoped `sources`

Each subagent **must not** see other subagents' in-flight work.

Each subagent **writes**:

- `context/steps/NN-output.yaml`
- `journal/entries/step-NN-*.yaml`
- `parallel/tasks/{task_id}-status.yaml`

### Flow

```
Steps 1 → 2 → 3 (sequential, interactive)
         │
    checkpoint 3
         │
    ┌────┼────┐
    ▼    ▼    ▼
   S4   S5   S7-draft   ← parallel subagents
    └────┼────┘
         ▼
   merge-parallel-research
         │
    checkpoint
         ▼
   Step 6 (sequential — needs merged 4+5)
         ▼
   Step 7 refine (replaces framework draft with memory context)
         ▼
   Steps 8 → 9 → 10
```

### Always sequential

- Step 1 — user interview
- Step 3 — KPI weights need confirmation
- Step 6 — memory/KB needs merged model + tools context
- Step 10 — artifact compile

### Cursor runtime

Parent launches subagents via **Task tool** — multiple Task calls in one message:

```
Task 1: model-selection (isolated inputs from rollup-through-03)
Task 2: design-tools-integration (isolated inputs)
Task 3: select-agent-framework draft (isolated inputs)
→ merge-parallel-research
```

### Conflict resolution

| Conflict | Resolution |
|----------|------------|
| Hosting bias mismatch (models vs framework) | Ask user |
| Tool/model tier dependency | Prefer model-selection |

---

## Context window impact

| Mode | Parent loads per step |
|------|----------------------|
| Monolithic (old) | All prior step YAMLs + raw fetches |
| Journal isolated | Rollup summary + current step inputs |
| + Parallel | Rollup + merge summary (not 3× research payloads) |

Estimated savings: **40–60%** tokens in parent agent after Step 3.

---

## Enabling parallel execution

In `harness-parallel.yaml`:

```yaml
execution:
  enabled: true
```

In `harness-sources.yaml` (optional):

```yaml
execution:
  parallel:
    enabled: true
```

Parent must confirm Step 3 checkpoint before launching `wave-post-3`.
