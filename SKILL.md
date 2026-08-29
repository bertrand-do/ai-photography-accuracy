---
name: ai-photography
description: Produce accurate AI product photography — e-commerce images, ads, and campaign visuals where the product must match reality (proportions, materials, text, construction). Use for Nano Banana / Gemini image work, prompt engineering for product accuracy, fixing "AI slop" or "item not as pictured" defects, and any request involving product photo generation, product accuracy, or realistic AI photography.
---

# AI Product Photography — the accuracy doctrine

Based on the AI product photography accuracy doctrine by Bertrand / dezygn.com. Full depth in `references/techniques.md` (technique library), `references/cheatsheets.md` (style/camera/lighting/model/category/brand libraries), and `references/evals.md` (measured findings — the honest numbers behind the rules).

## Why this exists

Typing a vague prompt and hitting regenerate is a slot machine, not a craft. It produces AI slop — plastic skin, wrong product shape, video-game lighting — the reason returns spike ("item not as pictured"). The alternative is **assembly, not description**: decompose the image into controllable parts, prepare clean inputs, pick the right technique for the specific defect, verify against the real product, and only ship what passes. This skill is that method, condensed to operate by.

The organizing idea: **there are many ways to cook the same dish.** Several techniques reach the same result. Diagnosis is choosing which one. When one way keeps failing, switch methods — don't force the same one harder. The kitchen frame: prep your ingredients → pick the method → taste as you go → finish by hand if needed → bank the winning method as a recipe.

## 1 · The 8 foundations — how the models actually behave

1. **Small Steps Law** — never ask for one big jump. A "jump" is the delta between what your inputs already show and what you're asking for. Big jumps fail in random, hard-to-debug ways. Every technique below turns one big jump into small, checked steps.
2. **Words are the strongest input** — text-to-image is the highest-fidelity path when the thing is describable. A reference photo is a crutch for what words can't capture; it also takes word-level control away (you can't edit pixels the way you edit a sentence). Before attaching a reference, ask: "could I just describe this?"
3. **Say it or show it, never both** — an ingredient is defined by words, by an image, or by both — never redundantly. Don't describe what an attached image already shows: anywhere your words differ from the pixels, even slightly, the two signals fight and pull the output away from the reference. Words for what you want to CHANGE, pictures for what you want to KEEP.
4. **The source beats the prompt** — a reference communicates *everything* it contains, including noise. A face in a background photo will appear in the output even if the prompt never mentions it. Crop every source to exactly what you want transferred; never use a source that contains a competing version of what you're adding (the Polluted Source Rule).
5. **Attention: first = loudest** — image models pay more attention to earlier tokens. This is not a bug, it's how they're built. Default order is Style → Subject → Action → Scene → Camera → Brand; break that order when one ingredient isn't landing and move it toward the front. A detail that keeps getting lost can be repeated from three different angles (subject, scene, brand line) — the repetition trick.
6. **Dimension blindness** — the model learned from photographs, and photographs never carried a ruler. It understands relative *magnitude*, never centimeters. Write "a 5cm border" and you might get one four times too big. Centimeters don't steer, they coast — they only look accurate when the requested size happens to match the object's typical size.
7. **Batch economics** — the discard pile is the quality filter doing its job. A generation is rarely perfect even with the right prompt; plan for variations, not one-shots, and let the client only ever see what passed.
8. **The prompt is the asset, not the image** — "the image is the echo; the prompt is the voice." A perfect prompt is complete, precise, and leaves no room for interpretation. When an image is wrong, the answer is in the prompt, not in painting over the picture. A prompt that wins becomes a **master**: the North Star for the whole series, edited surgically (swap only the changed clause) and never rewritten from scratch — you don't know which word was doing the heavy lifting.

## 2 · Visual Syntax — the language of an image, 6 ingredients

Every image decomposes into six ingredients, in this canonical order (front = loudest, per foundation 5):

