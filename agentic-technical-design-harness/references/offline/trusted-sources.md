# Trusted Sources for Technical Design Evidence

Use **only** these source classes when citing design evidence. Flag anything else as **unverified**.

## Allowed classes

| Class | Examples |
|-------|----------|
| Vendor primary docs | OpenAI, Anthropic, Google, LangChain/LangGraph, CrewAI, AutoGen, Semantic Kernel |
| Independent benchmarks | Artificial Analysis, LMArena, Hugging Face Open LLM Leaderboard |
| Standards / security | OpenTelemetry, NIST, OWASP LLM Top 10, CNCF project docs |
| Research / white papers | Peer-reviewed papers, reputable vendor engineering blogs with reproducible claims |
| Industry use cases | Named case studies with resolvable https URLs |

## Do NOT use as primary evidence

- Unattributed Medium/SEO posts
- Social media claims without primary link
- Harness-internal paths (`references/*.md`, skill files) as citations in the TDD
- Marketing pages without technical substance

## Citation rule

In the final Technical Design Document, cite the original `https://` URL. Offline stubs are lookup aids only.
