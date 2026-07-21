---
name: write-design-journal
description: Record research, decisions, and planning after each harness step. Writes journal entry, isolates cold payloads to disk, updates INDEX and checkpoint rollups. Parent agent loads summaries only — not full research.
compatibility: Reads harness-journal.yaml. Runs after every skill completes.
metadata:
  harness: agentic-design-harness
  runs_after_every_step: true
  version: "1.1.0"
---

# Write Design Journal

## Purpose

**Write** — audit trail of how research and planning happened.  
**Isolate** — raw fetches go to cold tier; parent context gets summary + pointers only.

Runs **after** each skill (and after parallel wave merge).

---

## Prerequisites

- Skill output written to `context/steps/NN-*.yaml`
- Context manifest at `context/steps/NN-manifest.yaml`
- `harness-journal.yaml` loaded at bootstrap

---

## Pipeline

```
FUNCTION writeJournalEntry(step, skill, step_output, context_manifest, execution_trace):

  policy = harness-journal.skills[skill]

  // ─── 1. BUILD RESEARCH LOG ─────────────────────────────────────────

  research_log = {
    sources_consulted: context_manifest.stable_prefix.sources
                       + context_manifest.dynamic_suffix.sources,
    freshness_actions: context_manifest.freshness_actions,
    queries: execution_trace.queries,
    validation: context_manifest.validation_results,
  }

  // Move raw fetch bodies to COLD tier — never keep in entry body
  FOR EACH raw_payload IN execution_trace.raw_fetches:
    path = "journal/payloads/{step:02d}-{skill}-{hash}.yaml"
    WRITE path WITH { source_id, fetched_at, content: raw_payload }
    research_log.queries[].result_pointer = path

  // ─── 2. EXTRACT DECISIONS (hot tier) ───────────────────────────────

  decisions = []
  FOR EACH field IN policy.write.decisions:
    decisions.add({
      field: field,
      value: resolve(step_output, field),
      rationale: execution_trace.rationale[field] OR "see output_pointer"
    })

  // ─── 3. WRITE SUMMARY (max 800 tokens) ───────────────────────────

  summary = compress(
    step_output,
    fields: policy.write.summary_fields,
    max_tokens: harness-journal.isolation.rules.each_step_writes_summary_max_tokens,
    preserve: decisions + open_questions
  )

  // ─── 4. WRITE ENTRY ────────────────────────────────────────────────

  entry = {
    entry_id: "step-{step:02d}-{skill}",
    step, skill,
    recorded_at: now(),
    status: completed | failed | parallel_merged,
    research_log,
    decisions,
    summary,
    output_pointer: policy.isolate.warm,
    payload_pointers: [cold tier paths],
    subagent_id: execution_trace.subagent_id OR null,
    parent_wave_id: execution_trace.wave_id OR null,
    open_questions: step_output.open_questions OR [],
    compression_stats: { full_output_tokens, summary_tokens, cold_payload_tokens }
  }

  WRITE journal/entries/{entry_id}.yaml

  // ─── 5. UPDATE INDEX ───────────────────────────────────────────────

  index = READ journal/INDEX.yaml OR { entries: [], latest_rollup: null }
  index.entries.append({
    entry_id, step, skill, status, summary_preview: first_200_chars(summary),
    output_pointer, recorded_at
  })
  WRITE journal/INDEX.yaml

  // ─── 6. CHECKPOINT ROLLUP (after user confirms gate) ───────────────

  IF policy.rollup_trigger AND user_checkpoint_confirmed:
    rollup = mergeSummaries(index.entries through checkpoint step)
    WRITE journal/rollup-through-{step:02d}.yaml
    index.latest_rollup = "rollup-through-{step:02d}.yaml"
    WRITE journal/INDEX.yaml

  RETURN entry
```

---

## Isolation tiers (what parent loads next)

| Tier | Location | Parent loads? |
|------|----------|---------------|
| **Hot** | `summary` + `decisions` in INDEX/rollup | Yes — always |
| **Warm** | `context/steps/NN-*.yaml` | On demand via `output_pointer` |
| **Cold** | `journal/payloads/*` | Never — disk audit only |

---

## INDEX.yaml schema

```yaml
harness_run_id: "<uuid or slug-timestamp>"
started_at: "<iso8601>"
entries:
  - entry_id: step-01-capture-business-flow
    step: 1
    skill: capture-business-flow
    status: completed
    summary_preview: "Telecom order dispute flow; 500/day; PII; GDPR..."
    output_pointer: context/steps/01-flow.yaml
    recorded_at: "..."
latest_rollup: rollup-through-03.yaml
checkpoints_confirmed: [1, 3]
```

---

## Design revision journaling (mandatory)

Whenever the design artifact is revised from feedback or new information (not only after a numbered skill step):

```
FUNCTION writeRevisionJournal(trigger, delta, decisions):
  WRITE journal/entries/revision-YYYYMMDD-<label>.yaml WITH {
    revision_id,
    type: design_revision,
    timestamp: now(),
    trigger,                 # e.g. path to architect review feedback file
    prior_review: optional,
    summary,
    decisions[],             # field, value, rationale
    delta_sections_added_or_expanded[],
    harness_updates_required[],  # if standards/skills must change
    pointers: { artifact, review, output_standards }
  }
  UPDATE journal/INDEX.yaml:
    updated_at, status, entries[], reviews[]
```

**Rule:** Do not overwrite `agents-output/agentic-design-harness/<slug>/<slug>.md` without a revision journal entry.

---

## Negative Scenarios

| Scenario | Response |
|----------|----------|
| Skill failed mid-step | Write entry with `status: failed`; do not rollup |
| Summary exceeds 800 tokens | Truncate narrative; keep all `decisions` intact |
| No raw fetches | `payload_pointers: []` |
| Parallel subagent wrote entry | Include `subagent_id`; parent merges later |
| Artifact revised without journal | ERROR — write revision entry before claiming done |

---

## Next

If step was part of parallel wave → wait for `merge-parallel-research`.  
Else → `manage-design-context` for next step loads **rollup + INDEX only**.
