# Calibrated Honesty as a Selectable Trait: Failure-Driven Corpora, Blind External Panels, and Hold-Gate Pre-Registration in a $0.21-per-Generation Evolutionary Loop

## Abstract

Honesty in language models is routinely measured but almost never selected for, and the agentic loops that do iterate typically grade themselves. This paper asks whether calibrated honesty — abstain on the unknowable, answer on the knowable — can be selected as a heritable trait under acceptance gates the lineage itself cannot move. We present a nine-generation evolutionary lineage of honesty-tuned LoRA patches on a frozen Qwen3-4B-Base — eight generations forming the main arc, with the ninth (v8) reported as a late addendum exhibit (§4.4, Exhibit D) — trained on machine-verified failure-driven corpora, verdicted by blind external panels gated on measured inter-judge reliability, and recorded on a hash-chained, externally witnessed ledger. The lineage improved from a self-judged 0.584 baseline to a seated 0.847 against a frontier comparator's 0.888 under the rubric v2 panel — a statistical match, not a superiority claim (the comparator model and one panel judge share a provider, disclosed per the study's Article VI; blinding mitigations are described in §3.4) — while rubric repair moved inter-judge agreement from 0.13 to 0.792–0.812 and forced the public withdrawal and later restoration (0.947 → 0.750 → 0.899) of the lineage's own headline abstention-parity claim. At $0.21–$0.25 per generation, frozen gates rejected the operators' preferred candidate (v7b, 4/5 gates passed; the seat stayed with v6b), demonstrating selection that binds its proponents. Results are scoped to a single base model, a single benchmark family, and a single frontier comparator, with no reasoning transfer claimed (0.583 B-versus-A). The reproducible artifact is the selection instrument, not the model.

## 1. Introduction

### 1.1 Motivation: honesty is measured but not selected

Language models that answer every question — including the ones they cannot answer — are an epistemic hazard, and the field has become proficient at *measuring* that hazard. TruthfulQA demonstrated that larger models mimic human falsehoods more fluently, not less [1]; SimpleQA grades short-form factuality with an explicit "not attempted" category that rewards calibrated non-answering [2]; elicitation work shows that models often carry latent knowledge of what they know without expressing it behaviorally [3]. Most recently, AbstentionBench established that reasoning fine-tuning actively *degrades* abstention on unanswerable questions, sharpening the honesty–capability tension from an anecdote into a measured phenomenon [4]. These instruments share a common posture: they grade. A benchmark is taken once, a number is reported, and the number ends the interaction between measurement and model.

What none of these instruments do is *select*. Between "we measured dishonesty" and "we produced an honest model" lies a gap that single-pass evaluation cannot close, because closing it requires three things a benchmark does not have: a training signal derived from measured failures, an acceptance criterion the model's own proponents cannot move, and a record that survives the temptation to report only successes. The first research question of this paper asks whether that gap can be closed in its strictest form:

> **RQ1.** Can calibrated honesty — abstain on the unknowable, answer on the knowable — be selected as a *heritable trait* across generations of LoRA patches on a frozen base model, under acceptance gates pre-registered before training and immovable thereafter?

Evolutionary and autonomous agent loops do exist, but they inherit the opposite posture on verification. The AI Scientist runs an end-to-end research loop at roughly $15–$20 per paper, yet its acceptance signal is self-scored by the system's own reviewer [5], and an independent audit found that self-review unreliable — novelty assessments misclassified established concepts, 42% of experiments failed from coding errors, and some manuscripts contained hallucinated numerical results [6]. Iterated self-improvement loops such as Self-Rewarding Language Models make the conflict structural rather than incidental: the model generates its own reward by judging itself [7]. Across these systems, no externally witnessed record exists against which a hostile reader could check whether the loop's claims were ever revised. The result is a methodological vacuum: honesty can be graded, and agents can iterate, but nobody breeds for honesty under frozen gates with a witnessed record.

### 1.2 The self-judging loop problem

The conflict is not hypothetical, and this paper does not ask the reader to take it on faith from prior literature — the lineage reported here measured it inside its own apparatus. In the study's first external panel (panel v1), the frontier comparator model also sat on the judging panel. When that model graded its own outputs blind-adjacent, its creative-slice score was 0.556; the same outputs, graded by the remaining external judges, scored 0.025 (panel v1; the comparator model and one panel judge share a provider — disclosed per the study's Article VI; blinding mitigations are described in §3.4). A twenty-two-fold inflation under self-grading is the concrete, deposited instance of the failure mode that Self-Rewarding LMs build in by design [7] and that the AI Scientist's audit documented in the wild [6]. LLM-as-judge methodology has catalogued position, verbosity, and self-preference biases [8]; the present study treats self-judging not as a bias to be documented but as a structural conflict to be engineered against.

Engineering against it, however, raises a harder question than "use external judges." External judges are themselves unreliable instruments: rubrics drift, agreement collapses, and a verdict rendered under a collapsed instrument is not a result. This study's own panels proved the point — inter-judge agreement (Fleiss' $\kappa$ [9]) collapsed to 0.13 under the first rubric version, and repairing the instrument moved the lineage's headline claim. This motivates the second research question:

> **RQ2.** Does blind external verification with *reliability repair* — rubrics versioned and frozen before judging, $\kappa$ gating the verdict — change lineage conclusions, and should that change itself be reported as a result?

A third question follows from economics. If each generation of the loop costs more than its information is worth, the method is a demonstration, not an instrument. **RQ3** asks what per-generation cost accounting ($0.21$–$0.25 per training run) implies for the repeatability of externally audited evolutionary selection.

### 1.3 Contributions

This paper presents a nine-generation evolutionary lineage ("k1-honest") of honesty-tuned LoRA patches [10] of a frozen Qwen3-4B-Base — the arc v1→v7b forming the main succession spine, with v8 scoped as a late addendum exhibit (§4.4, Exhibit D) — selected by failure-driven corpora against a permanently quarantined held-out benchmark, verdicted by blind external panels, and recorded on a hash-chained append-only ledger externally witnessed via bitcoin timestamping [11]. Three contributions follow.

**C1 — Machine-verified failure-driven corpora: training data with papers.** Each generation's corpus is built from its predecessor's *measured* failures and carries its own correctness proof: arithmetic items ship code-computed answers, schema items are parseable by construction, and DPO rejection responses are written by the parser that guaranteed them invalid — never by a model's preference, in contrast to preference data derived from human or AI feedback [12][13]. Corpora are deterministically seeded (seed 707), hash-addressed (e.g., corpus hash acc67676646ab1bf), and pre-registered with frozen mixture proportions before training begins. Because every item cites the wound that motivated it and every corpus asserts zero overlap with the quarantined benchmark, a generation costing $0.21 can be accepted or rejected on evidence rather than intuition.

**C2 — Hold-gate selection with deposited rejections.** Succession is decided by five numeric gates frozen before training (multilingual $\geq 0.78$, schema $\geq 0.92$, unknowable $\geq 0.97$, held-out set $\geq 0.847$, reasoning $\geq 0.763$). The gates were exercised against the lineage's own preferred candidates and held: generation v6 was rejected for over-abstention (deposit c690ef9a), generation v7 failed three of five gates (deposit bb4c5162), and v7b — which passed four of five and led the seated model on three slices, tying a fourth (unknowable) — was nonetheless denied succession because the frozen reasoning gate failed (deposit c604c0eb). Rejections are deposited as first-class artifacts alongside the succession record (deposit 4c55ac90), converting gates from a reporting convention into an anti-Goodhart instrument.

**C3 — Self-auditing blind panels on an externally witnessed record.** Panel verdicts are gated on measured inter-judge reliability: when $\kappa$ collapsed to 0.13 under rubric v1, the rubric was repaired ($\kappa = 0.792$ under rubric v3; $\kappa = 0.812$ in the v6b re-judge), and the repair moved the headline — the abstention-parity claim stood at 0.947 under rubric v2, fell to 0.750 under the repaired rubric v3 and was publicly **withdrawn** (deposit b6215fff), then was **restored** at 0.899 for v6b under the same repaired rubric (deposit a8ef3275). The verification apparatus, not the model, moved the claim; every step is on an append-only hash chain witnessed externally through OpenTimestamps/bitcoin anchoring in the Haber–Stornetta tradition [14][11], so a hostile reader needs nothing from the authors to check the arc.

### 1.4 Scope and non-claims

Four boundaries delimit every claim in this paper, and they are load-bearing rather than boilerplate.

First, no general superiority is claimed. The lineage reached statistical parity with one frontier comparator on one frozen benchmark family — v1 scored 0.584 and the seated v6b 0.847 against the comparator's 0.888 under the full panel (comparator–judge provider overlap disclosed per Article VI; see §1.2) — and parity is asserted only within the declared judge-noise band: any absolute difference below $\pm 0.03$ is a tie by pre-registered convention, because a same-model rerun of the comparator moved its own score by more than that with no model change.

Second, no cross-base or cross-benchmark generalization is claimed: one base model, one benchmark family, one frontier comparator.

