# Trusted Sources for Model & Benchmark Research

Use **only** these source classes when researching models in Step 4. Flag anything else as **unverified**.

## Vendor Official

| Provider | Pricing / Models | Benchmarks / Docs |
|----------|------------------|-------------------|
| OpenAI | https://developers.openai.com/api/docs/pricing | https://platform.openai.com/docs/models |
| Anthropic | https://claude.com/platform/api | https://docs.anthropic.com |
| Google | https://ai.google.dev/pricing | https://ai.google.dev/gemini-api/docs |
| Meta (Llama) | https://llama.meta.com | Hugging Face model cards |
| Mistral | https://mistral.ai/pricing | https://docs.mistral.ai |

## Independent Benchmarks

| Source | Use For |
|--------|---------|
| [Artificial Analysis](https://artificialanalysis.ai/) | Leaderboards, latency, price-performance |
| [LMSYS Chatbot Arena](https://chat.lmsys.org/) | Subjective quality rankings |
| [Hugging Face Open LLM Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard) | Open-weight benchmarks |
| Papers with Code | Task-specific SOTA (cite paper) |

## Self-Host Sizing

| Source | Use For |
|--------|---------|
| `references/compute-sizing/COMPUTE-SIZING.md` | VRAM formulas |
| Hugging Face model cards | Parameter count, context length |
| NVIDIA / cloud GPU docs | Instance types |

## Do NOT Use as Primary Evidence

- Unattributed blog posts
- Social media claims
- Model marketing without benchmark link
- Training-data cutoff anecdotes without task match

## When Catalog Is Stale

1. Check vendor pricing page (date in artifact)
2. Cross-check Artificial Analysis or vendor benchmark sheet
3. Note `pricing_verified_date` in output
