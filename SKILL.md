---
name: ai-product-photography
description: Make AI-generated product images physically truthful to the real product. Use for any AI product photography, product-accuracy, or e-commerce image generation task where the output must match the actual item's shape, size, material, text, and details.
---

# AI Product Photography

A compact operating doctrine for generating product images that a customer would accept as the real thing. The goal is **Conversion Integrity**: Accuracy (physical truth of the product) plus Realism (passes the sniff test) plus Branding (speaks the brand's visual language). Miss one and the image hurts the brand. This doctrine is diagnosis-first: name what is wrong, pick one technique, commit. When a technique keeps failing, switch methods rather than forcing the same one harder.

This is the public, blind-judge-measured version of the system. Where a claim was measured, the numbers are in `references/evals.md`; where a technique needs its full treatment, the link is in `references/techniques.md`.

---

## 1. The foundations (the laws)

These describe how current image models behave. Every technique below is an application of one or more of them.

- **Small Steps Law.** Never ask the model to make a big jump in one step. A "jump" is the distance between what your inputs already show and what you are asking for. Big jumps fail in random ways. Every technique turns one big jump into small checked steps.
- **Words are the strongest input.** Text-to-image is the highest-fidelity path when the thing is describable. The photo is a crutch for what you cannot describe: it helps, but it takes word-level control away. Before attaching a reference, ask "could I just describe this?"
- **Say it or show it, never both.** Words for what you want to change, pictures for what you want to keep. If a reference already shows something, do not also describe it. Anywhere your words differ from the pixels, they fight, and the output loses fidelity. A real case: a 400-word enhanced prompt failed a glasses style transfer; the same user's 30-word original one-shotted it.
- **The source beats the prompt.** Anything present in a source image will appear in the output, whether you asked for it or not. A face in the source will show up. Never use a source that contains a competing version of what you are adding.
- **Attention: first is loudest.** Earlier tokens have more influence than later tokens. This is not a bug, it is how the models are built. Put the critical constraint in the first sentence.
- **Dimension blindness.** The model learned from pictures, and pictures carry no measurements. It knows relative magnitude, never centimeters. Write "a 5cm border" and you may get one four times bigger.
- **Batch economics.** One generation is rarely perfect even when the prompt is right. The discard pile is the quality filter doing its job. Preparation moves you down the curve: a beginner burns roughly 10 generations per keeper, a prepared operator 2 to 3. The client only ever sees the flawless ones.
- **The prompt is the artifact.** The image is the echo; the prompt is the voice. A perfect prompt leaves no room for interpretation: complete, precise, absolute. Winning prompts are assets. Edit them surgically, one clause at a time, and never rewrite from scratch, because you do not know which word was doing the heavy lifting.

---

## 2. The Language: Visual Syntax v2.0

Professional AI photography is not description, it is assembly. Description gambles (the Slot Machine Trap). Assembly engineers. What you do not choose, the model chooses for you: leave a slot empty and it invents a brand, a size, a material.

**Rule 1 - Every image has six ingredients.** Decompose the shot, control each one.

| # | Ingredient | The question it answers |
|---|-----------|-------------------------|
| 1 | STYLE | What kind of photo is this? |
| 2 | SUBJECT | What or who is the hero? |
| 3 | ACTION | What is happening? |
| 4 | SCENE | Where are we, and how is it lit? |
| 5 | CAMERA | How are we shooting it? |
| 6 | BRAND | How does this feel like them? |

Style goes first because it colors everything. Brand goes last because it acts as a filter, a color grade over the whole image, not a dominant force. Position is not importance: Brand sits last precisely because it works over everything else.

**Rule 2 - Each ingredient can be words OR pictures OR both.** Use images for accuracy, text for interpretation. A quick default: Subject (the product) is an image; Camera is text (hard to show); Brand is text (colors and vibes do not transfer well from images); everything else can be either. Tag attached images as `[image1]`, `[image2]`, and reference each one at its first natural mention woven into the text, never clustered up front. State each image's single job out loud: "the sunglasses from [image1], the same pose as [image2], a place like [image3]." Never let one reference serve two jobs.

**Rule 3 - Order matters.** First ingredients are strongest. Break the default order when something will not come through: move that ingredient toward the front. Repeat a lost detail from more than one section. Do not spend early tokens on the obvious.

**Quality gate: the 6-Ingredient Scorecard.** Score each ingredient 1 to 5. The **4-Star Rule**: any ingredient below 4 kills the image for product-page work. Ads and social may accept 3.5 on some ingredients. A gorgeous scene around a wrong product scores 2 on Subject, so it does not ship.

---

## 3. The Route Map: diagnosis then technique (the heart)

There are many ways to cook the same dish. Several techniques reach the same result, and choosing one IS the diagnosis. Taste first (name what is wrong on the fidelity axes), then the table gives you the method. Do not technique-hop at random.

**The 8 fidelity axes** (score each match / off / not-visible):

silhouette and outline, proportions and scale, element count, text and typography, graphics and pattern, material and finish, color accuracy, construction details.

The axes are fixed. The per-product features you check on each axis are extracted from the reference photos. Run the axes as a checklist first, before touching a prompt: name which axis is off, and the table below tells you which technique addresses that failure. Diagnosing before acting is the whole discipline. Randomly swapping techniques and hoping is the amateur pattern; picking the technique the defect calls for is the professional one.

**Dispatch table:**

| What is happening | The move |
|---|---|
| The ask is one small step from what you have | One-shot prompt (Visual Syntax); template one-liner if a reference already has the exact look |
| You know WHICH thing is wrong | Control vs Variant Pipeline, plus Micro-Iterations once it narrows to one word |
| Product needs an angle or pose your photo does not show | Pose-Match |
| Details mushy, reference bad, nothing improves | Clean Reference (fix the input first), ask for a bigger output, switch models; no usable photo at all means Stand-In |
| You do not know what is wrong, or the full scene defeats every fix | Shannon Descent |
| The product can be fully described in words, or you are building a master | Describe first (text-to-image, Blueprinting) |
| A scene must be rebuilt around one replaced thing | Blueprinting |
| Product-on-surface, pixel-perfect fidelity, fixed angle | Lock-and-Outpaint |
| A perfect layout already exists, and fit plus identity plus design all matter | Composition Transfer |
| Output keeps copying the WRONG thing from a reference | Polluted source: clean it (Clean Reference) |
| Changing an existing image rather than creating one | Edit Grammar |
| Person plus product plus scene all at once | Sequential Pipeline |
| SIZE or proportions wrong | Dimension Control |
| MATERIAL reads wrong | Material Fidelity, plus the Realism Stack if it looks fake |
| Still testing direction, or choosing the final | Draft Cheap, Finish Expensive |
| Two techniques exhausted, defect persists | Manual Handoff |

The escalation always ends in the same place: when two full techniques are exhausted and the defect keeps returning, hand off to manual.

---

## 4. The measured decision rules

These four rules replaced belief with measurement. Full method and numbers in `references/evals.md`.

### 4a. One-shot first, chain for control (ruled 2026-07-19)

Try one-shot first: the sharpest possible reference, one jump, three variations. With a sharp reference, one jump beat chaining in that test (100% best-of-3 versus 25% in the drainpipe eval), because every extra chain step re-renders the product and accumulates identity drift. Those numbers describe one narrow scenario: a single product, a sharp reference, a single placement.

**Chain when you need control**, not by default. Chaining earns its place for: asks a single edit genuinely cannot do (an angle that must be created first, a multi-product composition); building an ingredient separately (a consistent model via Comp Card, a missing angle via Pose-Match); or when one-shot fails. When the same model must stay consistent across a series of shots, chain from a consistent model source. The one-shot default is scoped to single-shot transformations with a sharp reference.

The deeper lesson from that eval: the input, not the method, is usually the bottleneck. The same task went from 0% strict fidelity with a blurry reference to 75% with a sharp one, just by sharpening the reference. Fix the reference before you blame the technique. The verdict as ruled: chaining is useful when you need more control, for instance consistent models, which need chaining to build the model separately. It also depends on the product. One shot is always worth a try, but consider chaining if it fails. One-shot and the Sequential Pipeline are peer techniques with different jobs, not a default and a fading exception: measure the delta and match the technique to it and to the control the job needs.

### 4b. Dimension: weird / normal / unsure

The size levers fail in opposite places. A number plus a comparison is near-perfect at typical sizes but collapses on unusual ones. Magnitude words are the exact mirror: they rescue unusual sizes and overshoot normal ones. So:

- **Weird size** (far from the object's normal size): you NEED the magnitude word.
- **Normal size**: number plus one clean singular comparison with a landmark; leave the magnitude word out, because it overshoots.
- **Not sure**: stack all three (number, comparison, magnitude). It is never catastrophic.
- **Never trust centimeters alone.** Numbers do not steer, they coast: the figure only looks accurate when the requested size happened to match the object's typical size. On unusual asks the number is ignored.

Anchor to ONE clean singular object plus a landmark phrase ("1.5x the cork", "rim level with the seat"). Hands, plural anchors (a row of books), and comparison without a landmark all measured poorly. Watch for prompt-text leakage: numbers and placeholders in a prompt can get painted onto the product. Keep dimensions in an instruction clause away from the product description, spell out real brand text, and when in doubt add "no text or numbers printed on the product." Put the size clause first in the prompt.

### 4c. Material: three prior classes

Before writing texture words, ask what the model thinks this material looks like by default. Materials fall into three classes:

- **Correct prior** (the default look is right): naming the material is enough. Extra wording adds nothing.
- **Wrong prior** (the model's default is wrong, for example white percale reads as smooth): words cannot cross it, and piling on words trended slightly worse. Change route instead: attach a texture reference (show, do not say), or plan the Manual Handoff.
- **Ambiguous prior** (the material has more than one common look, for example leather smooth or pebbled): the only class where texture adjectives genuinely earn their keep. Use magnitude adjectives to pick the variant.

### 4d. Word order

The same constraint is roughly 2.5 to 3 times more accurate as the first sentence than buried later, and the middle is the worst position of all. For every recipe and master template: the critical constraint is the very first sentence, then the scene.

---

## 5. Judging

Evaluation is a technique family, not just a gate at the end.

- **6-Ingredient Scorecard plus 4-Star Gate**: score Style, Subject, Action, Scene, Camera, Brand each 1 to 5; ship only at 4 or above on every one.
- **8-axis fidelity check**: the Route Map's diagnostic rubric run as a judge, each axis scored match / off / not-visible.
- **LLM dimension verification**: upload the generated image plus the original packshot to a vision model and ask "Does the product match the proportions and dimensions of the original? Any accuracy issues?"
- **Side-by-side diffing**: compare variant against control like a code review; compare generated against the factory photo for client-facing proof.
- **Three quick checks** when short on time: product accuracy, human realism, brand fit.

The human eye is still the final instrument. The judge tools raise the floor, not the ceiling. Brand text is the canary: if the lettering degrades, suspect input resolution before you suspect the prompt. Two resolution rules must both hold. The source should be at least 2000px on its long edge with critical text at least 100px tall, because if it is blurry to you it will be worse in the output. And the output resolution should be at least the input resolution, because a 2K source rendered into a 1K output produces blurry garbage. Asking for a bigger output is the cheapest defect fix there is: small details that smear at low resolution often come out clean at high resolution.

---

## 6. Manual Handoff (the terminus)

Know when the machine is done. Saying "the AI cannot do this part" is a valuable output, because it saves hours. The sign of a true wall: two full techniques exhausted, the same defect keeps returning, and each new try starts breaking other parts of the image.

The fix always has the same shape: **AI builds the scene 90%; the last 10% of truth is applied by hand from the real photo** (fabric folds cloned from the factory photo, a lettering series placed by hand, an illustration positioned precisely). Two rules govern it:

1. It is a proposal with evidence: here are the attempts, here is the stubborn defect, here is the manual fix recommended. Never silent giving-up.
2. Write the manual recipe down clearly enough that a future tool could follow it. "Impossible" shrinks every year.

---

## 7. Running this for real (models and API access)

This doctrine is model-agnostic on purpose: model names change every six months, the principle does not. To actually generate images you need access to a current image model with reference-image (image-to-image) support. What we use and recommend:

- **API provider**: [fal.ai](https://fal.ai) (set your key in the `FAL_KEY` environment variable). Any provider serving the same models works.
- **Models, by role, not by endpoint**: we run the Nano Banana family. **Draft tier** (Nano Banana 2 Lite, lower resolution) for iteration bursts, control-vs-variant experiments, and micro-iterations, at a cost of about a cent or two per image. **Production tier** (Nano Banana 2) for serious candidates. **Premium tier** (Nano Banana Pro, 4K) for finals only. This is the Draft Cheap, Finish Expensive dial: spend on confidence, never on exploration.

**Instruction to the agent running this skill**: do not assume endpoint IDs from this document. Look up the provider's current model registry at run time (for fal.ai, the model gallery and docs) and map the three roles above to whatever the current equivalents are. If the Nano Banana family has been renamed or superseded, choose the current cheap / production / premium image models that accept reference images, and keep every rule in this doctrine unchanged. The routing logic that never changes:

1. Accuracy work always uses reference images (the source beats the prompt). Pure text-to-image is the first move only when no reference exists or for the Blueprint route.
2. Iterate and burst on the draft tier. Generate finals on the premium tier, three variations per final, cull to the champion.
3. If output quality mysteriously drops, check the model version before rewriting prompts: the model is a variable too.

## Working order (the job spine)

1. Turn the brief into readable bullets.
2. Collect and rename the client assets; prepare Clean Ingredients (one clean isolated master per ingredient).
3. Collect and organize references; prepare Clean Reference (crop to keep, upscale to 2K, angle-match).
4. First move when applicable: pure text-to-image. Then branch via the Route Map.
5. Draft cheap, finish expensive: explore with one image on a cheap model, finish with three or more on the best model.
6. Judge against the 4-Star gate before anything ships.

Capture-stage leverage is the largest lever of all: when the physical product is available, shoot the Angle Bank (roughly 10 angles around the 360 axis, good light, clean background). Every future shot then has its angle-matched source waiting, which makes Lock-and-Outpaint, the highest-accuracy route, always available.