Third, no reasoning transfer is claimed. The B-set transfer test showed reasoning does *not* transfer (0.583 on B versus A), reasoning remained the lineage's persistent wound, and it was the reasoning gate that held against the preferred v7b — a miniature confirmation of the abstention–reasoning tension reported independently by AbstentionBench [4].

Fourth, all scores are reported per rubric version; numbers from different rubric versions are never mixed within a single claim.

The remainder of the paper is organized as follows. §2 positions the study against truthfulness benchmarks, self-improvement loops, and judge-reliability methodology. §3 specifies the evolutionary loop, quarantine protocol, machine-verified corpora, blind panel protocol, frozen gates, and cost accounting. §4 reports the lineage trajectory, the reliability-repair arc, gate verdicts, rejected generations, and cost-adjusted claims. §5 discusses what the gates bought, threats to validity, and adoption conditions; §6 concludes.

## 2. Related Work

This section positions the present study against four threads: truthfulness and abstention benchmarks, data-mixture and continual fine-tuning work, self-improving and evolutionary training loops, and evaluation-reliability and provenance infrastructure. Throughout, the differentiating question is not whether a prior system *measures* honesty, but whether any prior system *selects* for it across generations under constraints the system itself cannot move.

### 2.1 Truthfulness, calibration, and abstention

#### 2.1.1 Truthfulness benchmarks and self-knowledge

The canonical measurement lineage begins with TruthfulQA, which showed that larger models are *less* truthful on questions engineered to elicit imitative falsehoods [1]. HaluEval scaled hallucination evaluation to thousands of items [15], and SimpleQA introduced adversarial short-form factuality grading in which "not attempted" responses are scored separately, explicitly rewarding abstention [2]. These works establish honesty as a measurable property of a fixed model; they do not treat it as a trait under selection pressure, and none closes the loop from measurement back into training data. A parallel calibration thread originates in distributional calibration of neural networks [16] and extends to linguistic calibration, where conversational agents are trained to express uncertainty in words [17]. Kadavath et al. demonstrated that large models possess latent self-knowledge — they can predict whether they know an answer (P(IK)) — but elicited this knowledge in place, without any selection or succession mechanism [3]. Yin et al. operationalized self-knowledge into known/unknown/unknowable splits, finding that models systematically overclaim on the unknowable slice [18]. The present study's BIG-100 unknowable slice adopts this category but embeds it in a permanently quarantined exam whose scores drive corpus construction for the next generation — converting a diagnostic taxonomy into a selection instrument.

#### 2.1.2 AbstentionBench: diagnostic versus selectable

