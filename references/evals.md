# Doctrine Evals — the measured findings

Based on the AI product photography accuracy doctrine by Bertrand / dezygn.com. This is the credibility layer: a first controlled eval campaign against the technique library above, run with identical base prompts, exactly one variable changed per arm, and a blind vision-model judge that never saw which arm it was scoring or what the target value was. The point of this page is honesty, not marketing — several results *overturned* prior assumptions in the doctrine itself, and that's noted explicitly wherever it happened.

**Method, in general** (applies to all four evals below): pick one falsifiable claim from the technique library; design arms where exactly one variable differs (the wording, the position, the route); run 3+ repeats per arm; score with a blind judge that never sees the arm label or the target value; treat anything not visible in the reference image as unverifiable, never as a defect (the judge can only be as fair as the reference is complete); write up an honest-interpretation section covering what the eval did NOT test and where sample sizes are thin. Findings carry a date and an implicit model-version — they are expected to expire and get re-tested as models change.

---

## 1 · Material Control — testing Material Fidelity

**Setup**: 5 materials × 5 prompt arms (plain material name / magnitude adjectives / craft analogy / forbid-by-name / all combined) × 3 repeats = 75 images. Chosen around the hardest real recurring case: percale-weave bedsheets, which models consistently render smooth regardless of wording.

**Result — materials sort into three distinct "prior" classes**:

| Scenario | Plain | Magnitude | Analogy | Forbid | Combined |
|---|---|---|---|---|---|
| Percale bedding | 2.67 | 2.22 | 2.33 | 2.22 | 2.11 |
| Linen duvet | 4.33 | 4.44 | 4.44 | 4.33 | 4.56 |
| Leather tote | 3.22 | **4.11** | 3.44 | 3.78 | 4.00 |
| Tweed blazer | 4.44 | 4.67 | 4.33 | 4.67 | 4.67 |
| Waffle towel | 4.33 | 4.33 | 4.22 | 4.44 | 4.22 |

1. **Correct prior** (linen, tweed, waffle) — simply naming the real material is enough; extra wording adds essentially nothing.
2. **Wrong prior** (white percale) — no wording crosses it. Every arm scored 2.1-2.7, and piling on more words trended slightly *worse* (the plainest arm was actually the best one). The model's default idea of "white hotel bed" is smooth, full stop, and no adjective stack talks it out of that default.
3. **Ambiguous prior** (leather — plausibly smooth OR pebbled) — the only class where wording genuinely paid off: plain naming scored 3.22, magnitude adjectives lifted it to 4.11. Texture adjectives earn their keep exactly when a material has more than one common look in the model's training data.

**The rule this produces**: before writing a single texture word, ask what the model already thinks that material looks like by default. If the default is right, name it and stop — more words don't help and can mildly hurt. If the default is wrong, no amount of wording will fix it — get a texture reference attached instead, or route to a manual finish. If the material is genuinely ambiguous, adjectives are the one case where they're worth writing.

**Open follow-up noted honestly**: does an attached close-up texture reference cross the "wrong prior" wall that words alone could not? Untested as of this writing.

---

## 2 · Dimension Control — testing the magnitude-ladder / comparison-anchoring toolkit

**Setup**: 6 scenarios spanning a wide range of scales (from a lip balm up to a floor vase, including the only test that asked the model to make something BIGGER rather than smaller), 7 arms from a full ablation (centimeters-only / magnitude words / relationship-only / every pairing / all combined), 126 images total, scored by a blind ratio judge measuring |actual size ratio − target ratio|.

**Ranking, mean absolute error (lower is better)**:

combined **0.112** > number+words 0.121 > words+comparison 0.164 > number+comparison 0.166 > magnitude 0.186 > relationship 0.193 > centimeters-only 0.196

**The key discovery — the levers fail in OPPOSITE places.** Number + comparison is near-perfect at typical, expected sizes (1-4% error) but collapses badly on unusual asks (56% error on a deliberately palm-sized perfume bottle). Magnitude words are almost the exact mirror image: they rescue unusual sizes but overshoot moderate, ordinary ones. Neither one dominates on its own — stacking all three levers wins specifically because the combination is never catastrophic in either direction.

**Three sharper findings than the original doctrine assumed**:

1. **Centimeters don't steer, they coast.** A centimeter figure only *looks* accurate when the requested size happens to already match the object's typical size. Ask for something unusual and the number gets effectively ignored — a request for a 5cm spice jar rendered at 94% of a mug's height instead of the correct 53%, because the model drew its default size and treated the number as decoration rather than instruction.
2. **Magnitude words are a hammer, not a dial.** "Extremely small" nails genuinely extreme targets (3% error) but badly overshoots moderate ones — a request for a modestly larger bud vase rendered 17% larger instead of the requested 40%; "notably tall" on a lip balm produced 2.0-2.2× height instead of the target 1.55×.
3. **Comparisons calibrate well, but only with a clean anchor.** "1.5× the width of the cork" landed within 2%. A landmark phrase ("rim level with the seat") landed within 7-9%. The anchors that FAILED: a hand (39% error), a row of similar objects like books (30% error), and a comparison stated without any landmark at all (25% error).

