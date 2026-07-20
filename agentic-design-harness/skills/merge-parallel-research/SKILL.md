---
name: merge-parallel-research
description: Merge outputs from parallel subagents after a wave completes. Resolve conflicts, write wave merge journal entry, checkpoint before continuing to sequential steps.
compatibility: Reads harness-parallel.yaml + harness-journal.yaml. Runs after parallel wave.
metadata:
  harness: agentic-design-harness
  version: "1.0.0"
---

# Merge Parallel Research

## Purpose

Parent orchestrator merges isolated subagent results from a **parallel wave** (e.g. post-Step 3 fan-out: models + tools + framework draft).

Subagents do not see each other's context. Parent validates, resolves conflicts, writes merge journal.

---

## Prerequisites

- Wave triggered per `harness-parallel.yaml`
- Checkpoint confirmed after trigger step (e.g. Step 3)
- All `task.outputs.step_file` exist OR `on_fail` policy applied
- Each task wrote `journal/entries/step-NN-*.yaml`

---

## Pipeline

```
FUNCTION mergeParallelWave(wave_id):

  wave = harness-parallel.waves[wave_id]
  results = {}

  // ─── 1. COLLECT SUBAGENT OUTPUTS ───────────────────────────────────

  FOR EACH task IN wave.tasks:
    status = READ parallel/tasks/{task.task_id}-status.yaml
    IF status.failed:
      APPLY task.on_fail  // block_wave_merge | continue_with_warning
    results[task.task_id] = {
      step_file: READ task.outputs.step_file,
      journal: READ task.outputs.journal_entry,
    }

  IF block_wave_merge triggered:
    REPORT failures; ASK user; STOP

  // ─── 2. CONFLICT DETECTION ─────────────────────────────────────────

  conflicts = []
  FOR EACH rule IN wave.merge.conflicts:
    IF detect(rule.between, results):
      conflicts.add(rule)

  FOR EACH conflict:
    IF resolve == ask_user:
      PRESENT side-by-side comparison from journal summaries
      WAIT user decision
    IF resolve == prefer_model_selection_for_llm_tier:
      APPLY model-selection decision over tools inference

  // ─── 3. WRITE MERGE ARTIFACT ───────────────────────────────────────

  merge = {
    wave_id,
    merged_at: now(),
    tasks: [task_id + status + summary from each journal],
    conflicts_detected: conflicts,
    conflicts_resolved: [...],
    combined_decisions: union of hot-tier decisions from all tasks,
    pointers: {
      models: context/steps/04-models.yaml,
      tools: context/steps/05-tools.yaml,
      framework_draft: context/steps/07-framework-draft.yaml,
    },
    next_sequential_step: 6,
    refine_required: [step 7 after step 6 per harness-parallel.refine_after_parallel],
  }

  WRITE parallel/merges/{wave_id}-merge.yaml

  // ─── 4. JOURNAL ENTRY FOR WAVE ─────────────────────────────────────

  writeJournalEntry(
    step: wave.trigger.after_step,
    skill: merge-parallel-research,
    status: parallel_merged,
    summary: "Wave {wave_id}: {n} tasks merged; {conflict_count} conflicts resolved",
    output_pointer: parallel/merges/{wave_id}-merge.yaml
  )

  // ─── 5. CHECKPOINT ─────────────────────────────────────────────────

  IF wave.merge.checkpoint_before_continue:
    PRESENT merge summary table to user
    ASK: "Parallel research merged — continue to Step 6 (memory/knowledge)?"
    WAIT confirmation

  PROCEED to design-memory-knowledge (Step 6)
```

---

## Launching subagents (Cursor runtime)

Parent uses **Task tool** — one task per `wave.tasks[]`:

```
Task prompt template:

  You are an isolated subagent for agentic-design-harness.
  Skill: {skill} — read agentic-design-harness/skills/{skill}/SKILL.md
  Inputs (from journal rollup only): {isolated_inputs.fields}
  Sources allowed: {sources}
  Run manage-design-context for this skill only.
  Write output: {outputs.step_file}
  Write journal via write-design-journal skill.
  Write status: parallel/tasks/{task_id}-status.yaml
  Do NOT access other parallel task outputs.
```

Launch all tasks in **one message with multiple Task calls** for true parallelism.

---

## Wave post-3 diagram

```
Step 3 checkpoint confirmed
         │
         ├──────────────┬──────────────┐
         ▼              ▼              ▼
   subagent:4     subagent:5     subagent:7-draft
   model-select   tools          framework
         │              │              │
         └──────────────┼──────────────┘
                        ▼
              merge-parallel-research
                        │
                        ▼ checkpoint
                   Step 6 sequential
                        │
                        ▼
              Step 7 refine framework (full context)
```

---

## Negative Scenarios

| Scenario | Response |
|----------|----------|
| One subagent timeout | Apply `on_fail`; continue or block per task policy |
| Conflicting hosting bias | `ask_user` per merge rules |
| Framework draft stale after Step 6 | Re-run Step 7 sequentially with `refine_after_parallel` |
