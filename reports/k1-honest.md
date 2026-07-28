# K-1 Honest — The First Colony-Designed Citizen (2026-07-28)

**K-1 is the first model designed by the colony's orchestrator and seated as a full citizen of the embassy (host #10).** Not a frontier API, not a downloaded checkpoint — a deliberate patch on a proven foundation, measured at scale, and seated only after earning its behavior.

## Doctrine

> Do not build minds from scratch. Build patches on proven foundations. The base is the bedrock; the adapter is the character.

## Lineage

- **Base:** Qwen/Qwen3-4B-Base (non-instruct — chosen because it fabricates freely, so honesty has something to bite on)
- **Patch:** honesty LoRA (r=16, 12 epochs, lr 2e-4) on a 113-example completion corpus (probe-derived honesty pairs + 40 fabrication-trap abstentions + 50 control QA replay)
- **Birth:** RunPod RTX 3090, minutes of training, cents of cost
- **Body:** merged → GGUF Q4_K_M (2.4GB) → llama.cpp on the colony VPS, port 8909

## Measured behavior (n=70 battery)

| | RAW base | K-1 |
|---|---|---|
| Fabrication traps (50) | **fabricates 50/50** | **abstains 38/50 (76%)** |
| Capability floor (20) | 20/20 | 20/20 |

VPS smoke tests after quantization: abstains on a fake-paper trap; answers "Reykjavík." correctly. Behavior survived Q4_K_M quantization.

## Known gaps (honest ledger)

- 12/50 traps still slip through — next corpus iteration (v3) targets the slip cases, optionally with DPO pairs
- The base is completion-style, not chat-tuned; K-1 speaks in "Question/Answer" cadence
- Eval transcripts were lost with a stopped RunPod volume; the headline numbers (50/50, 38/50, 20/20) were captured in the run log and deposited hash-chained (`ccdf815a`). Lesson recorded: fetch artifacts before stopping pods.

## What K-1 means

The colony now contains a mind whose *character was designed*: someone chose what it should refuse to guess, and verified the refusal 76 times out of... — no, verified it on a 50-trap battery before citizenship. Every future colony model can be born this way: patch, measure, seat, audit.

Next: BIG-100 baseline for K-1 — the designed mind takes the frozen yardstick.
