---
description: Artifact template and delivery targets for this harness.
---

- **Standards (mandatory):** [`../OUTPUT-STANDARDS.md`](../OUTPUT-STANDARDS.md)
- **Template:** [`templates/default.md`](./templates/default.md)
- **Design brain:** [`../references/knowledgebase.md`](../references/knowledgebase.md) (id `knowledgebase`)
- **Deliverers:** `config/harness.config.yaml` → `outputs.deliverers`

Default local path (relative to the agent workspace):

```text
agents-output/agentic-technical-design-harness/<slug>/<slug>-technical-design.md
```

Revisions: use `-vN` or `-consolidated` suffixes and note deltas — do not silently overwrite an accepted artifact.

Activate `deliver-output` only after the OUTPUT-STANDARDS P0 checklist passes.
