---
name: clarify-requirements
description: >
  Capture facts, assumptions, and blocking open questions from the executive HLD or requirement summary. Use as Step 1; ask — do not invent.
---

# Clarify requirements

## Purpose

Structured requirements pack at Accept quality — facts vs assumptions vs open Qs; note HLD delivery conflicts early.

## Instructions

1. Read executive HLD / requirement summary.  
2. Extract **confirmed facts** with sources.  
3. List **assumptions** as `Assumption — planning default` with who must approve.  
4. List **open questions** with blocking impact (write path, prod, gateway, IAM, volume, etc.).  
5. If HLD Phase wording implies Day-1 full multi-agent but risk posture favors slices: draft a **delivery interpretation** (planning default) and flag Product validation — do not silently pick.  
6. Ask clarifying questions for gaps; do not invent compliance/volumes/vendors.  
7. **Checkpoint** with user.

## Output

`requirements.yaml` with facts[], assumptions[], open_questions[], hld_delivery_notes.
