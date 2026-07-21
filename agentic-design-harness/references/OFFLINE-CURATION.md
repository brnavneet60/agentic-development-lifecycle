# Offline Curation Guide

Simple model: **one source list**, two modes, one job pipeline.

Primary curation URL catalog: `references/curation-sources/CURATION-SOURCES.md`.

---

## Source list

Every entry in `harness-sources.yaml` → `sources:` is either **online** or **offline**.

| mode | type | Example |
|------|------|---------|
| `online` | `web_search` | Vendor pricing URLs |
| `online` | `mcp` | Document RAG (PDF in vector DB), Confluence, Jira |
| `online` | `tool` | WebSearch tool |
| `offline` | `file` | `DESIGN-PATTERNS.md` |
| `offline` | `directory` | `domain-kb/` folder |

### PDF ebook

A PDF is **not** an offline source directly. Flow:

1. Upload PDF to vector DB
2. Register as **online** MCP source (`mcp-document-rag`)
3. Optionally run a **curation job** to materialize offline extracts

```
PDF file  →  vector DB  →  mcp-document-rag (online)
                              │
                              ▼ curation_job
                         ref-design-patterns-curated (offline)
                         created_from: mcp-document-rag
```

---

## Offline provenance: `created_from`

Every offline source has:

```yaml
- id: ref-design-patterns-curated
  mode: offline
  path: "{project_root}/curated/design-patterns/DESIGN-PATTERNS.md"
  created_from: mcp-document-rag    # online source that produced this file
  created_at: null                  # set by curation job on first run
  version: null
```

| `created_from` | Meaning |
|----------------|---------|
| `null` | Harness builtin — never derived from an online source |
| `<online-source-id>` | This offline file was built from that online source |

---

## Curation jobs

Jobs connect **online → offline**. They are **incremental** and **idempotent**.

Every curation run must log:
- `source_url` (from `CURATION-SOURCES.md` or source registry)
- `curated_at` (UTC timestamp)
- `source_version` (if available from vendor docs)

```yaml
curation_jobs:
  - id: job-design-patterns-from-ebook
    from_source: mcp-document-rag       # online
    to_source: ref-design-patterns-curated  # offline
    strategy:
      incremental: true
      idempotent: true
      state_file: "{project_root}/curation-state/job-design-patterns.json"
      change_detection: chunk_hash
```

### Incremental

- Track content hash per chunk/section in `state_file`
- On re-run, **skip unchanged** chunks
- Only merge new or modified content

### Idempotent

- Re-running with no upstream changes → **identical output**, no duplicates
- Safe to schedule (daily, weekly, on_source_change)

### Pseudo-code

```
state = load(state_file)
chunks = fetch(from_source, extract config)

for chunk in chunks:
  hash = sha256(chunk)
  if state[chunk.id].hash == hash:
    continue                    # unchanged — skip
  merge(chunk, to_source)        # upsert section or file
  state[chunk.id] = { hash, updated_at }

save(state_file)
update offline source created_at + version
```

---

## Using curated offline vs live online

At runtime (`runtime.prefer_offline_when_fresh: true`):

1. Use offline file if it exists and is not stale
2. If stale and `created_from` is set → fall back to that online source
3. Log which source was used in `decisions.log`

---

## Quick setup: ebook as design brain

```yaml
# 1. Enable online MCP (PDF already in vector DB)
- id: mcp-document-rag
  mode: online
  type: mcp
  enabled: true
  config:
    group_name: agentic-design-brain

# 2. Offline target (empty until job runs)
- id: ref-design-patterns-curated
  mode: offline
  created_from: mcp-document-rag
  path: "{project_root}/curated/design-patterns/DESIGN-PATTERNS.md"

# 3. Enable job
curation_jobs:
  - id: job-design-patterns-from-ebook
    enabled: true
    from_source: mcp-document-rag
    to_source: ref-design-patterns-curated
```

Run job once → offline file populated. Re-run anytime → only changed sections update.