| # | Ingredient | The question | Words or image? |
|---|-----------|---------------|------------------|
| 1 | **Style** | What kind of photo is this? | Either — colors everything downstream |
| 2 | **Subject** | What/who is the hero? | Image, for the product — accuracy needs pixels |
| 3 | **Action** | What's happening? | Either |
| 4 | **Scene** | Where are we, how's it lit? | Either |
| 5 | **Camera** | How is it shot? | Text — hard to show, easy to say (lens/aperture/framing) |
| 6 | **Brand** | How does this feel like the brand? | Text — colors and vibes rarely transfer from a reference image; acts as a filter over the whole image, not a dominant force |

Three rules fall out of this: (1) every image has these six slots, decompose and control each one; (2) each slot is words, an image, or both; (3) order matters — earlier ingredients dominate.

**What clients actually buy: Conversion Integrity** = Accuracy (physical truth of the product) + Realism (passes the sniff test) + Branding (speaks the brand's visual language). Miss any one and the image can hurt the brand.

**Quality gate**: score all six ingredients 1-5. Any ingredient below 4 kills the image for product-detail-page work; ads/social can accept 3.5+ on some ingredients. A gorgeous scene around a wrong product still scores low on Subject — it does not ship.

## 3 · The technique families — WHEN to reach for each

Full write-ups with prompt skeletons and field-proven wins are in `references/techniques.md`. Summary, grouped by what problem they solve:

**Source preparation** (fix the input before you ever touch the prompt — the cheapest, highest-leverage stage)
- **Clean Reference** — good light, neutral background, crop to keep only what you want transferred, upscale to ≥2K, angle-match the source to the intended output. The single biggest accuracy lever measured: the same task went from 0% to 75% strict fidelity just by swapping a blurry reference for a sharp one.
- **Angle Bank** — capture ~10 angles around a product's 360° axis once, in good light, clean background. This is the upstream unlock that makes the highest-accuracy technique (Lock-and-Outpaint, below) always available later. For shape-adaptive products (bedding, apparel) this generalizes to canonical states × angles, not just angles of a rigid object.
- **Clean Ingredients** — one clean, isolated master per ingredient in a shot (model, product, background, prop) — composite only from masters, never from styled sources.
- **Comp Card Technique** — for synthetic/repeat models: a styled comp card for choosing the look, a plain white-background/white-shirt clean portrait for actually compositing (the source always wins over the prompt, so anything in a styled source pollutes the output).
- **Stand-In Technique** — when you have the physical product but no photo of the pose/state you need: photograph anyone (yourself, a friend) holding or wearing it purely as a fit/pose reference; identity comes from elsewhere.

**Transfer** (borrow what already works instead of describing it)
- **Product / Style / Composition / Template-one-liner Transfer** — attach a reference and say what to copy from it: its product, its look, its arrangement, or (rarest, most powerful) everything at once. "Use the same composition as [image1]" replaces trying to dictate a whole layout in words.
- **Composition Transfer, 4-image form** — the hardest shot (a specific person wearing a specific product with true proportions) separates into four single-job images: fit reference, identity reference, setting reference, design reference. One image, one job — never let one reference carry two.

**Decomposition** (break a complex ask into small checked steps)
- **Sequential Pipeline** — the *planned* build order for known-complex shots: select ingredients → composite subject+product → place into scene → apply style/action → quality check. Validate at each gate before moving on; a mistake carried forward poisons everything after it.
- **Shannon Descent** — the *diagnostic* version, for when something already broke and you don't know what's wrong: strip away everything except the smallest piece that still fails, perfect it alone, then rebuild the scene around the solved anchor.

**Locking** (freeze what must not drift)
- **Lock-and-Outpaint** — keep the product's pixels frozen exactly in place and generate only the world around it. Never redrawn = never wrong = zero drift. The highest-accuracy route there is, but it demands an angle-matched source — which is exactly what an Angle Bank supplies.
- **Placeholder-and-Replace** — the post-hoc lock. Measured on nano-banana-class editors: a "locked" region is an anchor, not a freeze — the model re-renders it (a frame came back 25% undersized; a projected railing came back rebuilt). So flip the order: generate the world around a flat, featureless *placeholder* with the product's footprint, then composite the true product deterministically afterwards (behind-content edit for see-through, supersampled warp, luminance transfer from the placeholder, occlusion restore from a row-median background model). The product pixels never enter a model. For parametric products the angle-matched source is synthesized from a camera model (geometry-first: 3D guide → model dresses the scene → faces solved with a self-calibrated focal from two-face orthogonality). Freeform AI scenes at strong angles are painted, not projected — don't fit them; seed them. **Subtractive form** when the surface is a rendering problem but the geometry is data: generate the product blank in its real material, then cut the exact holes/print out of it — replace as little as accuracy requires (a synthetic shader lit by a matte placeholder reads as paper).
- **Blueprinting** — lock a scene in *words* instead of pixels: have the model describe the image so completely the description alone could recreate it, delete only the sentences describing the thing you're replacing (leave every other sentence exactly as-is), then regenerate with the new element filling the hole. Also escapes a low-resolution source ceiling, since you're regenerating from a fresh description, not the old pixels.

**Iteration** (learn something from every generation)
- **Control vs Variant Pipeline** — lock an immutable Control Base (composition, camera, layout), then test one isolated change at a time as a variant, keep what scores better, fold winners into a new champion. This is prompt engineering as version control; it avoids the failure mode of rewriting whole prompts (semantic leaking — the layout shifts when you only meant to change a texture).
- **Micro-Iterations** — the lightweight, in-session version: once you've found the ONE word that's failing, generate 10-15 variants of just that word/phrase ("oval" → "elongated oval" → "narrow oval"...) and expect 2-3 to land.
- **Draft Cheap, Finish Expensive** — two dials, turned up only as confidence rises: variation count (1 image while exploring an unproven direction; 3-10 once the direction is locked and you're picking the best of a litter) and model tier (cheap/fast model for drafts, premium/high-resolution model for the final render). Never one-shot at full price; never ship at draft quality.

**Wording** (speak the model's language)
- **Material Fidelity** — translate what the client means into words the model has seen a million times: material analogies over the client's own jargon ("grooves pressed like a linocut print" beats "engraved the way we want"), forbid-by-name exclusions, real film-stock/camera names over vague adjectives ("vintage look"), and a client glossary collected before generating. See §4 for the measured prior-test rule.
- **Dimension Control** — see §4 for the measured decision rule; the tools are a magnitude ladder, comparison anchoring to ONE clean singular landmark, shout-and-forbid (capitals + name the blocked mistake), and sketching a position words can't carry.
- **AI Realism Techniques** — kill the plastic look with small stacked physical cues, tested one at a time: visible pores/imperfections, real camera and lens names, banned words (perfect, flawless, airbrushed, porcelain — these trigger the CGI look), volume-controlled emotion words ("quiet joy" not "happy"). Realism is a collection of small physical cues stacked together, never one heavy effect — and each cue must be verified to actually help before you keep it.
- **Edit Grammar** — editing an existing image is a different grammar from creating one: describe the CHANGE, not the picture — a work order, not a wish. Formula: **Action + Target + Integration**. Action = the verb (remove/replace/add/overlay/extend). Target = the exact thing plus which reference image supplies it. Integration = how it blends — matched light direction, matched color, texture that bends with the surface, matched perspective. The integration line is the entire difference between an amateur and a professional edit.

**Judging** (verification is a technique family, not just a gate)
- 6-Ingredient Scorecard (1-5 per ingredient, 4-star minimum to ship for product-detail work).
- 8-axis fidelity check: silhouette/outline, proportions/scale, element count, text/typography, graphics/pattern, material/finish, color accuracy, construction details. Score each match / off / not-visible against the real reference.
- Upload the generated image alongside the original product photo to a vision model and ask directly: does this match proportions and dimensions? Any accuracy issues?
- Side-by-side diffing: compare a variant against its control, or a generated image against the real factory photo, like a code review.
- **Scale Audit (natural rulers)** — prove the render kept the product's true SIZE: anchor-free ratio checks first (aspect, internal proportions — no assumptions needed), then find an in-frame object of known low-variance real size (iris 11.7mm on a face; a brick, door, outlet, credit card in scenes — manufactured beats biological), measure both in pixels (color-mask bbox exact, grid-overlay ±10%), compute implied product size vs ground truth. Catches the silent 20–30% regression-to-typical-size the eye forgives; the % error doubles as the correction factor for the re-lock. For periodic patterns also verify the manufacturing rapport by autocorrelation (a stamped pattern repeats; a random scatter doesn't, and reads "too random").

**Manual Handoff** (know when the machine is done)
- The sign of a true wall: two full techniques exhausted, the same defect keeps returning, and each new attempt breaks something else. The fix has one shape: AI builds 90% of the image; the last 10% of truth is applied by hand in an editor from the real photo (cloning real fabric folds, placing real illustration/lettering elements, matching color to the brand's real swatches). Always a **proposal with evidence** (attempts made, the stubborn defect, the recommended manual fix) — never a silent give-up. Write the manual recipe down: "impossible" shrinks every year.

## 4 · The Route Map — diagnosis → technique

Taste first (name what's wrong), then pick ONE technique and commit. Never technique-hop randomly.

| What's happening | The move |
|---|---|
| The ask is one small step from what you have | One-shot prompt (Visual Syntax); a template one-liner if a reference has the exact look already |
| You know WHICH thing is wrong | Control vs Variant Pipeline (+ Micro-Iterations on the one failing word) |
| Product needs an angle/pose your photo doesn't show | Pose-Match: transform the ingredient first, one step, check it, save the angle forever |
| Details mushy, reference weak, nothing improves | Clean Reference first (fix the input); bigger output; switch models. No usable photo at all → Stand-In Technique |
| You don't know what's wrong, or the whole scene defeats every fix | Shannon Descent — isolate the smallest failing piece |
| The product can be fully described in words / building a master prompt | Describe first (text-to-image), or Blueprinting for a full scene rebuild |
| A scene must be rebuilt around one replaced thing | Blueprinting |
| Product-on-surface, pixel-perfect fidelity, fixed angle | Lock-and-Outpaint |
| Parametric / data-described product, see-through product, or any re-render unacceptable | Placeholder-and-Replace (post-hoc lock) |
| The shot needs an angle you can't photograph, product is parametric | Geometry-first: 3D guide → dress → solve faces → Placeholder-and-Replace |
| Surface is a rendering problem (metal, gloss, glass) but geometry is data | Subtractive Placeholder-and-Replace: model renders the blank material, we cut the holes/print |
| A perfect layout already exists; fit + identity + design all matter at once | Composition Transfer |
| Output keeps copying the WRONG thing from a reference | Polluted source — clean it |
| Changing an existing image, not creating one | Edit Grammar |
| Person + product + scene all at once | Sequential Pipeline |
| SIZE or proportions are wrong | Dimension Control |
| Product *looks* right but you can't prove the size is | Scale Audit — anchor-free ratios first, then a natural ruler |
| MATERIAL reads wrong | Material Fidelity (+ Realism Stack if it also looks synthetic) |
| Still testing direction / choosing the final | Draft Cheap, Finish Expensive |
| Two techniques exhausted, defect persists | Manual Handoff |

## 5 · Measured rules (from controlled evals — see `references/evals.md` for the full numbers and honest caveats)

These override intuition where they conflict with it:

- **One-jump default**: with a SHARP reference, one generation step beats a chain of transformations decisively (100% vs 25% pass rate in controlled testing) — every extra step re-renders the product and accumulates drift. Chain only for asks a single edit genuinely cannot do (an angle that must be created first). The input, not the method, is usually the real bottleneck — check reference sharpness before blaming the technique.
- **The dimension decision rule**: for a normal-sized ask, use number + one clean singular comparison with a landmark, and *leave out* the magnitude word (it overshoots on normal sizes). For a weird/unusual size, you need the magnitude word. If unsure, stack all three (number, comparison, magnitude) — it's never catastrophic. Never trust centimeters alone. A hand or a row of objects is a bad anchor; ONE clean singular object plus a landmark phrase works.
- **The material prior test**: before writing texture words, ask what the model *already* thinks that material looks like by default. Correct prior (the real name matches expectations) — naming it is enough, extra words add nothing. Wrong prior (the model's default clashes with reality, e.g. plain white percale defaulting to smooth) — no amount of wording crosses it; get a texture reference or plan a manual finish instead. Ambiguous prior (the material genuinely has more than one common look, e.g. leather) — this is the only case where adjectives earn their keep.
- **Word-order / position rule**: the identical clause is roughly 2.5-3× more accurate as the FIRST sentence of a prompt than buried later — and the MIDDLE is the worst position of all (an instruction embedded inside scene description dilutes more than putting it dead last). Put the critical constraint first, then the scene.
- **The variation ladder**: plan 3-6 variations for an easy, well-understood task; up to 10 for a borderline or fussy one. Generating 3 and keeping the best measurably raises the pass rate over generating 1. If you need more than ~10 attempts on the same prompt, the prompt — not the dice — is the problem; switch technique via the Route Map.
- **Verify the verifier (measured)**: an audit tuned on one material can be blind on another — dark-blob hole detection under-read bright see-through holes on lit metal while the pattern was exact by construction. Re-validate the instrument on a known-true image whenever material/lighting/resolution changes; report "unmeasured" over a false pass.
- **The lock is an anchor, not a freeze (measured)**: current nano-banana-class editors re-render "locked" pixels — twice measured (eyewear frame −25% scale; balustrade guide rebuilt at the model's own size). Lock-and-Outpaint as literally described only holds on mask-respecting inpaint models; otherwise use Placeholder-and-Replace. Corollary: a freeform AI scene is not projectively consistent (equal-panel fit residual floor ≈9% of face length in a test) — at strong angles, seed the scene from your own geometry instead of fitting the model's.
- **The Angle Bank**: capturing ~10 angles of a physical product once (or, for soft goods, canonical states × angles) is the single highest-leverage move available at capture time — it is the precondition that makes Lock-and-Outpaint, the highest-accuracy technique, available for every future request forever. Two minutes of capture buys years of accuracy.

## How to use this skill in practice

1. Get the brief and the client's real product photos. If the physical product is available, ask for an Angle Bank (~10 angles, good light, clean background) before generating anything — it is the cheapest fix available and it's permanent.
2. Prepare the source: crop to what you want to keep, upscale, angle-match to the intended composition.
3. Try text-to-image first if the shot is fully describable (foundation 2). Otherwise assemble the six Visual Syntax ingredients, front-loading whatever is unusual or hard to land.
4. Generate 1 image while exploring direction; once the direction is right, generate a small batch (§3 variation ladder) and keep the best.
5. Judge against the real product: 8-axis check, 6-ingredient scorecard, 4-star minimum. If something specific is wrong, diagnose which axis it is and route to the matching technique (§4) rather than regenerating blindly.
6. If two techniques get exhausted and the same defect returns, propose a manual finish with evidence rather than shipping a defect.
7. Save what worked: the winning prompt is the asset. Reuse it verbatim for the next shot in the series; edit only the clause that needs to change.

For prompt-language detail (exact style/camera/lighting/model/category/brand phrasing) see `references/cheatsheets.md`. For the technique library at full depth with worked examples see `references/techniques.md`. For the measured numbers behind §5 see `references/evals.md`.