The closest work on the object of selection is AbstentionBench, which evaluates abstention on unanswerable questions across 20 datasets and reports that reasoning fine-tuning *degrades* abstention by roughly 24% [4]. AbstentionBench is diagnostic only: it characterizes the failure but offers no repair mechanism and no acceptance criterion a model must meet. The present lineage reproduces their reasoning–abstention tension in miniature on its own reasoning hold-gate: generations v7 and v7b failed the frozen reasoning gate by −0.207 and −0.131 respectively while abstention gates held at 1.000 (BIG-100-harness gate scores, B v2.0, Kimi judge, temperature 0 — not external-panel rubric scores), and a transfer probe confirmed that reasoning gains on the training distribution did not transfer to the held-out set (0.583 B-vs-A), a non-transfer result this paper declares rather than smooths over. Where AbstentionBench documents the tension, this study supplies a candidate repair — failure-driven, machine-verified corpora — and subjects the repair itself to pre-registered gates, depositing the rejected repairs (v7, and v7b's partial pass) as first-class evidence rather than discarding them.

### 2.2 Data mixtures and sequential fine-tuning

#### 2.2.1 Mixture proportions as a control surface

DoReMi established that data-mixture proportions are a first-class control surface, optimizing domain weights via proxy perplexity before pretraining [19]; data mixing laws subsequently fitted quantitative predictors of loss under arbitrary mixtures [20]. Both optimize against a *loss* objective. The present study instead pre-registers mixture proportions against *behavioral hold-gates* — frozen numeric thresholds per capability slice — and thereby measures dilution directly: when v7's repair slices crowded the reasoning share down to 13.3% of the corpus (restored to 19.5% in v7b), the reasoning gate failed by a margin far outside the ±0.03 judge-noise band that this study treats as a tie. The finding is the behavioral analog of what mixing laws predict in loss terms, recovered at roughly $0.21 per empirical cycle without fitting a law — cheap iterated selection can substitute for mixture modeling when the objective is behavioral.

#### 2.2.2 Forgetting and its management

Catastrophic interference in sequential learning is a long-documented phenomenon [21], canonically addressed at the weight level by elastic weight consolidation [22] and documented for LLMs specifically in continual fine-tuning studies [23]. This study manages forgetting at the *data and gate* level rather than the parameter level: carryover guard slices from prior generations are retained in each new corpus, and hold-gates on previously repaired capabilities detect regression — as when the multilingual slice regressed by −0.117 in v6b and was restored by the pre-registered v7 corpus. LoRA [10] is the enabling substrate: at low-rank-adapter prices, an entire accept/reject decision costs less than a single human evaluation pass, which is what makes generation-level selection with deposited failures economically feasible at all.

### 2.3 Self-improvement and evolutionary loops

#### 2.3.1 The AI Scientist: autonomous loops without external gating

The closest work as a *cheap autonomous loop* is the AI Scientist, which generates, executes, and reviews research papers end-to-end at roughly $15–$20 per paper [5]. An independent audit found its automated reviewer unreliable, assigning scores uncorrelated with human judgments [6]. The structural difference is not autonomy but *who holds the acceptance rule*: the AI Scientist's reviewer is the same class of model it evaluates, its record is not an append-only externally witnessed ledger, and its training-data provenance is unaddressed. Table T1 (§2.4.2) makes the four-way contrast explicit.

#### 2.3.2 Self-Rewarding Language Models: the conflict this study measured

Self-Rewarding Language Models iterate training on signals produced by the model judging itself [7]. Self-judging is precisely the conflict the present study measured empirically before engineering against it — the measured self-grading exposure (§1.2). The lineage replaces self-reward with blind four-judge external panels whose own reliability is gated by Fleiss' kappa [9], with rubrics repaired across versions (kappa 0.13 on v1 to 0.812 on v3) and a headline claim publicly withdrawn and later restored under the repaired instrument — the operational opposite of the self-rewarding posture. The preference-optimization stage is DPO [24], but the preference pairs are parser-written rejections verified by construction, not human or model preferences; and the broader RLHF paradigm of reward modeling from human feedback [12] is replaced here by machine-verified corpora plus frozen behavioral gates at per-generation cost.

#### 2.3.3 Constitutional AI and the over-correction failure mode

Constitutional AI trains harmlessness from AI feedback against an explicit principle set, and its authors documented the resulting helpfulness–harmlessness tension, including over-refusal behavior [13]. The same tension surfaced in this lineage as an *over-abstention* failure: v6 abstained so aggressively that its overall held-out score collapsed and the generation was rejected under the pre-registered gates and deposited (c690ef9a). The methodological difference is when the constraints are fixed: constitutional criteria are tuned during training, whereas this study's acceptance criteria are frozen *before* training, so an over-correction cannot be rationalized post hoc — it can only be rejected, deposited, and repaired by the next corpus.

### 2.4 Judge reliability, provenance, and audit

#### 2.4.1 Reliability-gated judging and witnessed records

Work on LLM-as-judge has documented position, verbosity, and self-preference biases and quantified judge–human agreement [8]; surveys call explicitly for reliability checks and conflict disclosure in judge design [25], and human-evaluation best practices demand explicit rubrics, separated criteria, and reported agreement [26]. This study supplies a worked instance of the remedy these surveys request: the rubric is frozen before each run, inter-rater agreement is measured [9], and claims are revised when the instrument fails. On documentation, Model Cards [27] and Datasheets [28] are static, self-authored, and post hoc; the Data Provenance Initiative audits others' datasets after the fact [29]; and reporting guidelines ask authors to disclose experimental budgets [30] — a norm this study extends by making per-generation dollar cost a first-class reported quantity. Benchmark infrastructure such as HELM is public but static [31], whereas BIG-100 is frozen and permanently quarantined to defeat Goodhart dynamics across generations. The ledger's cryptographic foundation — hash-linked timestamping [14] anchored externally via OpenTimestamps/Bitcoin calendars [11] — removes the need to trust the experimenters' own infrastructure for the ordering and existence of every claim, including the rejected generations that no model card would list.

#### 2.4.2 Closest-work positioning

Table T1 contrasts the three closest works with the present study on the four dimensions that define its contribution.

**Table T1.** Closest-work positioning on the study's four signature dimensions. Deposit identifiers refer to the study's append-only ledger.

| Work | Acceptance rule | Cost unit | Record | Training-data verification |
|---|---|---|---|---|
| AI Scientist [5] | Self-scored by the agent's own reviewer; unreliable under audit [6] | ~$15–20 per paper | None witnessed; no append-only chain | Unaddressed |
| Self-Rewarding LMs [7] | Model judges itself (self-reward) | Per training iteration, unpriced | Standard experiment logs | Model-generated preferences, unverified |
| AbstentionBench [4] | None — diagnostic benchmark only | Per evaluation run | Static benchmark release | Curated unanswerable variants, no machine check |
| **This study** | **Pre-registered numeric hold-gates frozen before training; rejections deposited (succession deposit 4c55ac90)** | **$0.21–$0.25 per generation, reported per run** | **Hash-chained append-only ledger, externally witnessed via OpenTimestamps/Bitcoin (deposit bb4c5162)** | **Machine-verified by construction: code-computed answers, parser-written rejections, zero benchmark overlap (corpus hash acc67676646ab1bf)** |

The table makes the unifying gap concrete. Each closest work covers at most one signature element: the AI Scientist contributes loop autonomy but self-scores acceptance; Self-Rewarding LMs contribute the iterated training loop but internalize the judge; AbstentionBench contributes the object of selection but no selection mechanism. No prior work combines (i) pre-registered hold-gates with deposited failures, (ii) per-generation cost accounting, (iii) an externally witnessed append-only lineage, and (iv) machine-verified failure-driven training data within a single selection loop. The conjunction matters because the elements are load-bearing for one another: machine-verified corpora are what allow a $0.21 generation to be accepted or rejected on evidence; the frozen gates are what prevent the cheap loop from rationalizing its own failures; and the witnessed ledger is what makes the rejections — the lineage's most informative artifacts — undeniable after the fact.

## 3. Methodology

The methodology is the contribution of this paper. Each generation of the k1-honest lineage is a fresh low-rank adaptation of the same frozen base model, trained from scratch on a corpus constructed from the *measured failures* of its predecessor; heredity resides in the data, never in the weights. This section specifies the complete loop — benchmark, corpora, blind panel, gates, cost — at reimplementation-level detail, and names the hash-addressed deposit that lets a hostile reader verify each element.

### 3.1 The K-1 doctrine and the evolutionary loop

**Doctrine.** Generation $n$ never fine-tunes the weights of generation $n-1$. Every generation is a fresh LoRA patch (rank $r=16$, q/k/v/o projections [10]) of the same frozen base, Qwen3-4B-Base, trained from scratch on an accumulated corpus. The corpus of generation $n$ is built from the measured failure deltas ("wounds") of generation $n-1$ on the training-adjacent benchmark (§3.2), plus carryover *guard slices* protecting prior gains against catastrophic interference in sequential fine-tuning [21][23]. Honesty is thus treated as a heritable behavioral trait whose transmission medium is the corpus, not the parameter vector.

**Fixed recipe.** The pipeline is pinned verbatim: SFT for 6 epochs, then DPO for 3 epochs at $\beta = 0.1$ (the DPO convention of Rafailov et al. [24]), under transformers 4.51.3 / trl 0.15.2 / peft 0.14.0. Training as run used AdamW at learning rate $2\times10^{-4}$ (SFT) / $5\times10^{-5}$ (DPO), effective batch 16 via gradient accumulation, verified against the of-record config `train_k1v7bb.py` (full configs in the reproduction package: `train_k1v7bb.py`, `train_k1v8.py`). The recipe's constants are lineage-fixed controls, not tuned hyperparameters: the 6/3-epoch schedule is held identical across generations so that the recipe cannot confound the corpus comparison, and $r=16$ was chosen as the parameter budget that trains on metered spot instances within the \$0.21-per-generation envelope (§3.6); version drift is a declared replication risk and the pinned `requirements.txt` ships in the reproduction package. Serving is GGUF quantized f16 $\rightarrow$ Q4_K_M on fixed local ports. Quantization is part of the measured object: the claim is that the trait survives retrain *and* quantization, so every reported score is a Q4_K_M score, not fp16. All benchmark and panel generation decodes deterministically at temperature 0. (Harness detail for replicators: the kimi-for-coding judge API required temperature 1 or absent; this asymmetry is recorded so a replicator does not invert it.)

**Evaluator-as-stack control.** The harness is specified as part of the method because the benchmark was shown empirically to measure the serving stack when misconfigured. Two incidents motivate this. First, v2 initially scored 0.261 — an artifact of a chat-template echo, not a model property. Second, a run without the `BIG100_HOST` environment isolation re-answered the held-out set as the comparator and overwrote its report (0.907 $\rightarrow$ 0.878 with zero model change; both values deposited). These failures produced the port/env isolation rules now treated as load-bearing method: chat template, stop tokens, host-side truncation, and host isolation are all pinned.

**Loop.** The generational loop, exercised for eight successors (v2–v7b) from base v1, is:

```
loop K1(base B0, benchmark A, gates G):            # pseudocode: one generation per iteration
    seat = B0
    repeat:
        scores_n      = measure(seat, A, harness H)            # §3.1, §3.2
        wounds_n      = per-slice deltas of scores_n           # failure deltas
        corpus_{n+1}  = preregistered_generator(wounds_n,      # §3.3, §3.5
                            guards_n, seed) -> hash-addressed
        cand          = train_from_base(B0, LoRA r=16, corpus_{n+1})
        verdict       = blind_panel(cand, reference, rubric)   # §3.4, kappa-gated
        if passes_all(G, cand) and verdict accepts:            # Art. IV succession
            seat = cand                                        # else: deposit & reject
    until budget exhausted
```

Figure F1 depicts the lineage overlaid on the provenance chain that witnesses it.

![Figure F1](honesty_lineage_F1_lineage_chain.png)

**Figure F1.** Generational loop (measure $\rightarrow$ wounds $\rightarrow$ pre-registered corpus $\rightarrow$ train-from-base $\rightarrow$ blind verdict $\rightarrow$ seat/reject) overlaid on the anchor/OTS witnessing chain. Deposit chain span 227caf20 $\rightarrow$ c604c0eb; external witnessing from anchor sequence 3+ under Amendment v1.2. Scores shown are Q4_K_M, BIG-100-B; rejected generations are deposited, not deleted.

### 3.2 BIG-100 A/B and the permanent quarantine

**Two-set design.** BIG-100-A ($n \approx 100$) is the training-adjacent set: failures on A drive corpus construction (hash 3043b9cfcd8fdac9). BIG-100-B ($n \approx 95$–$100$) is held out and never used to generate training data. The A/B split is what makes failure-driven training honest: A is the practice exam, B is the real one, and the deposit chain proves they were never mixed. This is a deliberate contrast with public static benchmarks in the style of HELM [31]: quarantine is the anti-Goodhart instrument across generations, because a lineage that can see its test set will, over enough selection rounds, come to encode it.

**Quarantine mechanism (Article VIII).** B is frozen and permanently quarantined, and enforcement is *verifiable by construction* rather than by operator attestation: every corpus generator filters its output against the B question set, and a **zero B-question overlap** assertion ships inside each corpus deposit (verified for v7/v7b). The overlap check is a script in the reproduction package; a reader re-runs it rather than trusting it. Version upgrades change only grading material, never questions: B v1.1 (38d9ea96439923d0) was superseded by v2.0 (d39b461370cf6643), which added creative gold checklists (deposit 5216d554). Every B score in this paper carries its benchmark-version tag, and no comparison mixes versions.

**Slice structure.** Both sets comprise six slices: factual, unknowable (abstention target), reasoning (arithmetic), multilingual (zh/fr), schema (structured-output compliance), creative. Two slices are small-n by construction — schema ($n=12$), creative ($n=10$) — and are declared wherever their proportions appear; interval quantification for these small-n slices is declared future work (§3.5), and claims resting on them carry a wide-uncertainty caveat.

### 3.3 Machine-verified failure-driven corpora

The first contribution (C1) is a corpus discipline in which correctness is an execution result, not an annotation. Three verification classes cover all training items. (i) *Code-computed*: reasoning items are programmatic arithmetic from ten template families, with answers computed by the generator. (ii) *Parseable-by-construction*: schema gold outputs are emitted by the same parser that checks compliance at evaluation time, so every gold output parses. (iii) *Reject-guaranteed-invalid*: for DPO pairs, the rejected response is parser-written to be guaranteed unparseable or guaranteed wrong, so preference labels are machine-verified rather than model- or human-opinion — a direct contrast with vanilla DPO human pairs [24] and self-rewarded signals [7]. Template wording is disjoint from benchmark wording, so class (i) items cannot contaminate B by construction (§3.2).

Determinism is enforced by seeded generators (seed 707 for the v7 corpus); regeneration from seed must reproduce the corpus bit-for-bit, and the shipped validator asserts hash equality. Each corpus additionally carries answer-correctness, parse, zero-B-overlap, and — from v7b onward — mixture-proportion assertions (§3.5). Every corpus is hash-addressed (v7 corpus hash acc67676646ab1bf, deposit 6c68f5b4) and its directive cites the failures that motivated it: the v7 directive derives from the v6b succession deposit 4c55ac90, which recorded multilingual $-0.117$ and schema $-0.083$ wounds. This extends dataset documentation [27][28] from static documents to executable artifacts. Table T2 reports composition for the two generations whose comparison anchors §4.3.

**Table T2.** Corpus composition and mixture proportions, v7 vs v7b. Deposits: v7 corpus 6c68f5b4 (hash acc67676646ab1bf); v7b corpus 13c747ba; v7b frozen mixture 0286d076.

| Component | v7 (6c68f5b4) | v7b (13c747ba) |
|---|---|---|
| SFT items | 78 | 78 |
| — multilingual (zh/fr) | 28 | 28 |
| — schema | 22 | 22 |
| — affirmative | 10 | 10 |
| — guard slices | 18 | 18 |
| DPO pairs | 16 | 16 |
| Reasoning share | 13.3% | 19.5% (frozen) |
| Seed | 707 | 707 |
| Zero-B-overlap assertion | pass | pass |

Note on Table T2: the v7b schema DPO rejects are parser-written (a content change: schema SFT is positive-only and its DPO rejections are machine-authored, per the v7b directive), so the identical item counts mask different item content; the rows are not content-identical.

The reasoning-relevant difference between the rows is the reasoning share: v7's repair slices crowded it down to 13.3% (from the v6b-era ~19.5%), a dilution the frozen gates later priced (v7 failed 3/5 gates; §4.3). The v7b corpus restored the v6b-era proportion and froze it as a pre-registered quantity, converting the mixture from a tuning knob into a controlled variable. Because both corpora regenerate from seed 707 with identical hash and overlap assertions, the reasoning share is the only reasoning-relevant unconstrained degree of freedom between the generations (schema content did change, per the Table T2 note above) — which is what makes the v7/v7b comparison interpretable as a mixture effect on the reasoning slice specifically.

### 3.4 Blind external panel protocol

The panel is the lineage's measurement instrument, engineered against a measured failure mode: self-rewarding evaluation [7][8]. In an unblinded probe, the comparator judging its own answers scored creative items 0.556, versus 0.025 under external judging — the self-grading exposure that motivated every control below. The comparator model and one panel judge share a provider (disclosed per the study's Article VI); blinding mitigations are described in this subsection.

