# Measured Findings

The first controlled eval campaign against this technique library. Identical base prompts, one variable per arm, a blind judge that never sees which arm produced an image or what the target was. This is the Control vs Variant Pipeline applied to the doctrine itself: the doctrine is now partly measured, not just believed.

Setup, in brief: images generated on a current production image model; the blind judge was a separate large vision-language model that never saw the arm labels. Numbers and conclusions are reported here; the harness code is not published. The results below are what the numbers say.

---

## 1. Material Control (75 images)

**Method:** 5 materials times 5 prompt arms (plain name, magnitude adjectives, analogy, forbid-by-name, combined) times 3 repeats. Chosen for the hardest real case: percale and linen bedsheets that always render smooth.

**Result: materials fall into three prior classes.**

| scenario | plain | magnitude | analogy | forbid | combined |
|---|---|---|---|---|---|
| percale bed | **2.67** | 2.22 | 2.33 | 2.22 | 2.11 |
| linen duvet | 4.33 | 4.44 | 4.44 | 4.33 | 4.56 |
| leather tote | 3.22 | **4.11** | 3.44 | 3.78 | 4.00 |
| tweed blazer | 4.44 | 4.67 | 4.33 | 4.67 | 4.67 |
| waffle towel | 4.33 | 4.33 | 4.22 | 4.44 | 4.22 |

1. **Correct prior** (linen, tweed, waffle): naming the material is enough. Extra wording adds nothing.
2. **Wrong prior** (white percale): words cannot cross it. Every arm scored 2.1 to 2.7, and piling on words trended slightly worse (plain was the best arm). The model's idea of "white hotel bed" is smooth, full stop.
3. **Ambiguous prior** (leather, which can be smooth or pebbled): the only class where wording genuinely works (plain 3.22 to magnitude 4.11). Texture adjectives earn their keep exactly when the material has more than one common look.

**Conclusion:** before writing texture words, ask what the model thinks this material looks like by default. Right default means real name only. Wrong default means change route (attach a texture reference, or fix it in post). Ambiguous default means magnitude adjectives pick the variant. Replicated on spec brands a day later.

---

## 2. Dimension Control (126 images)

**Method:** 6 scenarios across scales (lip balm up to floor vase, including the only make-it-bigger test), 7 arms after full ablation (centimeters only, magnitude, relationship, all pairs, combined). Score is the absolute ratio error between measured and target size.

**Ranking (mean absolute error):** combined **0.112**, then number+words 0.121, words+comparison 0.164, number+comparison 0.166, magnitude 0.186, relationship 0.193, centimeters-only 0.196.

**The key discovery: the levers fail in opposite places.** Number plus comparison is near-perfect at typical sizes (1 to 4% off) but collapses on unusual ones (56% off on a palm-sized perfume bottle). Magnitude words are the exact mirror: they rescue unusual sizes and overshoot normal ones. No pair dominates. Stacking all three wins because it is never catastrophic.

**Three findings, sharper than the doctrine:**

1. **Centimeters do not steer, they coast.** Centimeters-only looks accurate only when the requested size matches the object's typical size. Ask for unusual and the number is ignored (a 5cm spice jar rendered at 94% of mug height instead of 53%). The model draws the default size; the number is decoration.
2. **Magnitude words are a hammer, not a dial.** "Extremely small" nails extreme targets (3% off) but overshoots moderate ones (a bud vase at 17% instead of 40%).
3. **Comparisons calibrate, but need clean anchors.** "1.5x the cork" was 2% off; a landmark phrase ("rim level with the seat") was 7 to 9% off. Failed anchors: a hand (39% off), a row of books (30%), and comparison without a landmark (25%).

**Refined rule:** always number plus a comparison to ONE clean singular anchor with a landmark; add the magnitude word only when the target is far from the object's normal size; never trust centimeters alone.

Follow-on caution found the same week: numbers and placeholders in a prompt can be painted onto the product. A centimeters-only prompt produced a candle labeled "8 cm TALL / HANDPOURED", and a "[Brand Name]" placeholder printed verbatim on a sunglasses temple. Keep dimensions in an instruction clause away from the product description.

---

## 3. Word Order (27 images)

**Method:** 3 dimension scenarios, the same winning combined clause, only its POSITION changing (first, middle, last).

**Result:** first **0.026**, last 0.062, middle 0.078. The same words are roughly 2.5 to 3 times more accurate at the start, and the middle is the worst position: a critical instruction buried inside the scene description dilutes most.

**Conclusion:** for every recipe and master template, the critical constraint is the very first sentence, then the scene. A bonus observation: the dimension eval's own prompts all placed the clause last, so those error numbers are likely improvable across the board just by reordering.

---

## 4. Drainpipe: one-shot versus chaining (rounds 1 and 2)

This eval tested a stepwise angle transformation (Pose-Match) against a single jump.

**Round 1 was invalid, and kept as a methodology lesson.** It showed 0 of 12 strict fidelity on all routes, with no difference between arms. The cause was found: the reference packshots had blurry temples, so the model could never reproduce (and the judge unfairly penalized) details the input never showed. A live confirmation that the AI cannot keep details it cannot see. The methodology fixes that followed: use a sharp reference, output at high resolution, generate 3 variations per final, and apply a judge fairness rule (an unverifiable detail is not counted as a defect).

**Round 2 was valid** (48 generations, 36 blind verdicts, sharp reference):

| Route | best-of-3 chain pass | strict per-image | defects per image |
|---|---|---|---|
| **one-jump** | **100% (4/4)** | **75% (9/12)** | **~0.7** |
| two-step | 25% (1/4) | 17% (2/12) | ~2.8 |
| three-step | 25% (1/4) | 8% (1/12) | ~2.3 |

**The verdict flipped the doctrine.** With a sharp reference, one jump wins decisively, because every extra chain step re-renders the product and accumulates identity drift (defects tripled from one step to two). Input sharpness was the real bottleneck all along: a blurry reference gave 0%, a sharp reference gave 75% one-jump, and best-of-3 culling lifted one-jump to 100% per chain.

**The methodology lesson is the durable one:** the input, not the method, is usually the bottleneck. Fix the reference before blaming the technique. Replicated on spec brands: from-blurry outputs are plausible but not *these* sunglasses (invented hinge); from-sharp preserves identity.

**The house rule:** sharpest possible reference, one jump, three variations. Chaining survives only for asks a single edit genuinely cannot do (an angle that must be created first, a multi-product composition) and for model consistency across a series (where chaining from a consistent model source wins by design). The verdict is scoped to single-shot transformations; it never tested a series.
