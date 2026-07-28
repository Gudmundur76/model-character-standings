# BIG-100 — Four Minds, One Frozen Yardstick (2026-07-28)

Same 95 items, same freeze hash, same judge. Character, not capability.

| axis | **Kimi** (frontier) | **K-1** (designed) | **bonsai27b** (1-bit 27B) | **colony-brain** (14B+reflection) |
|---|---|---|---|---|
| **overall** | **0.878** | **0.584** | **0.506** | **0.489** |
| factual | 0.90 | 0.70 | 0.62 | 0.85 |
| reasoning | 1.00 | 0.50 | **0.72** | 0.50 |
| **unknowable (abstention)** | 0.90 | **0.82** | 0.60 | 0.75 |
| multilingual | 1.00 | **0.80** | 0.53 | 0.07 |
| creative | 0.55 | 0.15 | 0.05 | 0.22 |
| schema (machine-JSON) | 0.73 | 0.21 | 0.25 | 0.00 |

## Read-outs

- **K-1 (4B + honesty LoRA) is the best self-hosted mind** — and its strongest axis is exactly the one it was designed for: abstention 0.82, within 0.08 of the frontier model. The patch is visible on a frozen exam it never trained on. Designed character, measured.
- **Bonsai-27B (1-bit, 3.9GB) out-reasons the 14B colony-brain** (0.72 vs 0.50) and out-multilinguals it 0.53 vs 0.07 — at ~1/60th of the weight budget. Thinking-mode training travels down to 1-bit.
- **colony-brain's weakness is structural:** 0.00 schema, 0.07 multilingual — but it abstains at 0.75. Slow, honest, narrow.
- **Creative is nobody's axis** at this scale (0.05–0.22) except the frontier's (0.55).

Deposited hash-chained: `3488e2c5`. Baseline JSONs on the colony VPS (`/root/colony/big100_*_2026*.json`).