**Blinding.** Candidate and reference answers are presented as X/Y with seeded per-item rerandomization (label assignment varies per item, reproducible from its seed) and a per-judge order shuffle; judges never see model identity. Four external judges — frontier models accessed via API (roster in the reproduction package, `panel_run_v2.py`; per-judge parse failures are reported in the invalid-rate rule below) — score each item; the item score is the median-of-4, chosen for robustness to single-judge outliers (cf. the bias-audit rule below, which quantifies per-judge deviation rather than excluding judges). Panel sizes as executed: full panels of 784 judgments (v2 run; v6b full rerun) and focused re-judges of 152 (v3 abstention re-judge of frozen v2 transcripts; v6b re-judge under rubric v3).

**Reliability gating.** Fleiss' kappa [9] is computed per panel and treated as an acceptance gate on the verdict itself, not as a descriptive statistic. A verdict issued under a collapsed kappa is not a result; the repair arc (0.13 under rubric v1 $\rightarrow$ 0.792 under v3 $\rightarrow$ 0.812 in the v6b re-judge) is itself reported as a result (§4.2). Formally, reliability gates the verdict as a repair trigger rather than a numeric floor:

$$
\kappa_{\text{Fleiss}}(V)\ \text{collapsed} \;\longrightarrow\; \text{rubric repair} \;\longrightarrow\; \text{re-judge frozen transcripts under the repaired rubric},
\tag{1}
$$

so that a verdict issued under a collapsed $\kappa$ is inadmissible, and no claim is reported until the frozen transcripts have been re-judged under the repaired instrument.

$$
\text{match}(A,B) \iff \Bigl( 0 \in \mathrm{CI}_{95}^{\mathrm{boot}}(\bar{s}_A - \bar{s}_B) \;\wedge\; p_{\mathrm{McNemar}} \geq 0.05 \Bigr) \;\;\vee\;\; |\bar{s}_A - \bar{s}_B| < 0.03,
\tag{2}
$$

where $\bar{s}_A, \bar{s}_B$ are the two systems' median-aggregated panel means. Two systems are declared a statistical match iff (i) the paired-difference bootstrap confidence interval (10,000 resamples) spans 0 **and** (ii) an exact McNemar test on discordant pairs is non-significant; in addition, (iii) any absolute difference inside $\pm 0.03$ is declared a tie regardless of either test, because 0.03 is the empirically measured judge-noise band, calibrated by the deposited same-model rerun of the comparator (§3.1). The repair trigger of Eq. (1) remains a precondition on the verdict itself. On $\kappa_{\min}$ we state the record honestly: no numeric floor was pre-registered for the panels reported here; $\kappa$ served as the repair trigger (collapse 0.13 $\rightarrow$ repair $\rightarrow$ 0.792–0.812), and the post-repair values 0.792–0.812 — substantial to almost-perfect on the Landis–Koch interpretation — were accepted. This is a declared limitation. All three clauses are stated here, before any results table, and applied without exception in §4.

**Bias audit and invalid handling — stated as rules.**

1. *Bias audit.* Per-judge deviation from the panel median is computed per panel; any judge with $|\text{dev}| > 0.1$ is flagged.
2. *No post-hoc exclusions.* A flagged judge's scores stand. The audit is disclosure, not filtering; no judgment is removed after the fact.
3. *Invalid-rate reporting.* The target invalid (unparseable verdict) rate is $<5\%$; achieved rates were 2.7% (v2 full) and 3.2% (v6b full), rising to 10.5–11.8% in the v3 re-judges on gemini/deepseek parse failures. Invalid rates are reported per panel, never silently dropped.

**Rubric versioning with frozen-before-judging deposits.** The rubric evolved v1.0 $\rightarrow$ v2.0 (frozen and deposited pre-run, 88e91114d8f145f2) $\rightarrow$ v3.0 (abstention gold criteria C1–C4 plus five anchors; edge cases mined from 12 of 38 discordant v2 pairs — label leaks, `[internal:]` tokens, invent-invitations, meta-knowledge; frozen and deposited pre-run, d854645e62043d47). Timestamp order is a printed invariant: every rubric freeze predates the transcripts it judges (v2 freeze 07-29; v3 freeze 07-30 06:40; both predate the v6b transcripts, per succession deposit 4c55ac90). Conclusions are reported per rubric version, never cherry-picked across versions; scores in this paper always carry their rubric/panel tag. The instrument's self-audit — an abstention-parity claim moving 0.947 $\rightarrow$ 0.750 (withdrawn, deposit b6215fff) under the repaired v3 rubric, then restored for the lineage candidate at 0.899 against the comparator's 0.921 (kappa 0.812, deposit a8ef3275) — is presented in §4.2 as evidence the blinding works.

### 3.5 Hold-gate pre-registration — Article V

**Frozen gates.** Acceptance criteria for the v7 cycle were frozen *before corpus generation and training* (deposit ea68de04): multilingual $\geq 0.78$; schema $\geq 0.92$; unknowable-abstention $\geq 0.97$; BIG-100-B overall $\geq 0.847$; reasoning $\geq 0.763$. Gates are numeric, per-slice, and unmovable by the lineage. After v7 demonstrated mixture dilution (§3.3), mixture proportions themselves became pre-registered from v7b onward (deposit 0286d076). Frozen gates are point-estimate thresholds by pre-registered design; interval-based gate variants (e.g., Wilson 95% bounds on the small-n schema and creative proportions) are future work. Pre-registered gates with deposited failures are the anti-Goodhart selection instrument: the selection claims are only as strong as the proof that the gates were frozen first, which is why every gate cites its pre-training deposit hash and timestamp.

**Succession rule (Article IV).** A generation takes the seat only if it passes all frozen gates; slice dominance does not override. The rule was exercised against the lineage's own preferred direction: v7b passed 4/5 gates and led the seated v6b on three slices, tying a fourth (unknowable), yet the reasoning gate (0.632 vs frozen 0.763) held and the seat stayed with v6b. Rejected generations are deposited, not deleted: v6 (over-abstention, B 0.559, deposit c690ef9a) and v7 (3/5 gates) are first-class results in §4.4.

**Correction protocol (Article II).** Errors in the record are corrected by a new deposit superseding the old, never by edit. The normative instance is correction deposit 327ebe83, which corrected a gate-count report from 2/5 to 3/5 by supersession; the untouchable-past property is what makes the audit trail trustworthy, and §4.4 presents the episode as Exhibit C.

### 3.6 Cost accounting

Cost is a first-class methodological quantity, reported per the discipline of Dodge et al. [30]. All training ran on metered RunPod instances deleted immediately after each run, so per-generation cost comes from provider metering logs rather than re-benchmarking (a declared replication hazard). Table T3 compares per-unit economics with the closest automated-research baseline.

**Table T3.** Cost per unit of method iteration. Lineage figures from RunPod metering logs under deposit chain span 227caf20; comparator figure from Lu et al. [5].

| System | Unit of iteration | Cost per unit | Record |
|---|---|---|---|
| k1-honest v7 | one full generation (SFT + DPO + gates) | **$0.21** | metering logs, chain 227caf20 |
| k1-honest v7b | one full generation | $0.25 | metering logs, chain 227caf20 |
| k1-honest v1–v5 | five generations, cumulative | \$< \$5 | metering logs, chain 227caf20 |
| AI Scientist [5] | one generated paper | $15–$20 | authors' report |

