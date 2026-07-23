# Curation Sources Map

This file documents **where offline reference packs are curated from**.  
Use these URLs as primary evidence during curation and refresh jobs.

## Design patterns and orchestration

- LangGraph concepts and multi-agent routing: [https://langchain-ai.github.io/langgraph/concepts/multi_agent/](https://langchain-ai.github.io/langgraph/concepts/multi_agent/)
- LangChain / LangGraph docs home: [https://python.langchain.com/docs/introduction/](https://python.langchain.com/docs/introduction/)
- CrewAI docs: [https://docs.crewai.com/](https://docs.crewai.com/)
- Microsoft AutoGen docs: [https://microsoft.github.io/autogen/stable/](https://microsoft.github.io/autogen/stable/)
- Semantic Kernel docs: [https://learn.microsoft.com/semantic-kernel/](https://learn.microsoft.com/semantic-kernel/)
- Albada, *Building Applications with AI Agents* (O'Reilly): [https://www.oreilly.com/library/view/building-applications-with/9781098176495/](https://www.oreilly.com/library/view/building-applications-with/9781098176495/)
- Book companion scenarios / eval harness: [https://github.com/michaelalbada/BuildingApplicationsWithAIAgents](https://github.com/michaelalbada/BuildingApplicationsWithAIAgents)

## Models, pricing, and benchmarks

- OpenAI pricing: [https://openai.com/api/pricing/](https://openai.com/api/pricing/)
- Anthropic pricing: [https://www.anthropic.com/pricing](https://www.anthropic.com/pricing)
- Google AI pricing: [https://ai.google.dev/pricing](https://ai.google.dev/pricing)
- Artificial Analysis: [https://artificialanalysis.ai/](https://artificialanalysis.ai/)
- LMSYS Chatbot Arena: [https://lmarena.ai/](https://lmarena.ai/)
- Hugging Face Open LLM Leaderboard: [https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard)

## Memory, knowledge, and RAG

- OpenAI embeddings guide: [https://platform.openai.com/docs/guides/embeddings](https://platform.openai.com/docs/guides/embeddings)
- Anthropic prompt engineering overview: [https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
- Weaviate RAG patterns: [https://weaviate.io/developers/weaviate/starter-guides/generative](https://weaviate.io/developers/weaviate/starter-guides/generative)
- Elasticsearch RAG documentation: [https://www.elastic.co/docs/solutions/search/rag](https://www.elastic.co/docs/solutions/search/rag)

## Security and guardrails

- OWASP LLM Top 10: [https://genai.owasp.org/llm-top-10/](https://genai.owasp.org/llm-top-10/)
- NIST AI Risk Management Framework: [https://www.nist.gov/itl/ai-risk-management-framework](https://www.nist.gov/itl/ai-risk-management-framework)
- OpenTelemetry docs: [https://opentelemetry.io/docs/](https://opentelemetry.io/docs/)

## Curation policy

- Only curate from official docs, standards bodies, and reproducible benchmark sources.
- Record `curated_at` and `source_url` metadata in generated offline files.
- If a source URL changes, update this map before the next curation run.
- **Artifact citation rule:** Design artifacts must cite these **web URLs** (or equivalent primary papers/case studies). Never cite this markdown file — or any other harness `references/*.md` — as Evidence Register evidence.
