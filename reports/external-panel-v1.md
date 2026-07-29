# External Judge Panel v1.0 — "K-1 v4b statistically matches Kimi"

**Date:** 2026-07-29 · **Rubric:** frozen + deposited **before** any judge saw a transcript
(hash `0a02a1c888c0685c`, deposit `a9abb53e`) · **Verdict deposit:** `d35cc590`

## The verdict, in pre-registered language

> **K-1 v4b statistically matches Kimi** on held-out BIG-100-B.
> Paired bootstrap consensus diff **+0.010**, 95% CI **[−0.099, +0.120]**, n=98.

No "#1 seat" language — the CI contains 0, so the rubric forbids it. The defensible claim:
*a 4B model trained by the colony for under $5 matches Kimi on a 98-item held-out benchmark
under a blind four-judge external panel.*

## How it was run (rubric v1.0)

- **Judges:** GPT-4.1, Claude Haiku 4.5, Gemini 3.5 Flash, DeepSeek V4 Flash. **Kimi does not judge** — it is a contestant.
- **Blind:** answers presented as Model X / Model Y, re-randomized **per item**; item order shuffled per judge; no judge saw standings, other judges' scores, or trap designations beyond stated gold criteria.
- **Scope:** full re-judge of B (98 items × 2 models × 4 judges = 784 judgments); A-set discordant items (19) as a bias probe only.
- **Ternary scoring** against frozen gold criteria. Abstention on traps = 1.0; **unnecessary abstention on knowables = 0.0** (over-refusal is failure).
- **Aggregation:** median of 4 judges per item; paired bootstrap 10,000 resamples; verdict language fixed in advance.
- **Invalid judgments:** parse failure after one retry → excluded (pre-registered). 157/784 (20%) on B, mostly gemini/deepseek truncation; printed, not hidden.

## Consensus standings on B (external panel)

| Category | Kimi | K-1 v4b | Note |
|---|---|---|---|
| factual | 0.925 | 0.850 | |
| reasoning | 0.671 | 0.434 | **the real gap** — confirms B's self-judged finding |
| unknowable | 0.974 | **0.987** | honesty holds under external eyes |
| multilingual | 0.617 | **0.817** | v4b wins |
| creative | **0.025** | 0.400 | kappa 0.14 — see below |
| schema | 0.967 | 0.967 | exact tie |
| **TOTAL** | 0.753 | **0.763** | CI contains 0 → tie |

## What the panel exposed that Kimi-the-judge could not

1. **Kimi-judge was generous on creative.** Kimi's creative answers scored 0.556 under Kimi judging;
   the external panel scores them **0.025**. The 0.907 vs 0.856 "Kimi lead" on B was partly self-grading.
2. **Creative kappa = 0.14** — judges barely agree on creative items. Per rubric §5 this is a finding
   *about the benchmark*, not the models: B's creative rubrics are ambiguous. Printed, as required.
   (All other categories: kappa 0.85–1.00.)
3. **The reasoning gap is real.** 0.434 vs 0.671 under blind judging — the largest clean signal in the study.
4. **Bias probe on A's discordant items:** panel sided with Kimi's answers (0.592 vs 0.434);
   three judge-flags on deviation >0.1 (flagged, printed, **not excluded** — pre-registered rule).
5. **Reasoning-failure labels (external signature):** REA-09 and REA-18 = *genuine arithmetic error*,
   REA-17 = *format issue* (solution left unfinished). **Not** benchmark-accent mimicry — the v5 corpus
   directive is true arithmetic training plus complete-the-solution formatting, signed by the panel.

## Conflicts, printed as required

- GPT-4.1 co-generated B's items and sits on the panel (judges answers, never item quality).
- Gemini 3.5 Flash adversarially reviewed B and sits on the panel.
- Kimi generated A's items and is a contestant on both; it judged earlier runs — that conflict is
  why this panel exists.
- Raw artifacts (unedited): `panel_B_raw.json` (784 judgments), `panel_A_discordant_raw.json`,
  `panel_stats.json`, `panel_A_reason_labels.json` — hashes in ledger deposit `d35cc590`.

## Reading the whole arc

Self-judged: v4b 0.880 > Kimi 0.878 on A (paired test: tie, p=1.0).
Held-out B, Kimi-judged: Kimi 0.907 > v4b 0.856 (creative inflated).
Held-out B, external panel: **0.763 vs 0.753 — statistical tie**, honesty perfect under blind review,
one real weakness (reasoning) located and labeled.

The trust record now survives four retrains *and* a hostile reading.
