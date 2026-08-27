# The Technique Library — full depth

Based on the AI product photography accuracy doctrine by Bertrand / dezygn.com. This is the technique layer behind `SKILL.md` §3-4: every family, expanded with the reasoning, the prompt patterns, and the field wins that proved each one.

Organizing principle: **there are many ways to cook the same dish.** The dish is the target image; each technique is a way to cook it. When one way keeps failing, switch methods — don't force the same one harder. Prep your ingredients (source preparation) → pick the method → taste as you go (judging) → finish by hand what the method can't reach (manual handoff) → and when a method works, write it down as a recipe and reuse it verbatim.

The unifying law underneath every technique: **never ask the AI to make a big jump in one step.** A "jump" is the distance between what your inputs already show and what you're asking for. Big jumps fail in random ways that are hard to debug. Every technique below exists to turn one big jump into several small, checked steps.

---

## Source Preparation

### Clean Reference

The number-one source-preparation technique. A reference communicates *everything* it contains — a busy or weak reference makes the model guess, and it guesses wrong in ways you can't predict. Cleanliness happens in two stages:

**At capture (upstream — the cheapest fixes happen here).** Good even lighting, a white or neutral background, the small details (text, hinges, seams) sharp and large enough in frame to read clearly. If it's blurry to you, it will be worse in the output — resolution problems compound downstream, they never resolve themselves.

**Downstream prep (before the model ever sees it).**
- Crop to keep only what you want transferred — if you're not trying to keep it, remove it. Ten seconds of cropping beats an hour of prompting.
- Upscale: source should be ≥2000px on the long edge; any critical text should render ≥100px tall (120-160px is the comfortable range). Output resolution should be ≥ input resolution — a 2K source rendered into a 1K output is blurry garbage no matter how good the prompt is.
- Strip noise: remove props, other people, hands, distracting backgrounds. Never use a source that contains a competing version of what you're adding (the Polluted Source Rule — a model already wearing glasses is not a glasses reference).
- Angle-match: pick the source whose angle matches your intended composition. Every degree off is something the model has to invent, and it invents wrong. If the exact angle doesn't exist yet, create it (see Pose-Match) and save it permanently.
- Aspect-match: crop the reference to the output's aspect ratio so the model isn't forced to invent what's outside the frame.

This is measurably the single biggest accuracy lever available. In controlled testing, the identical task went from 0% strict fidelity with a blurry reference to 75% with a sharp one — before any other technique was touched. Fix the input before you touch the prompt.

### Angle Bank

**"There is a huge amount of leverage at the image capture stage."** The reasoning chain:

1. Pure text-to-image is the ideal accuracy path (words are the strongest input) — but human language has real limits. Complex mechanisms and precise geometry are genuinely hard to fully describe.
2. So the next-best accuracy path is Lock-and-Outpaint (below) — the product's pixels are never redrawn, so they can't drift.
3. But Lock-and-Outpaint demands an angle-matched source: a three-quarter output needs a three-quarter-view source. The method is only as available as your angle coverage.
4. Hence the capture-stage unlock: if you have physical access to the product, **shoot an Angle Bank** — a multi-angle set around the full 360° axis, at least ~10 angles, captured once in good even light against a clean background. That single capture session guarantees high-accuracy production for every future composition, forever. Two minutes of capture buys years of accuracy.

Missing angles can be synthesized after the fact (see Pose-Match) — but with a hard caveat: **the model doesn't know what it doesn't know.** Ask it for the back of a product it has never seen, and it won't decline — it will invent a back, confidently and wrong. Synthesized angles are trustworthy only for geometry the existing sources already imply, and every synthesized angle should be checked against reality before it's trusted as a permanent asset.

**Capture tiers by budget**: a phone-only protocol (10 angles, daylight, clean background, free) covers small businesses and freelancer clients; a turntable + fixed camera + consistent light gives repeatable, evenly-spaced angles for a small studio; a full photogrammetry / 3D scan gives a precise ground-truth model that can render any angle at all — this fully solves "the model doesn't know the back," because the scan *is* the back.

