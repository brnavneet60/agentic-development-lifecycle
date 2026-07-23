---
name: design-evaluation
description: >
  Design slice-scoped offline/online evaluation with tool recall and parameter accuracy as first-class gates. Use as Step 9.
---

# Design evaluation

## Purpose

E2E evaluation at Accept quality — “an untested agent is an untrusted agent” (knowledgebase Ch 9).

## Instructions

1. Slice-scoped golden sets (not one blob for entire product).  
2. Scores: policy, facts, tone, routing, escalation **plus tool recall and parameter accuracy**.  
3. Default exit thresholds (Assumption unless Product overrides) — see OUTPUT-STANDARDS §7.  
4. Online canary + sampled judges; adversarial/red-team including injection and HITL bias drills.  
5. Document numeric evolve triggers for manager/critic even if labeled Assumption.  
6. Pinned judge model version; CI blocks promote on regression.  
7. Escalate to `nvidia-agent-evaluation` / primary sources as needed.

## Output

`evaluation.yaml` with suites[], metrics[], exit_gates_by_slice, evolve_triggers.
