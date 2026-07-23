---
description: Artifact template and delivery targets for this harness.
---

- **Standards (mandatory):** [`../OUTPUT-STANDARDS.md`](../OUTPUT-STANDARDS.md)
- **Template:** [`templates/default.md`](./templates/default.md)
- **Design brain:** [`../references/knowledgebase.md`](../references/knowledgebase.md) (id `knowledgebase`)
- **Deliverers:** `config/harness.config.yaml` → `outputs.deliverers`

Default local path is **configurable** (`outputs.deliverers[].path` / `project_root`). No shared testing tree is required.

If unset, a reasonable default is:

```text
runs/<slug>/<slug>-technical-design.md
```

Revisions: use `-vN` or `-consolidated` suffixes and note deltas — do not silently overwrite an accepted artifact.

Activate `deliver-output` only after the OUTPUT-STANDARDS P0 checklist passes.
