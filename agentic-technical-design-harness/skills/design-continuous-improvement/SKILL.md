---
name: design-continuous-improvement
description: >
  Design feedback loops, kill switches, and autonomy promotion gates. Use as Step 10 after evaluation.
---

# Design continuous improvement

## Purpose

Loop engineering at Accept quality (knowledgebase Ch 11, 13).

## Instructions

1. Define loops: slice promotion, trace mining, prompt/graph change, approver feedback, cost, HITL health, human-role evolution.  
2. Each loop: trigger, action, owner, **kill switch**.  
3. Autonomy promotion (Ask→Agent) is a **separate gated epic**, not silent.  
4. Cap agent tool-call loops; escalate when exceeded.  
5. Cite loop-engineering primary sources when needed.

## Output

`continuous-improvement.yaml` with loops[].