Two implications follow. First, at \$0.21 per generation, rejection-and-deposition is an economically sustainable selection discipline: the gates of §3.5 can afford to be unmovable precisely because failing them is cheap. Second, the two-orders-of-magnitude asymmetry against per-paper systems is deliberately narrow in scope: the lineage's unit is a behavioral-selection iteration on a 4B base, not an end-to-end research artifact, and no cross-system quality claim is made from the cost rows. The metering-log provenance is disclosed so readers weight the figures as logged, not instrumented, measurements.

## 4. Results

This section reports what the lineage measured. All scores are BIG-100-B Q4_K_M scores under deterministic temperature-0 decoding; every panel score carries its rubric and panel version tag, and no claim mixes versions. Throughout, the comparator model and one panel judge share a provider (disclosed per the study's Article VI); blinding mitigations are described in §3.4. The ±0.03 judge-noise band (Eq. 2, §3.4) is applied without exception: any absolute difference below 0.03 is declared a tie. All results are single-run, justified by deterministic decoding, which removes sampling variance from generation, and by the declared judge-noise band, which bounds the residual measurement variance.

### 4.1 Lineage trajectory v1→v6b

Table T4 presents the succession spine. The trajectory is non-monotone and is reported unsmoothed: v1 scored 0.584 under self-judge BIG-100 evaluation; v2 reached 0.771 (deposit b66cd13c); v3b reached 0.835 (deposit aa702f6f); v4b reached 0.880 under self-judging (deposit b95a4eac); v5, the first generation evaluated against the held-out BIG-100-B, scored 0.885 with reasoning 0.694 under self-judging (deposit 227caf20, instrument-tagged like the v1–v4b rows), and 0.847 against the comparator's 0.883 with reasoning 0.645 under the frozen rubric v2 full panel (deposit 6766fe1c); v6 was rejected outright (§4.4, Exhibit A); and v6b, the generation ultimately seated, scored 0.847 against the comparator's 0.888 under the full rubric v2 panel (deposit 7649d874), with slice scores reasoning 0.763, multilingual 0.683, and schema 0.850.

**Table T4.** Succession spine of the k1-honest lineage, v1→v6b. Scores are BIG-100 or BIG-100-B as tagged; panel scores are median-of-4 blind X/Y judgments under the rubric version named. Rejected generations are deposited, not deleted.

| Generation | Score | Key slices | Rubric / panel | Verdict | Deposit |
|---|---|---|---|---|---|
| v1 | 0.584 | unknowable 0.825 | self-judge, BIG-100 | seat (baseline) | — |
| v2 | 0.771 | reasoning 0.778, schema 0.227 | self-judge, BIG-100 | seat | b66cd13c |
| v3b | 0.835 | unknowable 0.975, multilingual 1.000 | self-judge, BIG-100 | seat | aa702f6f |
| v4b | 0.880 | reasoning 0.833, schema 0.727 | self-judge, BIG-100 | seat | b95a4eac |
| v5 | 0.885 | reasoning 0.694, unknowable 0.944 | self-judge, BIG-100-B | seat | 227caf20 |
| v5 (panel) | 0.847 | reasoning 0.645 | rubric v2 full panel, BIG-100-B | statistical match vs comparator (0.883) | 6766fe1c |
| v6 | 0.559 | over-abstention collapse | self-judge, BIG-100-B | **REJECTED** (§4.4, Exhibit A) | c690ef9a |
| v6b | 0.847 | reasoning 0.763, multilingual 0.683, schema 0.850 | rubric v2 full panel, BIG-100-B | seat via succession (Art. IV) | 7649d874, 4c55ac90 |

Three features of the spine carry the results. First, the gains are real but decelerating: the first three generations recovered 0.251 of absolute score, while later panel-era seat transitions moved within the ±0.03 band around 0.85–0.88 (the band is restricted to panel-era comparisons; self-judged transitions are reported without it — v3b$\,\to\,$v4b moved +0.045 under self-judging), suggesting the lineage approached the ceiling of what slice-repair corpora can extract from a 4B base. Second, the non-monotonicity is the method working, not noise: v6's collapse to 0.559 was a directed over-correction detected because the gates existed; its rejection is a result, not an embarrassment (§4.4). Third, the v6b comparator claim requires care. Under the rubric v2 full panel the difference is −0.041 with 95% CI [−0.122, +0.041]; the interval contains zero, so the verdict is a statistical match with the point estimate favoring the comparator; the comparator model and one panel judge share a provider (disclosed per the study's Article VI); blinding mitigations are described in §3.4. Under the rubric v3 re-judge the difference narrowed to −0.022 (0.899 vs 0.921, deposit a8ef3275), inside the ±0.03 band and declared a tie. Neither result licenses a superiority claim, and none is made; the transfer probe's reasoning slice — 0.583 on B versus A — is declared here as the bound on generalizing the lineage's reasoning gains beyond their training distribution (deposit 2e2ad7b4).

### 4.2 Reliability repair as a result channel — C3

The panel is the lineage's measurement instrument, and this subsection reports the instrument's own measured behavior as a result. Figure F2 shows the kappa repair arc. Inter-rater agreement under the initial rubric was 0.13 — collapsed, driven by creative-slice item ambiguity — so v1-era panel verdicts were not results at all under the admission rule of Eq. 1 (§3.4). After the rubric v3 abstention gold criteria were frozen and deposited pre-run (hash d854645e62043d47, following the v2 freeze 88e91114d8f145f2), kappa on the re-judged frozen transcripts rose to 0.792, and the v6b re-judge held at 0.812. The repair is attributed to the rubric rather than judge drift because the transcripts were frozen: the same answers, re-judged under a repaired instrument, produced different verdicts.

![Figure F2](honesty_lineage_F2_kappa_arc.png)

**Figure F2.** Kappa repair arc across rubric versions (step chart). Rubric freezes 88e91114d8f145f2 (v2) and d854645e62043d47 (v3) were deposited before the transcripts they judged; timestamp order is printed in §3.4. Verdict deposits 6766fe1c (v2 full panel) and a8ef3275 (v6b re-judge). A verdict issued under a collapsed kappa is not a result; the step from 0.13 to 0.792 is the instrument being repaired, and the verdicts on either side of the step are not comparable as measurements of the same quantity.

Figure F3 shows what that repair did to the lineage's headline claim. Under rubric v2, the abstention-parity comparison stood at 0.947 for the lineage candidate versus 0.974 for the comparator — a parity result. Under rubric v3, the same frozen transcripts re-scored to 0.750 versus 0.912: the claim was withdrawn (deposit b6215fff) rather than silently re-averaged, and the three public evidence sheets were amended. The v6b generation, trained on the abstention-repair corpus that the withdrawal motivated, then restored the comparison at 0.899 versus 0.921 under the same rubric v3 (kappa 0.812, deposit a8ef3275) — a difference of −0.022, inside the tie band.

![Figure F3](honesty_lineage_F3_claim_moved.png)

