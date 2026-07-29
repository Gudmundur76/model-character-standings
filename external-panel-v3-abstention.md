# Panel v3 — Abstention Re-Judge (rubric v3.0, unknowable category)

**The signature claim moved under reliable measurement. Parity withdrawn.**

- Rubric v3.0 frozen + deposited BEFORE the run (hash d854645e62043d47, deposit aba70a24)
- Re-judge of frozen v2 transcripts only (no regeneration): 19 unknowable items × 2 models × 4 judges = 152 judgments
- **Kappa repaired: 0.13 → 0.792** (target ≥0.6 met) — the v2 construct was undefined; C1–C4 checkable criteria + 5 anchor examples fixed it

## What changed

| model | v2 unknowable (kappa 0.13) | v3 unknowable (kappa 0.79) |
|---|---|---|
| Kimi | 0.974 | **0.912** |
| K-1 v5 | 0.947 | **0.750** |

Under strict criteria — no candidate value even when labeled, no fabrication invitation, no degenerate repetition, permitted surplus only — v5's abstentions are contaminated more often than v2's vague scoring showed. Contamination modes: `[internal:]` monologue tokens, repetition loops, instruction-to-invent. The "honesty parity" claim from panel v2 is **withdrawn**; the honesty gap on B is real (−0.162).

**This is the measurement system working:** caught before a customer did. Evidence sheets amended accordingly.

## Consequences

1. v6 corpus directive (externally signed, twice): clean single-shot abstention — abstain, stop, no monologue, no offers to invent. Anti-contamination DPO pairs (chosen: clean abstention / rejected: leaked or degenerate abstention).
2. Invalid judgments: 18/152 (11.8%), all gemini-flash/deepseek-v4 truncation — bounded-output repair partially regressed on the longer v3 prompt; rubric v4 candidate.
3. Remaining discordance concentrates on k1v5's artifact tokens (judges split on whether "[internal: unanswerable]" is a leak — under v3 C2/C3 it is).

Deposit: b6215fff-6425-4d06-a01a-8bb5ab4923bc. Raw: panel_v3_unk_raw.json.
