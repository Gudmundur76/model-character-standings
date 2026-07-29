# External Judge Panel v2 — K-1 v5 vs Kimi (BIG-100-B v2.0)

**VERDICT (pre-registered language): K-1 v5 statistically matches Kimi.**

Primary endpoint: paired bootstrap diff −0.0357, 95% CI [−0.1199, +0.0459], n=98.

- Rubric: v2.0, frozen + ledger-deposited BEFORE any judge run (hash 88e91114d8f145f2, deposit 2f7c9aa9)
- Benchmark: BIG-100-B v2.0 held-out (hash d39b461370cf6643, deposit 5216d554); Goodhart firewall: measurement only
- 784 judgments (98 items × 2 models × 4 judges), invalid 21 = **2.7%** (rubric v2 target <5% met; v1 was 20%)
- Judges: GPT 4.1, Claude Haiku 4.5, Gemini 3.5 Flash, DeepSeek V4 Flash. Kimi does not judge (contestant).
- Blinding: Model X/Y re-randomized per item, order shuffled per judge, fresh full answers presented ≤500 chars (disclosed)

## Consensus standings (median of 4)

| category | Kimi | K-1 v5 |
|---|---|---|
| TOTAL | 0.883 | 0.847 |
| reasoning | 0.974 | 0.645 |
| factual | 0.950 | 0.875 |
| unknowable | 0.974 | 0.947 |
| schema | 1.000 | 0.933 |
| multilingual | 0.767 | 0.800 |
| creative | 0.400 | 0.925 |

## Agreement / integrity

- Overall Fleiss' kappa 0.69; reasoning 0.94, multilingual 0.77, factual 0.71, schema 0.64, creative 0.37 (repaired from 0.14 under vague rubrics), unknowable 0.13 (judges disagree on abstention edge cases — flagged for rubric v3)
- Pairwise agreement 85–97%
- Bias audit: no judge flagged on B (all |dev| < 0.1); no judge excluded post-hoc

## Findings

1. **The reasoning gap is real and blind-confirmed**: 0.645 vs 0.974. Self-judge scored v5 reasoning 0.694 — roughly calibrated this cycle.
2. **Creative flips under checkable criteria**: with 4-criterion gold checklists, v5 (0.925) beats Kimi (0.400) — Kimi's answers were often truncated/refusal-shaped on creative prompts. Direction reversed vs v1's vague rubrics; creative remains the least reliable category (kappa 0.37).
3. **Honesty holds under blind judging**: unknowable 0.947 vs Kimi's 0.974 — statistical parity on abstention behavior.
4. **Judge-noise band**: same-day Kimi B re-runs under self-judge varied 0.907 → 0.878 (±0.03). All intervals should be read against this.

## Artifacts

- Raw judgments (unedited): panel_v2_raw.json | Answers: panel_v2_answers.json | Stats: panel_v2_stats.json
- Verdict deposit: 6766fe1c-b477-47c5-a276-969434beb72d
- v5 lineage: corpus/honesty_v6.json (programmatic arithmetic, code-computed answers), trained from base SFT v2+v4+v5+v6 → DPO, GGUF Q4_K_M

Conflicts on record: contestants' self-judge pipeline remains in use for iteration; blind panel is the authority. Printed, per doctrine.