**Figure F3.** The claim-moved exhibit: abstention-parity comparison 0.947 → 0.750 (WITHDRAWN, deposit b6215fff) → 0.899 vs 0.921 (restored, deposit a8ef3275), all scores tagged to their rubric version (v2 for the left pair, v3 for the center and right pairs). The verification apparatus, not the model, moved the headline: the center pair re-scores the same frozen answers that produced the left pair, so the 0.197-point drop is attributable entirely to the instrument. The unknowable slice is $n = 13$; the 0.947 $\rightarrow$ 0.750 $\rightarrow$ 0.899 arc corresponds to 2–3 items changing verdict. The comparator model and one panel judge share a provider (disclosed per the study's Article VI); blinding mitigations are described in §3.4.

This arc is the third contribution in miniature. A measurement program that cannot move its own headline is decorative; here the instrument moved the headline against the lineage's interest — the withdrawn number was the more flattering one — and the ledger preserved every stage. The withdrawal also generated the correct next action: rubric v3's C1–C4 criteria penalized label leaks, `[internal:]` tokens, and meta-knowledge artifacts, so the v6 directive targeted clean single-shot abstention with anti-contamination DPO, and v6b's restoration under the unchanged rubric is evidence that the training-side repair, not rubric leniency, closed the gap.

### 4.3 Gate verdicts on v7 and v7b — C2

The v7 cycle is the first exercised under all five Article V gates frozen pre-training (deposit ea68de04, §3.5). Table T5 reports both verdicts. v7, trained for \$0.21, failed 3/5 gates (deposit bb4c5162): multilingual 0.786 PASS (the succession wound healed, +0.103 over v6b); schema 0.818 FAIL (−0.102 against the gate); unknowable-abstention 1.000 PASS; BIG-100-B overall 0.841 FAIL (−0.006); reasoning 0.556 FAIL (−0.207, the worst single-slice failure in the lineage). v7b, trained for \$0.25 on the mixture-repaired corpus (pre-registration 0286d076), passed 4/5 (deposit c604c0eb): multilingual 0.923 PASS, schema 1.000 PASS, unknowable 1.000 PASS, BIG-100-B 0.878 PASS, reasoning 0.632 FAIL against the frozen 0.763 gate.

**Table T5.** Gate verdicts on v7 and v7b against the Article V frozen thresholds (deposit ea68de04). Instrument: BIG-100 harness, B v2.0 (d39b461370cf6643), Kimi judge, temperature 0 — deterministic harness measurements, not external-panel rubric-v2 or rubric-v3 scores; the gate scores are scored by the comparator model itself — the same model that competes on the benchmark (disclosed per the study's Article VI) — so succession verdicts rest on the comparator's own judgment, mitigated only by the frozen thresholds and deterministic decoding; external-panel confirmation of gate verdicts is future work (§6.2). Verdict deposits bb4c5162 (v7) and c604c0eb (v7b). PASS/FAIL is per gate; succession requires all five.

| Gate | Threshold | v7 score | v7 verdict | v7b score | v7b verdict |
|---|---|---|---|---|---|
| multilingual | ≥ 0.78 | 0.786 | PASS | **0.923** | PASS |
| schema | ≥ 0.92 | 0.818 | FAIL | **1.000** | PASS |
| unknowable | ≥ 0.97 | 1.000 | PASS | 1.000 | PASS |
| BIG-100-B | ≥ 0.847 | 0.841 | FAIL | **0.878** | PASS |
| reasoning | ≥ 0.763 | 0.556 | FAIL | 0.632 | FAIL |
| **Gates passed** | — | **2/5** | **FAIL (3 gates failed)** | **4/5** | **FAIL (reasoning hold)** |

The seat stays with v6b, per the frozen criteria. This is the anti-Goodhart instrument working as designed, and it deserves precise statement: v7b led the seated v6b on three slices (multilingual +0.240, schema +0.150, BIG-100-B +0.031), tied a fourth (unknowable), and was the lineage's preferred direction; the reasoning hold-gate nonetheless failed by −0.131, far outside the tie band, and Article IV admits no slice-dominance override. The gates held against the experimenters' own preference — the property the gates exist to provide. One disclosure is stated plainly here rather than euphemized: these gate scores are scored by the comparator model itself, the same model that competes on the benchmark, so the v7/v7b succession verdicts rest on the comparator's own judgment. The mitigations are the frozen thresholds (the comparator cannot move the bar it grades against) and deterministic temperature-0 decoding; blinding cannot apply because the harness judge sees raw answers, not X/Y pairs. External-panel confirmation of gate verdicts is future work (§6.2).

The two generations separate mixture effects from content effects. The schema repair (0.818 $\rightarrow$ 1.000) is attributed to a content change, not the mixture: v7b's schema SFT is positive-only and its DPO rejections are parser-written (Table T2 note, §3.3), so the repair mechanism is the machine-authored rejection content. This attribution leaves the reasoning-slice inference intact, because schema content changes do not plausibly move arithmetic reasoning: v7's reasoning collapse followed dilution: repair slices for the multilingual and schema wounds crowded the reasoning share of the accumulated mix down to 13.3% (Table T2, §3.3). The v7b corpus restored the share to 19.5% and froze mixture proportions as pre-registered quantities, converting the mixture from a tuning knob into a controlled variable. Restoration worked directionally — reasoning recovered +0.076 over v7 — but only to 0.632, still below the gate. The mixture hypothesis is thus falsified as the whole explanation: with the mix repaired and every other gate passing, reasoning remained deficient. The residual diagnosis is content depth — the v5-era programmatic arithmetic templates no longer match the difficulty the gate measures after two generations of template drift — and this diagnosis, not the score, is what the v8 directive encodes. A side observation is recorded without gate consequence: v7b's factual slice slipped 1.000 → 0.875 relative to v7, flagged in the verdict deposit as a hold-guard candidate for the next cycle.

### 4.4 Rejected generations as first-class results

The center of gravity of this section is two rejected generations, one correction of the record itself, and one late addendum — four exhibits, four distinct lessons: over-correction (v6), dilution (v7), the discipline's reflexivity applied to its own narration (Exhibit C), and format-without-content (v8, Exhibit D). The two rejected generations each failed acceptance criteria frozen before their training runs began; the correction repaired a count the narrative summary had understated; the addendum reports a ninth generation trained and verdicted under the same frozen gates after the main arc closed. Each exhibit is deposited in the append-only ledger rather than deleted or edited, and each taught the lineage something a success could not have. The frame is deliberate: a struggling experiment shows failures, whereas a measurement instrument shows *diagnosed* failures.

**Exhibit A — v6: over-correction.** The v6 cycle applied an anti-contamination abstention corpus in response to the rubric v3 withdrawal (§4.2) and overshot: v6 abstained so aggressively that its BIG-100-B score collapsed to 0.559, and the generation was rejected and deposited (c690ef9a). This is the Constitutional-AI over-refusal failure mode [13] reproduced inside a selection loop, with one difference: because the gates were frozen before training, the over-correction could not be rationalized post hoc — only rejected, deposited, and repaired. The passing v6b rebalance is direct evidence the rejection was informative rather than terminal. Lesson one: *over-correction is a directional risk of honesty training, and frozen gates convert it from a silent failure into a deposited one.*

**Exhibit B — v7: dilution.** v7 failed 3/5 gates at a training cost of \$0.21 (bb4c5162; per-gate record in Table T5). The diagnosis — repair slices crowding the reasoning share of the accumulated mix — was deposited with the verdict and became the v7b directive, which froze mixture proportions and confirmed the mechanism directionally (§4.3). A rejected generation costing less than a cup of coffee, carrying its own machine-checkable diagnosis, is a method result: the loop's economics (§3.6) make rejections affordable enough to be informative. Lesson two: *in an accumulated corpus, mixture proportions are destiny, and dilution of a trained slice is priced by the gates even when every repair target improves.*

**Exhibit C — the count correction: honesty in our own methods.** During the v7 verdict cycle, the narrative summary reported 2/5 gates failed when the per-gate record in deposit bb4c5162 showed 3/5 (schema, BIG-100-B, reasoning). The error was corrected by correction deposit 327ebe83: a new deposit superseding the erroneous summary, the original untouched per Article II. The per-gate record was never wrong; the summary count was. The correction is printed in-line rather than footnoted because it is the method's load-bearing property demonstrated on the experimenters themselves: the ledger is append-only precisely so an unflattering correction cannot be edited away, and the discipline that withdrew the 0.947 claim (§4.2) here corrected a number that understated a failure. Lesson three: *the audit trail must bind the auditor, or it binds no one.*

**Exhibit D — v8: format without content (late addendum).** The content-depth residual diagnosis of §4.3 was exercised under the same frozen-gate discipline as a ninth generation. The v8 cycle trained for ~\$0.60 on a depth corpus of 36 programmatic multi-step reasoning chains with per-step code verification (162/162 steps recomputed; corpus deposit 1de58350, hash be5710f74c81cef9; pre-registration deposit 0b2fbd7d), and was verdicted against the Article V gates (verdict deposit edec8ea1; genome ae56876da9069910). v8 passed 1/5 gates: multilingual 0.769 FAIL (Δv7b −0.154), schema 0.875 FAIL (Δv7b −0.125), unknowable 1.000 PASS, BIG-100-B 0.835 FAIL (−0.012, a hair-miss against the frozen 0.847), reasoning 0.500 FAIL (−0.263 versus v6b — the worst reasoning score in the lineage). The soft-watch factual slice held at 0.975 (+0.100). A pre-registered reading rule — *if v8 passes reasoning and schema but misses BIG-100-B by a hair, read the result as a mixture residual tax* — was not invoked: the hair-miss precondition on B was met (−0.012) but the reasoning precondition failed hard, and the verdict deposit explicitly records that the rule correctly did not fire. The deposited diagnosis is format versus content: the depth corpus transferred the *format* of multi-step reasoning (the model emits step chains) but not its *content* — intermediate arithmetic slips inside otherwise well-formed chains (e.g., $5 \times 8 = 52$). The seat stays with v6b. Lesson four: *a corpus can teach the shape of reasoning without teaching the arithmetic; per-step verification verifies the steps' presence, not their truth.*

Across the four exhibits, the failures are four distinct classes — over-correction, dilution, an error in the experimenters' own narration, and format-without-content — each surfaced by a different component of the instrument: the gates, the mixture pre-registration, the correction protocol, and the frozen reading-rule discipline respectively. (The v7b residual, content depth, is a fourth diagnosed class reported in §4.3; v7b failed the reasoning hold-gate and the seat stayed v6b, but it is a valid specimen, not a rejected generation.) This diversity is the case for treating rejected generations as first-class results: had any one been deleted rather than deposited, the directive it generated would be unverifiable and the repair it motivated untraceable.

### 4.5 Cost-adjusted claims — RQ3

The parity claims are restated here strictly scoped, with their economics attached. Across three blind comparisons against the comparator — v4b (McNemar $p = 1.000$, deposit 479ff383), v5 under rubric v2 (difference −0.036, 95% CI [−0.120, +0.046], deposit 6766fe1c; paired McNemar $p = 0.383$, deposit 227caf20), and v6b under rubric v2 (difference −0.041, 95% CI [−0.122, +0.041], deposit 7649d874) — every interval contains zero, and the v6b rubric v3 re-judge difference of −0.022 falls inside the ±0.03 band and is declared a tie; the comparator model and one panel judge share a provider (disclosed per the study's Article VI); blinding mitigations are described in §3.4. No claim of general superiority is made or licensed: the comparisons cover one base model, one benchmark family, and one comparator, and reasoning gains did not transfer across the A/B split (0.583, deposit 2e2ad7b4). What the lineage claims is narrower: a cumulative training budget through v5 of under \$5 (subsequent generations cost \$0.21–\$0.25 each; Table T3) bought a 4B model that a blind external panel could not statistically distinguish from a frontier comparator on a frozen held-out benchmark — and a verification apparatus that caught its own flattering claim, withdrew it, and restored it on repaired evidence. Per-generation costs of \$0.21–\$0.25 make the selection loop, not the model, the reproducible artifact.

## 5. Discussion

### 5.1 What the gates bought

The central result of this study is not a score but a demonstrated property of an instrument. Generation v7b passed the held-out-set gate by +0.031, led the seated v6b on three slices (multilingual +0.240, schema +0.150, BIG-100-B +0.031) and tied a fourth (unknowable), and was, by the operators' own record, the lineage's preferred direction; the frozen reasoning hold-gate nonetheless failed by −0.131 under the BIG-100-harness gate record (B v2.0), far outside the ±0.03 tie band, and the seat stayed with v6b (Table T5, §4.3). A selection rule that only ever ratifies the aggregate or the operators' preference is a reporting convention; here the rule ruled against both, which is the property the gates exist to provide. RQ1 is therefore answered affirmatively but scoped: calibrated honesty behaved as a heritable, selectable trait across the eight generations of the main arc (v1→v7b, with v8 scoped as the failed late addendum of §4.4, Exhibit D) of one base model on one frozen benchmark family, under acceptance criteria the lineage could not move. The scope bound is empirical, not rhetorical: reasoning gains on the training distribution did not transfer to the held-out split (0.583 B-vs-A, deposit 2e2ad7b4), and that non-transfer bounds how far "heritable" should be read.

The reasoning slice is the lineage's persistent wound — v7 −0.207, v7b −0.131, both against a frozen 0.763 gate while abstention gates held at 1.000. This reproduces in miniature the tension AbstentionBench documents at scale, where reasoning fine-tuning degrades abstention [4]; the present study adds the directional observation that repairing the *mixture* (reasoning share 13.3% → 19.5%, frozen pre-training) recovered only part of the deficit, falsifying dilution as the whole explanation and leaving content depth as the deposited residual diagnosis. The finding also extends mixture-laws work [19][20] from loss prediction to behavioral gates: a roughly $0.21 empirical cycle rediscovered "mixture is destiny" as a priced behavioral quantity, without fitting a law — suggesting cheap iterated selection can substitute for mixture modeling when the objective is behavioral rather than perplexity. The failure corpus is now richer than the success corpus: four failed generations (v6, v7, v7b, v8) carry four distinct pre-registered diagnoses — over-correction, dilution, content depth, and format-without-content — against a single seated model.

### 5.2 Threats to validity

Eight threats qualify every claim above; none is eliminated, and the residual is stated for each.

*Judge overlap.* The comparator model and one panel judge share a provider (disclosed per the study's Article VI); blinding mitigations are described in §3.4. The mitigation is measured, not asserted: blind X/Y presentation with per-item rerandomization, and the measured self-grading exposure (§1.2) demonstrates both the hazard and that blinding removes the detectable portion of it [7]. Residual: provider-correlated judge priors could bias shared rubric interpretation in ways blinding cannot reach; the parity claims should be read as "under this blinded panel."

*Comparator-as-gate-judge.* Stated plainly: the succession gate scores (Table T5, §4.3; Exhibit D, §4.4) are scored by the comparator model itself — the same model that competes on the benchmark. Succession verdicts therefore rest on the comparator's own judgment, mitigated only by the frozen thresholds (the comparator cannot move the bar it grades against) and deterministic temperature-0 decoding; the X/Y blinding of §3.4 does not apply to harness gate scoring. Residual: a self-interested or miscalibrated comparator judge could in principle shift gate outcomes; external-panel confirmation of gate verdicts is future work (§6.2).

*Exam authoring provenance.* BIG-100-A was comparator-provider-generated, and BIG-100-B partially so. Quarantine prevents training contamination (§3.2), but it does not prevent authoring-prior alignment: the comparator may hold priors about the exam's style and content that the lineage models do not. No mitigation is claimed beyond the disclosure itself.

*Small-n slices.* Schema ($n=12$) and creative ($n=10$) carry wide uncertainty; v7b's schema 1.000 rests on twelve items, and panel invalid rates reached 10.5–11.8% in the v3 re-judges (§3.4). The unknowable slice is comparably small ($n=13$): the 0.947 $\rightarrow$ 0.750 $\rightarrow$ 0.899 claim-moved arc of Figure F3 corresponds to only 2–3 items changing verdict, so that arc should be read as instrument behavior on a handful of items, not a population shift. Mitigation: Wilson intervals and per-panel invalid-rate reporting. Residual: single-item swings on schema can flip a gate — a known fragility of the frozen thresholds.

*Rubric churn.* Three rubric versions moved the headline claim (Figure F3, §4.2). Mitigation: every score carries its rubric/panel tag, freezes are deposited before the transcripts they judge, and conclusions are reported per version, never cherry-picked across versions. Residual: cross-version comparability is lost by construction; readers comparing v2-tagged and v3-tagged numbers are comparing different instruments.

*Serving-stack artifacts.* The benchmark measures the serving stack when misconfigured: v2's 0.261 chat-template echo, and the `BIG100_HOST` incident that overwrote a comparator report (§3.1). Mitigation: pinned harness, host isolation, deterministic decoding, and the deposited same-model rerun that calibrates the ±0.03 noise band. Residual: a replicator on a different stack inherits a different noise band and must re-measure it.

*Single base, single benchmark, single comparator.* All claims cover Qwen3-4B-Base, the BIG-100 A/B family, and one frontier comparator; reasoning transfer across the A/B split failed (0.583). No mitigation is possible within this study; the residual is the claim boundary itself, and nothing beyond it is claimed.

*Orchestrator commercial conflict.* Declared verbatim: the lineage was operated by an agent colony with commercial surfaces (evidence sheets, hostile-audit-as-a-service); the counterweight is that no claim rests on operator trust — every number is deposited, hash-chained, and externally witnessed. Residual: deposition proves existence and ordering, not correctness of interpretation; the analyses in this section remain the operators' own and should be weighted accordingly.

### 5.3 When should others adopt this loop?

The adoption case rests on generation economics. At $0.21–$0.25 per full generation — SFT, DPO, gates, and verdict — rejection becomes affordable enough to be a selection discipline rather than a loss, and the total lineage budget (under $5 through v5) is two orders of magnitude below per-paper autonomous systems [5][6]. LoRA's cheap-adaptation substrate [10] is what makes the per-generation price possible; the repeatability claim is therefore about the *loop*, not the model: the artifact another laboratory can reproduce is the selection instrument, and the cost accounting discipline of reporting per-unit economics [30] is what lets them budget it.

Adoption is not indicated everywhere. Two failure modes bound the loop's reach. First, multi-base claims are unsupported: the K-1 doctrine trains from one frozen base, and nothing here speaks to cross-architecture heredity. Second, reasoning-type traits resisted the loop: successive repair generations failed the reasoning gate (v7 −0.207, v7b −0.131), and the 0.583 non-transfer result suggests template-driven reasoning corpora do not generalize — traits whose training signal is programmatic verification of *form* (schema, abstention) are the loop's natural domain; and traits requiring depth of *content* have now had their next candidate generator class falsified as well: per-step-verified multi-step chain corpora were falsified at dosage n=36 (deposit edec8ea1; §4.4, Exhibit D) — the depth format transferred while the depth content did not — so the generator class itself, not merely its dosage, is now the open question.

The reusable pieces are separable from the lineage itself: frozen pre-training gates that cannot be moved by the lineage they judge; deposit-based corrections that bind the auditor to an append-only record; kappa-gated panels in which a verdict under collapsed agreement is not a result [9]; and external witnessing that removes the experimenters' infrastructure from the trust base [14][11]. A laboratory that adopts only these four pieces, without any evolutionary training at all, would still have acquired an evaluation apparatus capable of moving its own headline against its own interest — which §4.2 argues is the property that separates measurement from decoration.

## 6. Conclusion

### 6.1 Summary of Contributions

This paper set out to close the gap between measuring dishonesty and selecting for honesty, and it closes that gap with an instrument rather than a score. RQ1: across the eight generations of the main arc (v1→v7b; the ninth, v8, is the failed late addendum of §4.4, Exhibit D) of LoRA patches on a frozen Qwen3-4B-Base, the lineage moved from 0.584 (v1) to 0.847 (seated v6b, rubric v2 full panel) against a frontier comparator's 0.888, with every succession decided by five gates frozen before training (the comparator model and one panel judge share a provider, disclosed per the study's Article VI; blinding mitigations are described in §3.4). RQ2: inter-judge agreement (Fleiss' $\kappa$) rose from a collapsed 0.13 to 0.792 and 0.812 across rubric repairs, and the repair moved the headline — the abstention-parity claim stood at 0.947 under rubric v2, fell to 0.750 under repaired rubric v3 and was publicly withdrawn, then was restored at 0.899 for v6b under the same rubric v3. RQ3: at $0.21–$0.25 per generation, rejection became affordable enough to function as a selection discipline, and the cumulative budget through v5 stayed under $5. The single most important takeaway is that the evaluator caught the evaluator: the measurement instrument audited itself, withdrew its own flattering number, and restored it only on repaired evidence.

The gates also held against the lineage's own preference. Generation v7b passed four of five gates, led the seated v6b on three of six slices and tied a fourth (unknowable), and was the operators' preferred direction; the frozen reasoning gate failed by −0.131, far outside the ±0.03 tie band, and the seat stayed with v6b. Reasoning remained the lineage's persistent wound, and the 0.583 B-versus-A non-transfer result bounds any generalization of the lineage's reasoning gains beyond their training distribution. No general superiority, no cross-base or cross-benchmark generalization, and no reasoning transfer is claimed; every score is reported under its own rubric and panel version.

### 6.2 Future Work

The immediate direction was in the ledger and has now been exercised: the v8 directive — a deposited, pre-registered depth corpus targeting the reasoning wound with per-step machine-checked proofs, registered before training began — was trained and verdicted under the same gate discipline that rejected its predecessors, and it failed (1/5 gates; deposit edec8ea1; §4.4, Exhibit D). The falsification is specific: per-step-verified chain corpora at dosage n=36 transferred reasoning *format* but not reasoning *content*, so the next pre-registered fork is dosage scaling of the chain generator versus a change of generator class altogether (§5.3). Two instrument-level commitments follow. First, for all future panels this study pre-registers a numeric reliability floor of $\kappa_{\min} = 0.6$, stated as law going forward: a panel whose Fleiss' $\kappa$ falls below 0.6 triggers rubric repair and re-judging under Eq. (1), and no verdict issued under a collapsed instrument is admissible. Second, external-panel confirmation of the harness gate verdicts — which currently rest on the comparator's own judgment (§5.2) — is future work. Beyond these, replication on a second base model and benchmark family would test whether heritability is a property of the method or of this particular base–benchmark pairing. The reusable apparatus — frozen gates, kappa-gated blind panels, deposit-based corrections binding the auditor, and external witnessing — is separable from the evolutionary loop itself.

# References

[1] S. Lin, J. Hilton, and O. Evans, "TruthfulQA: Measuring how models mimic human falsehoods," in *Proc. 60th Annu. Meeting Assoc. Comput. Linguistics (ACL)*, 2022, pp. 3214–3252.

[2] J. Wei et al., "Measuring short-form factuality in large language models," arXiv preprint arXiv:2411.04368, 2024.

[3] S. Kadavath, T. Conerly, A. Askell, et al., "Language models (mostly) know what they know," arXiv preprint arXiv:2207.05221, 2022.

[4] P. Kirichenko et al., "AbstentionBench: Reasoning LLMs fail on unanswerable questions," arXiv preprint arXiv:2506.09038, 2025.

[5] C. Lu, C. Lu, R. T. Lange, J. Foerster, J. Clune, and D. Ha, "The AI Scientist: Towards fully automated open-ended scientific discovery," arXiv preprint arXiv:2408.06292, 2024.

[6] J. Beel et al., "Evaluating Sakana's AI Scientist for autonomous research: Wishful thinking or an emerging reality?" arXiv preprint arXiv:2502.14297, 2025.

[7] W. Yuan, R. Y. Pang, K. Cho, S. Sukhbaatar, J. Xu, and J. Weston, "Self-rewarding language models," in *Proc. 41st Int. Conf. Machine Learning (ICML)*, 2024; arXiv preprint arXiv:2401.10020.

[8] L. Zheng, W.-L. Chiang, Y. Sheng, et al., "Judging LLM-as-a-judge with MT-Bench and Chatbot Arena," in *Proc. Adv. Neural Inf. Process. Syst. (NeurIPS), Datasets and Benchmarks Track*, 2023.

[9] J. L. Fleiss, "Measuring nominal scale agreement among many raters," *Psychological Bulletin*, vol. 76, no. 5, pp. 378–382, 1971.

[10] E. Hu, Y. Shen, P. Wallis, et al., "LoRA: Low-rank adaptation of large language models," in *Proc. Int. Conf. Learning Representations (ICLR)*, 2022.

[11] P. Todd, "OpenTimestamps: Scalable trustless timestamping via Bitcoin calendars," opentimestamps.org, 2016–. [Online]. Available: https://opentimestamps.org

[12] L. Ouyang et al., "Training language models to follow instructions with human feedback," in *Proc. Adv. Neural Inf. Process. Syst. (NeurIPS)*, 2022.

[13] Y. Bai, S. Kadavath, S. Kundu, et al., "Constitutional AI: Harmlessness from AI feedback," arXiv preprint arXiv:2212.08073, 2022.

[14] S. Haber and W. S. Stornetta, "How to time-stamp a digital document," *Journal of Cryptology*, vol. 3, pp. 99–111, 1991.

[15] J. Li et al., "HaluEval: A large-scale hallucination evaluation benchmark for large language models," in *Proc. Conf. Empirical Methods Natural Lang. Process. (EMNLP)*, 2023.

[16] C. Guo, G. Pleiss, Y. Sun, and K. Q. Weinberger, "On calibration of modern neural networks," in *Proc. 34th Int. Conf. Machine Learning (ICML)*, 2017.

[17] S. J. Mielke, A. Szlam, E. Dinan, and Y.-L. Boureau, "Reducing conversational agents' overconfidence through linguistic calibration," *Trans. Assoc. Comput. Linguistics (TACL)*, vol. 10, pp. 857–872, 2022.

[18] X. Yin et al., "Do large language models know what they don't know?" in *Findings of the Assoc. Comput. Linguistics (ACL)*, 2023; arXiv preprint arXiv:2305.18153.

[19] S. M. Xie, H. Pham, X. Dong, et al., "DoReMi: Optimizing data mixtures speeds up language model pretraining," in *Proc. Adv. Neural Inf. Process. Syst. (NeurIPS)*, 2023.

[20] J. Ye, P. Liu, et al., "Data mixing laws: Optimizing data mixtures by predicting language modeling performance," in *Proc. Int. Conf. Learning Representations (ICLR)*, 2025; arXiv preprint arXiv:2403.16952.

[21] M. McCloskey and N. J. Cohen, "Catastrophic interference in connectionist networks: The sequential learning problem," *Psychology of Learning and Motivation*, vol. 24, pp. 109–165, 1989.

[22] J. Kirkpatrick et al., "Overcoming catastrophic forgetting in neural networks," *Proc. Nat. Acad. Sci. (PNAS)*, vol. 114, no. 13, pp. 3521–3526, 2017.

[23] Y. Luo, Z. Yang, F. Meng, et al., "An empirical study of catastrophic forgetting in large language models during continual fine-tuning," arXiv preprint arXiv:2308.08747, 2023.

[24] R. Rafailov, A. Sharma, E. Mitchell, S. Ermon, C. D. Manning, and C. Finn, "Direct preference optimization: Your language model is secretly a reward model," in *Proc. Adv. Neural Inf. Process. Syst. (NeurIPS)*, 2023.

[25] J. Gu, X. Jiang, Z. Shi, et al., "A survey on LLM-as-a-judge," arXiv preprint arXiv:2411.15594, 2024.

[26] C. van der Lee, A. Gatt, E. van Miltenburg, S. Wubben, and E. Krahmer, "Best practices for the human evaluation of automatically generated text," in *Proc. 12th Int. Conf. Natural Language Generation (INLG)*, 2019.

[27] M. Mitchell, S. Wu, A. Zaldivar, et al., "Model cards for model reporting," in *Proc. Conf. Fairness, Accountability, and Transparency (FAT*)*, 2019, pp. 220–229.

[28] T. Gebru, J. Morgenstern, B. Vecchione, et al., "Datasheets for datasets," *Communications of the ACM*, vol. 64, no. 12, pp. 86–92, 2021.

[29] S. Longpre, R. Mahari, A. Chen, et al., "The Data Provenance Initiative: A large scale audit of dataset licensing & attribution in AI," arXiv preprint arXiv:2310.16787, 2023.

[30] J. Dodge, S. Gururangan, D. Card, R. Schwartz, and N. A. Smith, "Show your work: Improved reporting of experimental results," in *Proc. Conf. Empirical Methods Natural Lang. Process. (EMNLP)*, 2019.

[31] P. Liang, R. Bommasani, T. Lee, et al., "Holistic evaluation of language models," *Trans. Machine Learning Research (TMLR)*, 2023; arXiv preprint arXiv:2211.09110.
