# Compute Sizing Reference — Self-Hosted LLM Inference

**Version:** 0.1.0 | **Last Updated:** 2026-07-06

> Indicative sizing only. Validate with benchmark on your workload before procurement.
> Sources: [Hugging Face Llama 3.1 blog](https://huggingface.co/blog/llama31), [llmrun VRAM calculator](https://llmrun.dev/model/meta-llama-meta-llama-3-70b)

---

## 1. VRAM Formula

```
weight_vram_gb = params_billion × bytes_per_param

bytes_per_param:
  FP16/BF16 = 2
  FP8       = 1
  INT4      = 0.5

total_vram_gb = weight_vram_gb × workload_multiplier + kv_cache_gb

workload_multiplier:
  dev/single-user     = 1.5
  production batched  = 1.8
  long-context heavy  = 2.5
```

---

## 2. Model Size Reference Table

| Params | FP16 VRAM | INT8 VRAM | INT4 VRAM | Min Production GPU |
|--------|-----------|-----------|-----------|-------------------|
| 3B | 6 GB | 3 GB | 2 GB | T4, RTX 3060 |
| 8B | 16 GB | 8 GB | 4 GB | L4, RTX 4090, A10G |
| 14B | 28 GB | 14 GB | 7 GB | A10G, L40S |
| 70B | 140 GB | 70 GB | 35–48 GB | A100 40GB (INT4), 2×A100 80GB (FP16) |
| 72B | 144 GB | 72 GB | 36–50 GB | Same as 70B class |
| 405B | 810 GB | 405 GB | 203 GB | 8× H100 (FP8) |

---

## 3. KV Cache Add-On (Llama-class, approximate)

Additional VRAM for context (FP16 KV):

| Model | 8K ctx | 32K ctx | 128K ctx |
|-------|--------|---------|----------|
| 8B | 0.5 GB | 2 GB | 8 GB |
| 70B | 5 GB | 20 GB | 40 GB |

---

## 4. GPU Configuration Recommendations

### Tier A — Dev / POC

| Model Class | Config | Est. Cloud $/hr |
|-------------|--------|-----------------|
| 8B INT4 | 1× T4 16GB or RTX 4090 | $0.35–0.80 |
| 70B INT4 | 1× A100 40GB | $1.50 |

### Tier B — Production (moderate throughput)

| Model Class | Config | Est. Cloud $/hr |
|-------------|--------|-----------------|
| 8B FP16 | 1× A10G | $1.00 |
| 70B INT4 | 1× A100 80GB or H100 | $2.50–3.50 |
| 70B INT8 | 1× A100 80GB | $2.50 |

### Tier C — Production (high throughput)

| Model Class | Config | Est. Cloud $/hr |
|-------------|--------|-----------------|
| 70B FP16 | 2× A100 80GB (tensor parallel) | $5.00 |
| 70B INT4 | 2× A100 40GB | $3.00 |

---

## 5. Replica Sizing

```
peak_rps = daily_interactions × peak_factor / 86400
peak_factor default = 10 (10× average during peak hour)

replicas = ceil(peak_rps × avg_latency_sec / batch_efficiency)
batch_efficiency:
  vLLM/TGI = 0.6–0.8
  Ollama single-user = 0.3
```

**Example:** 10,000 flows/day, 4 LLM calls each, peak_factor=10, latency=3s, efficiency=0.7

```
peak_rps = 10000 × 10 / 86400 ≈ 1.16 rps × 4 calls = 4.6 inf/sec
replicas = ceil(4.6 × 3 / 0.7) = ceil(19.7) → 20 replicas (or scale horizontally)
```

At this scale, **API hosting or managed inference** may be more economical — compare in model-selection.

---

## 6. Inference Runtime Selection

| Runtime | Best For | Notes |
|---------|----------|-------|
| **vLLM** | Production throughput, multi-GPU | PagedAttention, OpenAI-compatible API |
| **TGI** | HuggingFace ecosystem, enterprise | Production-ready, quantization support |
| **Ollama** | Local dev, POC | Simplest setup; not for high throughput |
| **llama.cpp** | Edge, CPU+GPU split | GGUF quantization |
| **NVIDIA NIM** | Enterprise GPU deployments | Pre-optimized containers |

---

## 7. On-Prem Hardware Alternatives

| Hardware | Unified/VRAM | Suitable Models |
|----------|--------------|-----------------|
| Mac Studio M4 Max 128GB | 128 GB | 70B INT4 comfortably |
| Mac Studio M2 Ultra 192GB | 192 GB | 70B FP16 (tight) |
| 2× RTX 4090 24GB | 48 GB total | 70B INT4 with tensor parallel |
| 1× RTX 6000 Ada 48GB | 48 GB | 70B INT4 |

---

## 8. Monthly Cost Estimate (Self-Hosted Cloud)

```
monthly_usd = gpu_hourly × 24 × 30 × replicas × utilization

utilization defaults:
  dev: 0.3
  production: 0.5–0.7
```

**Example:** 1× A100 40GB @ $1.50/hr, 2 replicas, 50% util

```
monthly = 1.50 × 24 × 30 × 2 × 0.5 = $1,080/month
```

Compare against API cost estimate for same workload volume.