**A practical capture list**: front, back, left, right, both front three-quarters, both back three-quarters, top, plus tight close-ups of every piece of text, logo, or hardware detail.

**Shape-adaptive products** (bedding, apparel, drape) don't have one fixed geometry, so the bank generalizes from *angles of a rigid object* to **canonical states × angles** — e.g. for bedding: made-bed front, made-bed sides, a folded stack, a draped detail shot, plus texture close-ups (which double as the material-prior reference the material-fidelity work below calls for).

### Clean Ingredients

Every ingredient in a shot — model, product, background, any prop — gets ONE clean, isolated master, and you composite only from the masters, never from a styled or busy source. A shot with two models, a product, and a background needs four clean masters, not two.

- **Model** → a clean portrait: plain background, plain shirt, no accessories.
- **Product** → an isolated packshot on white, with every key angle saved as a permanent asset.
- **Scene/background** → the empty stage, approved with nothing in it yet.
- **Any other element** (logo, illustration, prop) → isolated on a neutral background at the correct resolution.

Why this matters: the source always beats the prompt. Anything present in a styled source — clothing, an old accessory, a busy background — pollutes every composite made from it. A single comp card with sunglasses visible in a corner panel once cost hours of failed prompting, purely because composited new glasses kept landing where the panel's sunglasses had been; a clean portrait fixed it on the first try. The masters are permanent assets — name them, tag them, and reuse them across every future job.

### Comp Card Technique (synthetic model consistency)

For a synthetic model that needs to recur across many shots, keep two distinct assets, not one:

- **The comp card** — a grid of poses, on a white/grey background, plain white tee, no accessories, multiple angles. Its only job is helping you *choose* the model. Never composite from it directly.
- **The clean portrait** — the single version you actually composite from every time.

This is the general one-clean-master-per-ingredient rule, specialized for people. Because the source always wins over the prompt, any clothing, background, or accessory visible in a comp card will bleed into anything composited from it. The fix cost real time to learn: comp cards shown fully dressed against busy backgrounds wasted hours before stripping them down to white-tee-on-white-background solved it in one pass.

**Model realism cues worth stacking**: 3-4 stacked facial features (shape + chin + cheekbones + eyes + lips — single descriptors alone produce generic faces); the word "youthful" when you need an accurate young age (without it, 20-year-olds tend to render 28+); explicitly negate default stubble ("clean-shaven") for male models unless you want a beard; volume-controlled emotion words ("quiet joy", "subtle smile") rather than raw emotion words; anti-plastic cues ("natural skin texture with visible pores", "slight facial asymmetry", "authentic, unretouched appearance").

Clients react to synthetic models like casting calls — expect rejection and iteration rounds on the model itself before locking one in, then only comp-card the winner.

### Stand-In Technique

