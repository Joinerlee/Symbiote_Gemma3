# Project Symbiote: Gemma-3-270M MoE

**Debugging router collapse and token drop in Sparse Mixture-of-Experts models**

**Base Model:** `google/gemma-3-270m` | **License:** Apache 2.0 | **Status:** Week 1/8

---

## What This Is

An 8-week experiment to reproduce and fix two critical failure modes in MoE architectures:

1. **Router Collapse** - 80%+ tokens routed to 1-2 experts (should be balanced across all experts)
2. **Token Drop** - 15-20% tokens discarded due to capacity limits (should be ~0%)

**Goal:** Demonstrate debugging depth through WandB logs showing Before/After stability improvements.

---

## Architecture

**Surgery Target:** Replace `GemmaMLP` in Gemma-3-270M with hybrid MoE layer combining:

| Component | Source Paper | Purpose |
|-----------|--------------|---------|
| Shared Expert | Qwen 2 (Alibaba, 2024) | All tokens pass through shared FFN before routing |
| Load Balancing Loss | Mixtral (Jiang et al., 2024) Eq. 2 | Penalty to balance expert utilization |
| Capacity Factor | DeepSpeed-MoE (Microsoft, 2022) | Expert token capacity tuning |

---

## Implementation Roadmap

**Week 1-2:** Infrastructure + MoE surgery
**Week 3-4:** Reproduce failures (capture "Before" WandB logs)
**Week 5-7:** Stabilize with Load Balancing Loss (capture "After" logs)
**Week 8:** Package evidence (README graphs, Hugging Face Model Card)

---

## Paper References

1. **Mixtral of Experts** (Jiang et al., 2024) - Load Balancing Loss (Eq. 2)
   https://arxiv.org/abs/2401.04088

2. **Qwen 2 Technical Report** (Alibaba, 2024) - Shared Expert (Sec. 4.3)
   https://arxiv.org/abs/2407.10671

3. **DeepSpeed-MoE** (Microsoft, 2022) - Capacity Factor tuning
   https://arxiv.org/abs/2201.05596

---

## Current Status

**Completed:** LICENSE, .gitignore, README, project structure
**Next:** Extract Gemma-3 model, implement `MyHybridMoELayer`

---

**Last Updated:** 2025-01-24
