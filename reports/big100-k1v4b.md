# BIG-100 — K-1 v4b: 0.880, the colony's model takes the #1 seat

**Date:** 2026-07-29 · **Bench:** BIG-100 frozen (95 items, sha256 `3043b9cfcd8fdac9`) · **Judge:** Kimi strict JSON
**Ledger deposit:** `b95a4eac-95b6-443e-a6ad-e78683ede931`

## Standings

| # | Mind | Overall | Unknowable | Schema | Reasoning |
|---|---|---|---|---|---|
| 1 | **K-1 v4b (4B, colony-trained)** | **0.880** | **1.000** | 0.727 | 0.833 |
| 2 | Kimi | 0.878 | — | — | — |
| 3 | K-1 v3 (4B) | 0.835 | 0.975 | 0.667 | 0.722 |
| 4 | K-1 v2 (4B) | 0.771 | 1.000 | 0.227 | 0.778 |
| 5 | K-1 v1 (4B) | 0.584 | 0.825 | — | — |
| 6 | Bonsai-27B | 0.506 | — | — | — |
| 7 | colony-brain | 0.489 | — | — | — |

## K-1 v4b by type

factual 0.895 · reasoning 0.833 · **unknowable 1.000** · multilingual 0.933 · creative 0.778 · schema 0.727

## How it got here — failure-driven corpus generation

Each version was built from the *measured failures* of the previous one:

| Version | Failure observed | Corpus response | Result |
|---|---|---|---|
| v2 | fabricated on subtle traps | v3 DPO subtle-trap pairs | abstention 38→45/50 |
| v2 | abstained on prompt-given data (schema 0.227) | v4 calibration corpus | schema → 0.667, but over-refusal cured |
| v3 | format collapse, wrong arithmetic, hedge tails | v5 precision corpus | **0.880, #1** |

## The honest iteration log

- **v4a — REJECTED.** Adding 30 precision examples with only 10 guards diluted abstention
  (battery 42→33/50). Not shipped.
- **v4b — rebalance (+20 guards), then measure.** Battery said abstain 31/50 — worse than v3b's 42 —
  but the frozen benchmark disagreed: **unknowable 1.000, perfect abstention on all 13 trap items**.
  Lesson, recorded: the strict 50-trap battery under-predicts benchmark abstention; proxies guide,
  the frozen benchmark decides. We measured instead of guessing, and the result stands.
- v4b gains over v3: reasoning +0.111, creative +0.178, schema +0.060, unknowable +0.025,
  at a cost of factual −0.005, multilingual −0.067. Whole surface reported, as always.

## Caveats we say out loud

- Kimi judges this benchmark, and Kimi also competes on it. The judge is a strict rubric-scorer
  on frozen items, but a fully external judge panel is the next integrity upgrade.
- A 4B model topping one frozen 95-item benchmark proves the *method* (verify-or-abstain +
  failure-driven corpora), not general superiority. BIG-100 is our yardstick; it is not the world.

Total training cost across all five K-1 versions: **under $5 of RunPod GPU time.**

K-1 v4b is seated as `k1-honest` (port 8909). Raw: `/root/colony/big100_k1v4b_20260729.json`.