The camera route for creating a missing reference (its siblings: Pose-Match is the AI route, sketching is the drawn route — pick by what you're holding: a physical product → stand-in; only photos → pose-match; neither → sketch). Also useful as a recovery move when nothing else improves and no usable photo exists at all.

When you have the physical product but no photo of the *state* you need (worn on a face, half-folded, tilted just so, several items arranged together): photograph anyone — yourself, a friend, anyone available — wearing, holding, or arranging the product, and use that photo purely as a FIT/POSE reference. Proportions, scale, and position come from this photo; identity comes from somewhere else entirely. It also works product-only: fold or tilt the product yourself and shoot that arrangement as the reference the model didn't have.

**Precondition**: someone has to actually hold the physical product — often that's the client, not you. If nobody can take that photo, fall back to Lock-and-Outpaint, reuse a proven prompt from a similar past job, or generate-and-confirm the missing reference instead of asking for an impossible stand-in shot.

**The 4-image role assignment** (the advanced version — rendering a specific model wearing a specific product accurately):

| Slot | Role | Extracts |
|---|---|---|
| image 1 | Real person wearing the product | FIT — proportions, product-to-face/body ratio, where it actually sits |
| image 2 | The model's clean portrait | IDENTITY — whose face to render |
| image 3 | An environment photo | SETTING |
| image 4 | Product alone on white | DESIGN — exact shape, materials, details |

This works because it separates concerns: fit and design are different information, and naming an explicit identity anchor ("render this person's face") prevents identity-blending between two source images. Tight, close-up framing forces the model to prioritize the product-to-body relationship correctly.

---

## Transfer — borrow what already works

The family of moves that copy an existing reference instead of describing it in words. All obey the golden rule: don't describe what a reference already shows, and give every attached image exactly one job.

- **Product Transfer** — attach the actual product photo; the model recreates it in a new scene. The bread-and-butter move — always feed it a properly Clean Reference.
- **Style Transfer** — attach an aesthetic reference: "using [image1] as the aesthetic template, recreate [image2] in the same studio product photography style." One sentence replaces seventy-plus words of style description.
- **Composition Transfer** — borrow the layout, pose, or framing: "use the same composition as [image1]." Described in full below — it's the deepest technique in the family.
- **Template One-Liner / Full Transfer** — when a single reference already has exactly the look you want, wholesale: the one-sentence prompt IS the whole prompt. The reference carries the look, your product photo carries the product, and your words name only what should differ. The most powerful of the transfer techniques, but also the trickiest — get it wrong and everything drifts at once.

Decision guide: what do you actually want from the reference? Its product → Product Transfer. Its look → Style Transfer. Its arrangement → Composition Transfer. Everything at once → Template One-Liner.

### Composition Transfer, in depth

Describing a composition in words is nearly impossible — try dictating exactly where every arm, object, and shadow sits in a scene. So don't describe it: attach the picture with the perfect pose, framing, or arrangement, and say the magic line — **"use the same composition as [image1]"** — then attach your own product as a second image to supply the content. The layout image carries the arrangement; your product image carries the product; your words carry only the surrounding context. Even an imperfect transfer beats trying to describe a layout in words. Don't describe a pose — show one.

**The general law underneath it: one image, one job.** Never let a single reference serve two purposes at once — a double-duty reference produces corrupted results because the model can't tell which aspects of it to keep and which to ignore. Name each image's job out loud in the prompt: "the product from [image1], the same pose as [image2], a place like [image3]."

**The four-image worn-product form** handles the hardest recurring shot in the trade — a specific person wearing a specific product with true proportions. It typically fails three ways (the product renders oversized, faces blend between two people, or fine design details get lost), and the root cause is almost always one image doing two jobs at once. The cure is total separation into four single-job slots: a real photo of someone wearing the product (FIT), the model's clean portrait (IDENTITY), a photo of the setting (SETTING), and the product alone on white (DESIGN). Say whose face out loud ("draw this person's face") to prevent face-blending, and frame close-ups tightly so proportions have less room to drift.

When to reach for this: a perfect layout already exists somewhere; a client says "I want something like this"; a whole product line needs identical framing; or fit, identity, and design all matter simultaneously. A real photo of a similar arrangement, used purely as a spatial-layout reference, has repeatedly solved spatial-reasoning problems that hours of pure text prompting could not.

---

## Decomposition — small, checked steps

### Sequential Pipeline

"Complex images aren't one problem. They're five sequential problems." One-shot generation collapses for anything with real complexity — a person plus a product plus a scene plus a style, all at once. Each step should instead produce a **validated intermediate asset** before the next step begins:

1. Select your ingredients (clean portrait, clean packshot, scene, style references).
2. Composite subject + product only — validate accuracy at this gate before anything else touches the image.
3. Place the validated composite into the scene.
4. Apply style and action.
5. Run the full quality check (6-Ingredient Scorecard, 4-Star Rule).

**The gate discipline**: at every step, stop and ask — is the product right? Is the fit right? Is the face right? Fix it HERE. A mistake carried forward poisons everything generated after it, exactly the way no real photographer sets up model, product, lighting, and full set all at once for a single exposure. Skip the composite step for genuinely simple products (a t-shirt, a bottle); do it religiously for eyewear, jewelry, transparent materials, and any small branded detail. Run each stage in its own session where possible — context bleeds between stages and pollutes them.

Trying to merge everything (scene + model + product) into one shot in one pass, for a genuinely complex product, has repeatedly wasted many hours where a properly staged pipeline shipped in a fraction of the time.

### Shannon Descent

**Shrink the problem until it can't hide.** Use this when you don't know what's failing, or when every fix inside the full scene fails anyway. Throw away everything except the smallest piece that still fails, perfect it completely in isolation, then rebuild the scene around that solved anchor — checking that it survives each addition.

Why it works: a complex scene is a crowd of instructions competing for the model's limited attention. The one detail you actually care about may be getting too small a share of that attention. Isolated on its own, the model pours all of its attention into it, and you can finally see clearly whether it's actually right.

You can shrink surprisingly far — down to a single element, or even down to a single instruction inside the prompt. Classic example: lettering renders wrong in every composite → generate the lettering alone on white in its true material, perfect it there, then composite the solved piece in. It also works in reverse: build the empty room first, get it approved empty, then place the product into the approved space.

This is the *diagnostic* sibling of the Sequential Pipeline — the pipeline is the planned build order for a shot you already know is complex; Shannon Descent is what you reach for when something has already broken and you don't yet know why.

---

## Locking — zero drift, in pixels or in words

### Lock-and-Outpaint

**The highest-accuracy route there is.** Keep the product image pixel-locked exactly in place, and outpaint only the environment around it: "keep [product] in exact original position, crop, zoom, and angle — do not regenerate, alter, or reprocess the product itself. Outpaint the surroundings only." The logic is simple: every time a model redraws a product, something can drift. Never redrawn means never wrong means zero drift. The only thing you're asking the model to do is blend the *light* onto a locked, untouched product. From one frozen studio shot you can produce a whole series — the same untouched product placed on wood, silk, concrete, leather, whatever the scene calls for.

**Prompt skeleton**:
1. Lock clause — exact position/crop/angle, stated explicitly as "completely unchanged, do not regenerate."
2. Outpaint clause — the surface or environment description, plus any camera repositioning needed.
3. Integration clause — lighting direction and color temperature matched to the locked product, with realistic contact shadows.
4. Optional realism layer — vignette, grain, dynamic range (see the Realism Stack below).

Best used for product-only shots where the packshot's existing angle already matches the target composition — the angle-match rule still applies here as much as anywhere. This is precisely why the Angle Bank matters: it's the upstream capture practice that keeps a matching angle-locked source always available.

### Blueprinting

**Lock the image in words instead of in pixels.** Pixels are hard to edit; words are easy to edit — so convert, edit, regenerate:

1. **Draw the blueprint** — ask the model to describe the existing image so completely that the description alone could recreate it. Use a numbered-entity style for anything with duplicates ("woman 2… chair 3… decanter 2") — that's what makes the recreation controllable, because each entity can then be surgically edited on its own.
2. **Edit the blueprint** — delete only the sentences describing the thing you're replacing, and keep every other sentence exactly as written. You've now cut a hole shaped precisely like the old element.
3. **Regenerate** with the new element attached to fill that hole.

Bonus: the finished blueprint becomes a reusable master — one well-built description can carry a whole product line through the same scene, edited clause by clause for each new product.

Three uses worth knowing: **asset recreation** (cleanly replicate an illustration or pattern before applying it elsewhere); **upscaling a low-resolution source** by regenerating it from a fresh description, which escapes the resolution ceiling of the original pixels entirely; and **complex-scene rebuild**, recreating an entire scene as a long structured description, deliberately leaving out the one element you intend to replace, then attaching your own version of that element as an ingredient.

Use it when a scene must be rebuilt around one replaced thing, or when you need genuine word-level control over a layout that currently only exists as pixels.

---

## Iteration — learn something from every generation

### Control vs Variant Pipeline

Prompt engineering treated as version control. Lock an immutable **Control Base** — composition, camera, structural layout — and never edit it during the experiment. Test **isolated variants** one at a time, each a single appended change (a lens-physics tweak, a material-precision detail, a tonal adjustment), and score each one against the control as better, worse, or the same. Winners fold into a **new champion**; repeat. You stop gambling and start running small experiments, and every image teaches you something you keep.

This solves the specific failure mode of rewriting a whole prompt at once: token overcrowding, and **semantic leaking** — where a change meant to affect only texture accidentally shifts the whole layout, because the model can no longer tell which words are doing what.

**The three layers**:
1. **Control Base** — spatial geometry, camera, structural layout. Never touched mid-experiment.
2. **Variants** — one isolated change each: lens physics (vignette, chromatic aberration, sensor noise), material precision (tool marks, porosity, surface irregularity), tonal shifts (film grain, patina, ambient light bounce).
3. **Calibration Layer** — when stacking variants starts to dilute the intended style or palette, move the priority tokens back to the very front of the prompt (the attention rule in action).

A worked case tested nine realism variants one at a time against a locked control: vignette, chromatic edge, asymmetric exposure, non-uniform cast, and tonal range all helped; production marks / tool-mark detail helped most of all; porosity variation introduced artifacts and atmospheric dust proved invisible, so both were dropped. The consolidated winners became the new champion build. The general finding: **small physical cues stacked together consistently beat one single heavy stylistic effect.**

Use this when your prompt is almost working and you already know — or strongly suspect — which single thing is wrong.

### Micro-Iterations

When one specific detail won't render correctly, don't retry the identical prompt and hope — vary ONLY the language describing that one problem area, while holding everything else completely stable. Run 10-15 small variants; expect 2-3 to land. Example: narrow eyewear kept rendering too tall; varying only the shape descriptors ("oval" → "elongated oval" → "flattened oval" → "slim oval", plus an explicit height constraint) surfaced the versions that finally held.

The framing that makes this useful: generation is a dice roll, so once you've found the ONE word that's failing, roll many dice all aimed at that single word rather than at the whole prompt. This is the lightweight, in-session version of the Control vs Variant Pipeline — the same idea, without the formal locked baseline and scored experiment matrix.

### Draft Cheap, Finish Expensive

Two dials on one axis: how sure are you of the direction? Turn both up only as confidence rises.

**Dial 1 — variation count.** While exploring an unproven idea, composition, or direction: generate ONE image at a time. Extra copies of an unproven idea are pure waste. Once the direction is locked and you're just choosing the final: generate a batch of the winning prompt and pick the best of the litter.

**The variation ladder**: one generation is rarely perfect even when the prompt is exactly right — the same prompt with different draws produces only some keepers. Scale expected variation count to task difficulty: **3-6 variations for an easy, well-understood task; up to ~10 for a borderline or fussy one.** If you find yourself needing more than ~10 attempts on the identical prompt, the prompt — not the dice — is the actual problem; switch technique instead of grinding the same one harder.

**Dial 2 — model tier.** Draft on a cheap, fast model while you're still deciding *what* to make at all — resolution doesn't matter yet. Switch to the premium, higher-resolution model only for the final render. The specific model names on this ladder change every six months; the principle doesn't.

Rule of thumb: never one-shot at full price, never ship at draft quality.

---

## Wording — speak the model's language

### Material Fidelity

Translate what the client means into words the model has actually seen a million times in training. The model knows the physical world only through its training photos — the exact same real-world idea lands or misses entirely depending on which words describe it.

**The six moves**:
1. **Material analogies** — describe a finish as a famous craft or process, not the client's own jargon: "engraved the way we want" becomes "grooves pressed like a linocut print, filled with matte enamel." A phrasing breakthrough of exactly this shape once solved a stubborn engraving job that adjectives alone couldn't touch.
2. **Forbid by name** — every named exclusion closes a door the model would otherwise wander through: "no sheen, no shine, no satin gloss; not slubby, not textured like linen."
3. **Real names beat adjectives** — a real film stock beats "vintage look"; a real camera-and-lens combination beats "professional photo."
4. **Build the client glossary first** — collect the client's own precise technical vocabulary before generating anything. Those exact terms are what distinguish THE product from something merely similar to it.
5. **Hunt the one wrong word** — when an image is almost right, don't rewrite the whole prompt. Ask which near-twin word is actually wrong (engrave, emboss, and intaglio each pull a different physical shape) — then burst that one word with Micro-Iterations.
6. **Steal proven wording** — a phrase that has already worked gets reused whole, verbatim, in future prompts. You don't reliably know which word was doing the load-bearing work, so don't risk losing it by paraphrasing.

See `references/evals.md` for the measured "material prior" rule this whole technique now answers to — words genuinely can't cross every prior, and knowing which kind of prior you're facing tells you whether to keep writing or to stop and get a texture reference instead.

### Dimension Control

The technique kit for dimension blindness: the model learned from pictures, and pictures never carried a ruler. It knows relative magnitude, never centimeters. Write "a 5cm border" and you might get one four times too big. Five tools, used together:

1. **Magnitude ladder** — escalate the size word until reality matches: "small" → "very small" → "extremely small." Keep both the number (truth for the humans reading the prompt) and the winning word (the actual steering signal for the model) in the final version.
2. **Comparison anchoring** — chain the size to an object the model knows cold, with ONE clean singular anchor (not a hand, not a row of objects — see the measured findings in `references/evals.md`): "the lamp is the same width as the dinner plate beside it."
3. **Landmark anchoring** — use the body's own landmarks, or the product's own parts, as the ruler: "sits low on the face, the bottom of the lens just reaching mid-nose; the top rim clearly below the eyebrows, with a visible strip of skin between brow and frame." For an object beside furniture: "no taller than the books next to it."
4. **Shout and forbid** — capitals plus an explicitly named blocked mistake: "CRITICAL: only 4cm tall — NOT tall aviator-style frames."
5. **Sketch it** — when a position genuinely won't go into words, draw it. Even a rough sketch speaks the model's native visual language and has been measured to double the hit rate on a stubborn positioning problem.

See `references/evals.md` §Dimension Control for the exact decision rule these five tools now resolve into.

### AI Realism Techniques (the Realism Stack)

How to break the "that's obviously AI" tell, for people in particular:

- **Kill the plastic look**: "visible skin pores, subtle skin texture", "natural imperfections, slight uneven skin tone", "raw photo, unretouched".
- **Fine detail**: "peach fuzz on cheeks", "subtle blemishes, slight under-eye shadows", "natural skin sheen, slight perspiration".
- **Camera physics kills the CGI look**: real camera and lens names ("shot on Hasselblad X2D" or "Canon EOS R5" for editorial; "shot on iPhone 15 Pro" for UGC); real focal lengths (85mm portrait, 50mm, 105mm macro); "sharp focus on eyes, shallow depth of field, subtle film grain, realistic dynamic range."
- **Banned words**: "perfect skin, flawless, airbrushed, porcelain skin, hyper-realistic" all trigger the plastic/CGI look. Replace with "natural skin texture, subtle imperfections, unretouched, realistic."
- **Candid framing sells it further**: harsh direct flash, a slightly tilted horizon, motion blur at the edges of frame; real film stocks (Kodak Portra 400/800, Cinestill 800T) as physical carriers of the look.

**The master principle**: realism is a *collection of small physical cues stacked together*, not one heavy effect — and every cue must be tested one at a time via the Control vs Variant Pipeline, keeping only the ones that visibly help. When a client says an image "looks AI-generated — too uniform, too clean," that's the signal to run exactly this experiment: test vignette, chromatic aberration at the edges, asymmetric exposure, non-uniform light cast, surface tool-marks or grain, and light-source imperfections one at a time, keeping only what measurably helps.

**Deliberately imperfect light**: real light is uneven — "hotter near the entry point, falling off across the width" — and dual conflicting light sources (warm ambient light plus a flat flash) read as authentic precisely because they're unflattering. Perfectly even studio light is one of the tells that reads as synthetic.

### Edit Grammar — Action + Target + Integration

Two prompting modes exist, and mixing them makes mush. **Creating** describes the picture you want. **Editing** describes the CHANGE — write a work order, not a wish.

**Formula**: Action + Target + Integration.
1. **Action** — the verb: remove, replace, add, overlay, extend, recolor.
2. **Target** — the exact thing, with image roles named: "overlay the logo [image2] centered on the chest of the shirt [image1], at about 15% of the shirt's width."
3. **Integration** — how the change actually blends in: light (new shadows follow the scene's existing light direction), color (matches the scene's existing palette), texture (a logo bends with the fabric's wrinkles instead of floating flat on top), perspective (added objects follow the scene's existing vanishing lines).

"Add a coffee cup on the table" is an amateur edit. "Add a white ceramic cup on the wooden table, bottom right, lit from the upper left to match the existing shadows, with a soft reflection on the polished wood" is a professional one. **The integration line is the entire difference** between the two. Every specific edit type — removal, background replacement, object addition, attribute change, multi-image composition, relocation, resizing, outpainting — is a skeleton built on exactly this pattern. Lock-and-Outpaint, above, is outpainting perfected by this same grammar.

---

## Judging — verification as a technique, not just a gate

Evaluation deserves the same rigor as generation:

- **The 6-Ingredient Scorecard + 4-Star Gate** — score Style, Subject, Action, Scene, Camera, Brand each 1-5; ship only at 4+ on every one for product-detail-page work. A gorgeous scene wrapped around a wrong product scores low on Subject — it does not ship regardless of how good everything else looks. Ads and social content can sometimes accept 3.5+ on individual ingredients.
- **The 8-axis fidelity check** — a diagnostic rubric run as a formal check: silhouette/outline, proportions/scale, element count, text/typography, graphics/pattern, material/finish, color accuracy, construction details. Score each axis match / off / not-visible against the real reference.
- **LLM dimension verification** — upload the generated image alongside the original packshot to a vision model and ask directly: "Does the product match the proportions and dimensions of the original? Any accuracy issues?"
- **Side-by-side diffing** — compare a variant against its control the way you'd review a code diff; compare a generated image against the real factory photo for any client-facing proof shot.
- **The three quick checks** when time is short: product accuracy, human realism, brand fit.
- **The Scale Audit** — measure whether the render kept the product's true size; full write-up below.

### The Scale Audit — natural rulers

**Pairs with: Dimension Control (its verification counterpart).**

**The problem it solves.** Dimension blindness doesn't only corrupt inputs — it corrupts outputs, silently. The model learned every product category at its *typical* size, so a render drifts toward that typical size no matter what the reference showed: an oversized frame shrinks toward normal glasses, an unusually small bag grows toward normal bags. The eye half-notices ("it reads a bit less oversized than the product?") but can't prove it, so the image ships. The Scale Audit turns that feeling into a number.

The insight: **a photograph contains no ruler, but almost every photograph contains an object whose real size is already known.** Find it, and the whole image becomes measurable.

**The method:**

1. **Ground truth first.** Get the product's real measurements — caliper, spec sheet, the marking printed inside a temple arm. No ground truth, no audit.
2. **Run the anchor-free checks before anything else.** Aspect ratio (width ÷ height) and internal proportion ratios (bridge ÷ total width, handle ÷ bag height, logo ÷ panel) need **no ruler at all** — they compare the product only to itself, so they carry zero anchor uncertainty. These are your most trustworthy numbers and they catch shape drift the eye forgives: in the field case below, the variant that "looked fine" had flattened the lens height by 40%.
3. **Pick a natural ruler.** An in-frame object whose real-world size is known with **low variance across the population of that object**. That last clause is the whole skill of it — the ruler changes with the scene:

   | Scene contains… | Ruler | Real size | Variance |
   |---|---|---|---|
   | A face | **Iris diameter** | 11.7 mm | ±4% — the best biological ruler there is |
   | A face | Interpupillary distance | ~62 mm adult | ±6% |
   | A hand holding the product | Credit card, phone (if present) | 85.6 mm / model spec | ~0% — manufactured |
   | A room | Door height, outlet, light switch | 2030 mm / regional standard | very low |
   | A roof / façade | **Brick or tile** (regional standard format) | e.g. 215×65 mm UK brick | low — manufactured |
   | A kitchen / table | Wine bottle, soda can, A4 sheet | 300 mm / 66 mm ⌀ / 210×297 mm | ~0% — standardized |

   The ranking rule: **manufactured/standardized object > low-variance biological (iris) > high-variance biological (hands, face width, body height — avoid; they vary ±10%+ and you can't know which end of the range this person is on).** Two *independent* rulers agreeing upgrades a verdict from "likely" to "confirmed."
4. **Measure in pixels.** Two instruments:
   - **Color-mask bounding box** (programmatic): select the product's pixels by color rule, take the bbox — exact to ±2px. Calibrate in two passes: a *tight* mask to locate the product zone, then a *medium* mask restricted to that zone to measure — a single loose mask bleeds into hair/shadows, a single tight one misses thin dark parts. Both failure modes will happen; the two-pass split is the fix.
   - **Grid overlay** (visual): render the image with a labeled coordinate grid (lines every 10–25px, axis numbers drawn on) and *read* positions off it. This exists because a vision model can see but cannot measure — the grid converts seeing into reading. Use it for anything a color mask can't isolate: pupils, seam positions, soft edges. Accuracy ±10%.
5. **Compute.** `px-per-mm = ruler_px ÷ ruler_mm`, then `implied product size = product_px ÷ px-per-mm`, then `% error vs ground truth`.
6. **Verdict tiers — respect the noise floor.** Drift **>15%**: confirmed, reject or correct. **8–15%**: probable — bring in a second ruler before acting. **<8%**: below the instrument's resolution — pass; this gate catches the AI's characteristic 20–30% regression-to-typical, it cannot referee a 3% dispute.
7. **Close the loop.** The error is not just a grade, it's the correction factor. Rendered at 72% of true scale → re-lock the canvas with the product composited ~1.4× larger relative to the scene, and/or add a Dimension Control clause anchored to *the same ruler object the audit used* ("the frame is wider than her face — outer edges past her cheekbones"). Audit again after regenerating: the gate is only a gate if every variant passes through it.

**Field case (where this was discovered).** NOFILTER eyewear, 139×54 mm oversized frame (bridge 15 mm), lock-and-outpaint portrait on nano-banana-2-lite, 3 variants. Anchor-free check: the best variant's aspect came within **1.6%** of the real frame; another — visually acceptable — was **+40%** flattened. Scale audit on the winner: frame measured 361px; if size-true, the implied scale demanded a ~30px iris and ~161px IPD; measured ~40px and ~225px. Both rulers independently: **glasses rendered at ~72–75% of true size** — the model had quietly shrunk an oversized design to typical-glasses proportion. Invisible to the eye as a defect, decisive as a number.

The human eye remains the final instrument. Judge tooling raises the floor of what gets caught — it does not replace a good eye for detail.

---

## Manual Handoff — knowing when the machine is done

**Saying "the AI can't do this part" is itself a valuable output — it saves hours that would otherwise be spent fighting a wall.** The sign of a true wall: two full techniques have been exhausted, the same defect keeps returning, and each new attempt starts breaking OTHER parts of the image that were previously fine. The fix always has the same shape: **the AI builds the scene to about 90%; the last 10% of truth is applied by hand from the real photo**, in an image editor.

**Field-proven sub-methods**:
- **Texture/fold transplant** — clone-brush the real fabric's folds and texture from the factory photo directly onto the AI-generated image; blend modes, curves, and white balance adjustments bring it into agreement with the surrounding light.
- **Element extraction & placement** — select the real illustration or lettering from the source photo and place each instance by hand when a whole series needs to match perfectly.
- **Color matching** — direct swatch/Pantone matching, skin-tone correction, and bounded color adjustments against the brand's real reference colors.
- **Detail repair** — paint a softly blurred texture back in from the reference when the model keeps over-sharpening a detail that should stay soft; clean up small hallucinations (a misaligned screw, asymmetric hardware) by hand.

**Two rules govern this always**:
1. It is a **proposal with evidence** — "here are my attempts, here is the exact defect that won't resolve, here is the manual fix I recommend" — never a silent give-up.
2. Write the manual recipe down clearly enough that a future automated tool could eventually do it. What's "impossible" today shrinks every year, and the documented recipe is what lets you catch up the moment it stops being impossible.

If you're skilled at both graphic editing and AI generation, that combination is genuinely rare and valuable — most people are strong at only one half of this pipeline.
