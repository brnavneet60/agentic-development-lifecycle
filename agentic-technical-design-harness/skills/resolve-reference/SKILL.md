---
name: resolve-reference
description: >
  Resolve harness reference ids from config/harness.config.yaml to concrete
  paths or locators. Prefer mode offline. Use when the task needs evidence,
  standards, playbooks, or any configured reference resource.
---

# Resolve reference

1. Read `config/harness.config.yaml` → `references`.
2. Match by `id` or by `description` relevance to the task.
3. If `mode: offline` (local_file, local_dir, doc, or mirrored git):
   - Read the local `path` (or path under `references/offline/`).
4. If only online sources match, or offline content is missing/stale for the question:
   - Activate `fetch-online` with the reference `id`.
5. Return: id, type, mode, locator used, and short excerpt / path for the caller.
6. Never treat harness-internal paths as citable external evidence in final artifacts;
   when a curated offline pack has an original `source_url`, prefer that URL in citations.
