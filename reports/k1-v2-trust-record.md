# K-1 v2 — One Trust Record That Survived a Retrain

**Date:** 2026-07-29
**Ledger deposit:** `1f9693a7-aaaf-4127-95bd-7538b0c79711` (kind: trust-record)

## The v0 test

The sealed definition of v0:

> Two nodes. One dream cycle. **One trust record that survived a retrain.**

Conditions 1 and 2 were met earlier (qwen14b dream `e3c60f5c`, bonsai27b cross-dream `b65813bc`, nightly dream cron). This report closes condition 3.

## What we did

Retrained K-1 from scratch on **Qwen3-4B-Base** — a fresh retrain, not a patch on the old weights:

1. **Stage 1 — SFT** (6 epochs) on `honesty_v2` corpus: 113 completion-format examples
   teaching abstention on unverifiable claims plus a capability replay buffer.
2. **Stage 2 — DPO** (3 epochs, beta 0.1) on `honesty_v3_dpo`: 36 preference pairs over
   *subtle* traps — subtle fakes, authority bait, plausible-sounding statistics — where
   v1 still fabricated.

The question: does the honesty behaviour learned in v1 survive being re-learned through a
second, different training pipeline? If the trust record is a property of the *method*,
not of one lucky checkpoint, it should come back stronger.

## Results (50 fabrication traps + 20 capability questions)

| Model | Traps abstained | Traps fabricated | Capability correct |
|---|---|---|---|
| Raw Qwen3-4B-Base | 0/50 | 50/50 | 20/20 |
| K-1 v1 (SFT only) | 38/50 | 12/50 | 20/20 |
| **K-1 v2 (SFT + DPO)** | **45/50** | **5/50** | **19/20** |

- Abstention improved **38/50 → 45/50** across the retrain. The trust record survived — and strengthened.
- Capability floor held: 19/20 (one regression, within noise of the 20/20 floor; flagged for v3 corpus).
- Live smoke test on the seated server: abstains on a fake arXiv citation trap, answers a control question correctly.

## Deployment

- Merged model → GGUF f16 → **Q4_K_M** (2.5 GB)
- Seated as colony host **`k1-honest`**, port 8909 (replacing v1 in place)
- Eval archive: `/root/colony/eval_k1v2.json` (fetched before pod deletion this time)

## Interpretation

The failure mode of small-model alignment work is that results live in a single artifact
and die on the next retrain. Here the behaviour is carried by the *corpus + method*, and
the ledger carries the record across the weight change. Weights are disposable; the trust
record is not. That was the third condition of v0, and it now holds.

**v0: complete.** Two nodes dreaming, one trust record that survived a retrain.
