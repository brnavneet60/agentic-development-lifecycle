# Quality baseline

**Rule:** Every harness run must meet **OUTPUT-STANDARDS.md** (current major version) before calling `deliver-output`.

That bar requires:

- Knowledgebase-first design (`references/knowledgebase.md`)
- Sequence ≠ end-state (sliced MVP vs target topology)
- Propose → non-LLM authorize → execute for irreversible actions
- Named models with dated pricing
- PDM epic → slice → gate → KPI map and prompt governance
- Platform density (AuthZ matrix with Authorize column, K8s resilience notes)
- Tool recall / parameter accuracy in eval
- Full external evidence URLs (plus book title + chapter for knowledgebase claims)

Stakeholder closures (Product sign-off, legal, vendor DPAs) remain **per use case** process gates — they do not excuse omitting architecture sections.
