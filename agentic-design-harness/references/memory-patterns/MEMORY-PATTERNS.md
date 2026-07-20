# Memory Patterns

| Pattern | Description | Store Examples | Use When |
|---------|-------------|----------------|----------|
| **Session** | Current conversation only | In-memory, Redis TTL | Stateless FAQ bots |
| **Episodic** | Past interactions per user | Postgres, vector + metadata | Support history |
| **Semantic** | Facts about user/org | Vector DB, knowledge graph | Personalization |
| **Procedural** | Learned workflows | Rule store, fine-tune (advanced) | Repeated processes |

## Kagent Platform Note

On Kagent: distinguish **Memory CRD** vs **Agent MemorySpec** vs substrate snapshot — validate in `kagent-platform-harness`.

## Retention & Compliance

- GDPR erasure → episodic memory must support delete-by-user
- Regulated industries → avoid storing raw PII in long-term memory; store references only

## Short vs Long Term

| Term | Typical TTL | Content |
|------|-------------|---------|
| Short | Session / 24h | Working context, tool results |
| Long | 30d–years | Preferences, case history, org facts |
