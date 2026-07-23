---
name: fetch-online
description: >
  Fetch live reference content from web_url, git_url, or mcp_server entries.
  Use only when offline references are insufficient, the user requests live data,
  or the task needs current versions/CVEs/pricing.
---

# Fetch online

Preconditions: a `references[]` entry with `mode: online` (or offline miss).

| type | Action |
|------|--------|
| web_url | Fetch URL; prefer primary docs over SEO blogs |
| git_url | Clone/pull to `clone_dir` (or temp), read `path_in_repo` at `ref` |
| mcp_server | Call allowlisted `tools` on `server`; do not invent tool names |

Rules:

1. Check `when` on the reference before fetching.
2. Cite the canonical https URL (or MCP document id + server) in evidence registers.
3. On failure: report error, fall back to offline, ask user — do not fabricate.
4. Do not print secrets from MCP or auth headers.
5. Prefer sources listed in `references/offline/trusted-sources.md`.