**The resulting decision rule**: always use a number plus a comparison to ONE clean, singular anchor with an explicit landmark phrase. Add the magnitude word only when the target size is genuinely far from the object's normal size — for a normal-range ask, the magnitude word actively overshoots and should be left out. Never trust a bare centimeter figure to do any steering on its own.

---

## 3 · Word Order — testing the attention-hierarchy rule

**Setup**: 3 dimension scenarios, the exact same winning combined clause from eval #2, with only its POSITION in the prompt varied (first / middle / last), 27 images, scored by the same blind judge.

**Result (mean absolute error)**: FIRST **0.026** · LAST 0.062 · MIDDLE 0.078.

This confirms and quantifies the attention-hierarchy rule directly: identical words are roughly **2.5-3× more accurate** when placed as the very first sentence of a prompt compared to placed later. The more surprising part: **middle is the worst position of all** — a critical instruction buried inside a scene description dilutes attention on it more than putting it dead last does. The practical rule for any recipe or master prompt template: state the critical constraint as the first sentence, and describe the surrounding scene after it. (Side note: because every scenario in eval #2 above had its clause placed last, those dimension-control numbers are likely improvable across the board just by moving the clause to the front — worth re-testing.)

---

## 4 · The Chaining Question — testing one-jump vs multi-step transformation

**Setup and false start (kept in the record as a methodology lesson, not deleted)**: round 1 tested 0/12 strict fidelity across every chaining route, with literally no difference between arms — a "null result" that initially looked like it disproved the whole premise. Investigating turned up the real cause: the reference photo used had blurry temple/hinge detail on the eyewear being tested, and the model could never reproduce (and the judge was unfairly penalizing the absence of) detail the source never actually showed clearly. This is a direct, costly confirmation that the model can't retain details it was never given cleanly in the first place — and it's exactly why a null result still counts as a finding, but only when the write-up is honest enough to catch its own limits before assuming the conclusion.

**Round 2 (valid)**: a properly sharp three-quarter packshot with legible temple text, upscaled, rendered at 4K output, with 3 variations generated per final step and an explicit judge fairness rule (anything unverifiable in the reference is not counted as a defect). 48 generations total, 36 blind verdicts.

| Route | Best-of-3 chain pass rate | Strict per-image pass rate | Defects per image |
|-------|---------------------------|------------------------------|--------------------|
| One-jump (single transformation) | **100% (4/4)** | **75% (9/12)** | **~0.7** |
| Two-step chain | 25% (1/4) | 17% (2/12) | ~2.8 |
| Three-step chain | 25% (1/4) | 8% (1/12) | ~2.3 |

**The verdict flips the prior assumption.** With a genuinely sharp reference, one direct jump wins decisively — every additional chain step re-renders the product from scratch and accumulates identity drift, and defect counts roughly quadrupled going from one step to two. Input sharpness was the real bottleneck the entire time: the identical blurry reference produced 0% regardless of route, while the sharp reference produced 75% in a single jump. Generating 3 variations and keeping the best measurably lifted the one-jump route from 75% per-image to 100% per-chain — a legitimate, cheap quality lever, far cheaper than adding pipeline steps.

**The resulting house rule**: default to sharpest-possible reference + one direct jump + 3 variations, and cull to the best. Reserve multi-step chaining for asks that a single edit genuinely cannot accomplish in one pass (an angle that must be synthesized before anything else can happen, or a multi-product composite). Chaining is the exception now, not the default route — and this boundary is expected to keep shrinking as models improve.

---

## Reading these results honestly

A few standing caveats worth repeating, since they're part of what makes this data trustworthy rather than promotional:

- **Sample sizes here are modest** (27-126 images per eval) — enough to establish clear rankings and directional rules, not enough to claim precise universal error percentages for every possible product or scenario.
- **These are snapshots of a specific model generation.** The dimension and material "priors" in particular are properties of what a specific model was trained on — they will shift, and possibly invert, as models are retrained. Re-test standing rules whenever the underlying model changes.
- **A null result is still a result**, provided the write-up is honest enough to look for its own bugs before accepting the conclusion — the invalidated round 1 of the chaining eval is kept in this record specifically to make that point, not hidden as an embarrassment.
- **The judge is only as fair as the reference is complete.** Any defect claim against a detail the source image never clearly showed is not a real defect — it's an artifact of an incomplete reference, and every eval here enforces that rule explicitly.

The deeper point of running controlled evals at all: competitors can copy a technique's *name*. They can't as easily copy the discipline of measuring whether it actually works, by how much, and where it breaks — that measurement habit is the part worth building for yourself.
