# Reference Cheatsheets — the 80/20 libraries

Based on the AI product photography accuracy doctrine by Bertrand / dezygn.com. These are the fast-reference libraries for the six Visual Syntax ingredients (see `SKILL.md` §2): exact prompt language for Style, Camera, Scene/Lighting, Subject (people and products), and Brand. Pull from these directly when assembling a prompt rather than inventing phrasing from scratch — proven wording beats improvised wording.

---

## Style Reference — the 10 core styles

| # | Style | When to use | Prompt language |
|---|-------|-------------|-----------------|
| 1 | **Clean Catalog** (high-key bright) | E-commerce marketplaces, product-detail pages, maximum clarity | "Clean catalog product photography, white background, bright studio lighting, sharp focus, professional high-key" |
| 2 | **Lifestyle / UGC** | Instagram, TikTok, social ads, building trust | Lifestyle: "natural window light, authentic feel, real environment, candid moment." UGC: "authentic UGC photography, shot on iPhone, candid bathroom selfie, natural imperfect lighting" |
| 3 | **Luxury / Editorial** | Luxury beauty, hero images, campaigns | "Luxury editorial product photography, marble surface, gold accents, dramatic lighting, premium and sophisticated aesthetic" |
| 4 | **Minimalist / Scandinavian** | Design-forward, sustainable brands | "Minimalist Scandinavian product photography, pale gray background, lots of negative space, monochromatic, modern and clean" |
| 5 | **Moody / Dark** | Premium positioning, cinematic storytelling | "Moody product photography, dark charcoal background, dramatic directional lighting, high contrast, cinematic and mysterious" |
| 6 | **Vintage / Film** | Artisanal, heritage brands | "Vintage product photography, Kodak Portra film aesthetic, warm saturated tones, soft film grain, nostalgic 70s feel" |
| 7 | **Natural / Golden Hour** | Wellness, skincare, lifestyle | "Natural golden hour product photography by window, soft warm light, peaceful and organic atmosphere, warm natural tones" |
| 8 | **Flat Lay** | Social, storytelling, collections | "Flat lay product photography overhead, arranged with [props], marble surface, soft natural light, artistic composition" |
| 9 | **Macro / Detail** | Texture, quality, ingredient focus | "Macro product photography, extreme close-up showing texture, shallow depth of field, fine details, professional macro shot" |
| 10 | **Technical / Schematic** | Tech, supplements, clinical brands | "Technical product photography, neutral gray background, perfectly centered, multiple precise angles, clinical documentation style" |

**Vibe → purpose**: Clean Catalog = clarity/trust · Editorial = desire/aspiration · Lifestyle = context/relatability · UGC = authenticity/social proof · Moody = drama/premium · Minimalist = design/modern.

**By-shot-type defaults**

| Shot type | Style | Environment | Lighting | Action |
|-----------|-------|-------------|----------|--------|
| Packshot | Clean Catalog | White/neutral studio | Soft studio, even | None (product only) |
| Hero | Editorial or Moody | Studio or styled surface | Soft studio, dramatic | Static display, maybe floating |
| Lifestyle | Lifestyle / Natural | Real-world location | Natural window or golden hour | Active use, natural moment |
| UGC | UGC | Home, bathroom, casual | Natural, "imperfect" | Candid, caught in the moment |
| Catalog | Clean Catalog | Clean studio | Soft studio, uniform | None |

**Common style mistakes**: no style specified at all (what you don't choose, the model chooses for you, and it chooses generic); mixing incompatible styles ("UGC bathroom selfie with dramatic studio lighting" doesn't exist in nature); over-describing style with a pile of adjectives when a few precise words would beat it.

---

## Camera Reference — ingredient 5

The 80/20 when unsure: **85mm, f/4, three-quarter angle, soft studio.**

**Winning combos**

| Goal | Recipe |
|------|--------|
| Premium Hero | 85mm + f/1.8 + soft studio 3-point |
| Authentic Lifestyle | 50mm + f/1.8-2.8 + natural window |
| Catalog / Detail | 85mm + f/8 + studio bright |
| Ultra-Luxury | 135mm + f/1.4-2.8 + moody dramatic |
| UGC / Real Feel | 50mm + f/4-5.6 + golden hour |
| Detail / Macro | 100mm+ macro + f/2.8-4 + studio precise |
| Flat Lay / Social | 50mm + f/2.8-4 + natural overhead |
| Environmental Context | 35-50mm + f/5.6-8 + natural ambient |
| Fashion/Jewelry On-Person | 50mm + f/2.8-4 + natural mixed |
| Minimalist Product | 50mm + f/8-11 + high-key studio |
| Luxury Tabletop Still | 85mm + f/2.8-4 + studio 3-point |

**Only 3 focal lengths matter**: **50mm** ("the world as you naturally see it" — lifestyle, UGC, context, flat lays, people); **85mm — the default** (flattering compression, beautiful bokeh, the professional standard — when unsure, choose this); **135mm** (maximum bokeh and compression, ultra-premium cinematic, use sparingly).

**Only 2 aperture zones matter, plus the safe middle**: **f/1.8-2.8 "Beautiful Blur"** (single hero item, background disappears — avoid when multiple areas must stay sharp); **f/4 — most versatile** (easier focus, style plus some retained context, the safe "works for everything" choice); **f/8-11 "Sharp Catalog"** (everything sharp front-to-back — e-commerce, technical, multi-part products — too clinical for premium hero work).

**The 5 framings**

| Framing | Effect | Use for |
|---------|--------|---------|
| Straight-on | Direct, symmetrical, honest | Catalog, symmetrical products (watches, phones) |
| **Three-quarter — default** | Depth + dimension, shows front AND side; "almost always works" | Hero shots, most products |
| Overhead / flat lay | Bird's-eye, styled composition | Social, product + props |
| Low angle | Powerful, commanding, scale | Luxury statements — rare but impactful; reads unnatural if overused |
| Close-up / macro | Texture, craftsmanship proof | Jewelry detail, quality storytelling |

**Master formula**: "[Focal length] lens, [aperture] aperture, [lighting], [framing angle], [depth result], [mood/vibe]" — e.g. "85mm lens, f/1.8 aperture, studio three-point lighting, 3/4 angle, creamy bokeh background, cinematic premium aesthetic."

**Common camera mistakes**: letting the model choose (no camera spec = random perspective, no set-wide consistency); wrong combo for the job (f/1.8 blurs catalog detail; f/8 kills hero drama); inconsistency across a set (keep one camera recipe per product line).

---

## Scene and Lighting Reference

**The 8 environment presets**

| Preset | Signature materials & props | Palette | Prompt snippet |
|--------|----------------------------|---------|----------------|
| Luxury/Premium | Marble, brass/gold, velvet/silk, candles, orchids | Jewel tones, gold, cream, black | "Luxury premium product on marble surface, gold accents, soft candlelight, opulent spa aesthetic" |
| Minimalist/Scandinavian | White/pale gray, light wood, negative space, single stem | White, light gray, pale beige, wood | "Minimalist Scandinavian product photography, pale gray background, lots of negative space, monochromatic clean aesthetic" |
| Rustic/Artisanal | Reclaimed wood, linen/burlap, herbs, terracotta, handmade ceramics | Earth tones, rust, sage, honey gold | "Rustic artisanal product photography, wooden surfaces, natural ingredients, herb accents, cottage handmade aesthetic" |
| Modern/Tech | Polished concrete, glass, brushed aluminum, chrome | Black, white, charcoal, metallic | "Modern tech product photography, sleek contemporary space, metallic accents, clean lines, urban loft aesthetic" |
| Wellness/Organic | Natural wood, plants (monstera, ferns), stone, linen, crystals | Sage, cream, plant greens, earth browns | "Wellness organic product photography, botanical elements, natural green plants, outdoor light, peaceful wellness feel" |
| Playful/Fun | Bright paper backdrops, colorful tiles, confetti, fun props | Neon, pastels, rainbow, bold | "Playful fun product photography, bright colorful background, cheerful energetic setup, fun youthful vibes" |
| Professional/Corporate | Polished desk, glass/chrome, leather, documents | Navy, charcoal, white, gold accents | "Professional corporate product photography, polished business desk, trustworthy aesthetic, polished and professional" |
| Bohemian/Free-Spirited | Tapestry/kilim, vintage wood, macramé, dried flowers | Warm jewels, rust, terracotta, mustard | "Bohemian eclectic product photography, colorful textiles, vintage elements, artistic free-spirited aesthetic" |

Master formula: "[Product] in [environment], [lighting setup]. [Palette], [lighting temperature]. [Mood], [brand archetype]."

**The 5 lighting recipes**

| Recipe | Feel / best for | Exact prompt language | Key setup numbers |
|--------|-----------------|----------------------|-------------------|
| Natural Window Light | Authentic, lifestyle, UGC, skincare | "natural window light from left side, soft diffused daylight, authentic lifestyle lighting, warm natural tones, gentle shadows" | Subject 3-5 ft from window; sheer-curtain diffusion; white reflector opposite |
| Soft Studio Three-Point | E-commerce, luxury, REFLECTIVE items | "three-point soft lighting setup, key light from upper left, fill light right side, back light for separation, polished premium aesthetic" | Key 45° up/45° side; fill opposite; backlight 6 ft behind |
| Golden Hour | Beauty, editorial, romance — NOT reflective items | "golden hour sunlight, warm directional light from side, golden amber tones, romantic mood, sunset glow, cinematic feel" | 1-2h before sunset; warm white balance 3200-4000K |
| High-Key Bright | Amazon/marketplace, clinical, catalogs | "white background, bright studio lighting, sharp focus, maximum clarity, high-key bright aesthetic, pristine and clean" | Neutral 5500K; blow out background; fill from all sides |
| Moody/Dramatic | Luxury, fragrance, editorial, fine jewelry | "dark charcoal background, strong directional lighting, high contrast, cinematic and mysterious, dramatic shadows and highlights" | Single key at 45°, minimal fill; expose for highlights; cool 5500-6500K |

**Two hard rules**: reflective products (glasses, jewelry, metal, glass) always need soft studio light with fill — single-direction light hides critical detail in shadow, and golden hour is effectively banned for them. And lighting is roughly half of the whole equation: an imperfect lens with perfect light will beat a perfect lens with bad light.

**Action & pose library, by niche**
- Skincare: cradling at chest (serene, "nurturing care") · examining at face level (curious focus) · applying to skin (satisfied concentration) · displaying/presenting (confident recommendation, direct camera engagement).
- Beverage: drinking/sipping (quiet joy, mid-sip) · holding at side (casual break, warm approachability) · toasting (celebratory).
- Fashion: wearing full body (confident ease, shows fit and drape) · adjusting a detail (hands on collar/hem, showcases craftsmanship).
- Tech: using/typing (engaged focus) · cradling device (comfortable trust).
- Food: eating (mid-bite, satisfied pleasure) · preparing (hands chopping/stirring, artisanal care).
- Fitness: using equipment (focused determination, dynamic) · stretching/recovery (peaceful, mindful).

Master formula: "[Archetype] [action/pose], [expression], [looking direction]. Wearing [clothing]. [Lighting], [film stock/style]." Gaze logic: looking at the product signals interest; looking at camera signals connection; looking away/candid signals authenticity (best for UGC).

**Expression vocabulary**

| Expression | Prompt phrase | Best for |
|-----------|---------------|----------|
| Serene | "serene peaceful expression, calm soft gaze, quiet contentment" | Wellness, spa, luxury skincare |
| Confident | "confident assured expression, direct steady gaze, controlled authority" | Professional, premium, corporate |
| Joyful | "joyful genuine smile, bright happy eyes with crinkles, authentic happiness" | Family, lifestyle, celebration |
| Focused | "focused concentrated expression, intent sharp gaze, purposeful attention" | Productivity, sports, technical |
| Curious | "curious wondering expression, wide bright eyes, engaged wonder" | Education, innovation, youth |
| Satisfied | "satisfied pleased expression, warm contentment, accomplished joy" | Food, beauty, results-focused |
| Playful | "playful creative expression, lighthearted smile, spontaneous joy" | Gen-Z, trendy, entertainment |
| Contemplative | "contemplative thoughtful expression, pensive inward gaze, wise reflection" | Mindfulness, luxury, mental health |
| Powerful | "powerful commanding expression, strong intense gaze, dominant authority" | Sports, leadership, bold brands |
| Authentic/Candid | "authentic genuine expression, candid real moment, relatable realness" | UGC, community, ethical brands |

**Quick decision tree**: environment follows brand positioning (luxury → Luxury preset; youth → Playful; wellness → Organic; creative → Bohemian). Lighting follows platform (Instagram → golden hour/window; Amazon → high-key; editorial → moody; professional → three-point; authentic → window).

---

## Model Archetypes — ingredient 3 (people)

**The 10 archetypes**

| Archetype | Age | Vibe words | Best for |
|-----------|-----|-----------|----------|
| Luxury Woman | 26-35 | Elegant, refined, polished, aspirational | Luxury jewelry, watches, premium skincare, editorial |
| Everyday Mom | 30-42 | Warm, relatable, genuine, trustworthy | Family/household, organic brands, UGC |
| Fitness Enthusiast | 20-30 | Athletic, energetic, determined | Activewear, supplements, sports gear |
| Business Professional | 35-50 | Authoritative, polished, composed | B2B, finance, professional services |
| Gen-Z Creative | 18-24 ⚠ needs "youthful" | Artistic, playful, indie, digital-native | Youth brands, streetwear, apps |
| Mature Sophisticate | 50-65 | Cultured, graceful, timeless | Premium anti-aging, wealth management, travel |
| Rugged Outdoorsman | 30-45 | Weathered, authentic, grounded | Outdoor gear, workwear, heritage brands |
| Tech-Savvy Millennial | 24-35 | Modern, sleek, minimalist | Tech products, startups, smart home |
| Wellness Seeker | 25-40 | Peaceful, holistic, serene | Yoga, organic, clean-label, meditation |
| Fashion Forward | 20-30 | Bold, editorial, avant-garde | Designer brands, beauty, high fashion |

**Master prompt template**: "Portrait photo of a [youthful?] [age]-year-old [ethnicity] [man/woman] with [stacked facial features], [hair description], [facial hair control if male], [expression], head and shoulders framing, wearing [clothing], in [location] with [lighting]. [Mood/vibe], shot on [film stock or camera]."

**Face construction rules**:
- Feature stacking: single descriptors alone produce generic faces. Stack 3-4: face = [shape]+[chin]+[cheekbones]+[eyes]+[lips] (e.g. "oblong face, pointed chin, high cheekbones, hooded eyes, thin lips"). Nose gets its own separate construction: [shape]+[bridge]+[tip]+[nostrils].
- Age accuracy: ages 18-24 need the word "youthful" explicitly, or 20-year-olds tend to render as 28+; prefer "teen"/"child" phrasing over specifying very young exact ages.
- Facial hair (male): the model adds stubble by default — say "no facial hair" / "clean-shaven" explicitly, or specify the exact beard you want.
- Emotion volume control: never use raw emotion words. "Quiet joy" not "happy"; "restrained anxious look with concerned brow" not "worried"; "controlled anger with tension around mouth" not "angry"; "mild melancholy" not "sad."
- Always specify both ethnicity and exact age — this breaks the model's tendency toward stereotyped defaults.

**Film stocks & camera modifiers** (mood dial, placed at the end of the prompt)

| Modifier | Effect |
|----------|--------|
| Cinestill 800T | Cinematic night look, cool shadows, halation |
| Tri-X 400 | Gritty black-and-white documentary |
| Fujicolor Pro | Natural candid color tones |
| Sony A7sII | Crisp modern realism |
| Polaroid SX-70 | Soft vintage instant-photo look |

**Safety-filter workarounds**: "sports bra and briefs" instead of "bikini"; "larger chest" instead of "large bust"; avoid stacking multiple anatomical descriptors; move any suggestive context into the clothing description rather than the body description.

---

## Product Category Reference — ingredient 3 (products)

**The quick table**

| Category | Key attributes to always specify | Known model weak spot |
|----------|----------------------------------|-------------------|
| Skincare / Beauty | Container material (glass/plastic/ceramic — critical), cap type (dropper/pump), liquid color, finish (matte/frosted/glossy) | Accurate text on labels |
| Supplements | Bottle material (HDPE/amber glass/clear), capsule color, capacity/count, cap type | Readable label text |
| Food Packaging | Format (box/pouch/can) + material, size/weight, color scheme & design | Perfect text reproduction |
| Apparel | Fabric type & composition (critical — e.g. "80% cotton 20% spandex"), fit/silhouette, exact color, fabric weight | Readable logos/tags |
| Jewelry | Metal type & karat, stone type/cut/carat, dimensions, finish | Tiny hallmarks/engravings |
| Electronics | Exact model & color, screen content if visible, materials (aluminum/glass) | UI/interface accuracy |
| Home Goods | Material composition, dimensions, color & texture, finish | Fine details/stitching |
| Pet Products | Material & durability, size/capacity, pet type | Size-label readability |

**Universal description template**: "[Product type] made of [material], [exact size/capacity], [color — hex or named], featuring [key details: cap/closure/label/stones/ports], [finish]. Positioned on [surface], lit with [lighting type]."

**Rules that hold across every category**:
- Material words do the heavy lifting — "frosted glass serum bottle showing opaque white cream inside" beats "nice bottle" every time.
- State exact capacity/size, and remember the model reads magnitude, not units (see Dimension Control).
- Say explicitly whether text/labels should be visible and exactly what they should say — never expect perfect text reproduction; text is always the canary for whether resolution or prompting has a problem.
- Each category's known weak spot is your first quality check for that category — check it before anything else.

---

## Brand and Palette Reference — ingredient 6

Brand acts as a FILTER over the whole image — the same product, run through 8 different brand personalities, looks entirely different each time.

**Industry palettes (with hex)**

| Industry | Primary colors | Vibe / lighting |
|----------|---------------|-----------------|
| Luxury/Beauty | Emerald #2d5a3d · burgundy #800020 · gold #d4af37 · cream #f5f1e8 · charcoal #1a1a2e | Opulent; dramatic/moody |
| Health/Wellness | Sage #7b9e89 · calm blue #5a8d9e · fresh green #a8d5ba · warm tan #c9b8a8 | Peaceful; warm natural |
| Tech/Electronics | Charcoal #1f1f1f · white #ffffff · tech blue #0066ff · silver #c0c0c0 | Clean; bright clinical |
| Food & Beverage | Warm brown #8b4513 · coffee #a67c52 · gold #d4a574 · terracotta #e07a5f | Appetizing; warm golden |
| Fashion/Apparel | Navy #001f3f · camel #c9a961 · blush #f4d4c8 · gold #d4af37 | Elegant; warm studio |
| Home/Lifestyle | Terracotta #c9614f · warm tan #a89968 · navy #2c3e50 · olive #7a8c6f | Cozy; warm soft |
| Pet Products | Warm orange #ff8c42 · pet brown #8b6f47 · fresh green #7cb342 | Playful; warm energetic |
| Baby/Kids | Soft pink #ffc0cb · baby blue #b3d9ff · peach #ffe6cc · mint #b2dfdb | Gentle; soft bright |

Formula: "[industry] → [primary hex] + [secondary hex] + [neutral hex], [visual markers] + [lighting temperature] = [brand vibe]."

**The 8 brand archetypes**

| Archetype | Palette core | Materials | Camera/light | Example brands | Prompt snippet |
|-----------|-------------|-----------|--------------|----------------|----------------|
| Luxe Sophisticate | Emerald #2d5a3d, sapphire #003f87, gold #d4af37 | Marble, velvet, silk, brass | 85-135mm f/1.8-2.8, dramatic | Tom Ford, Hermès, Chanel | "Luxury premium product, emerald and gold palette, marble surface, dramatic studio lighting" |
| Clean Minimalist | White #ffffff, pale gray #f5f5f5, soft black #1a1a1a | Matte white, light wood, concrete | 50mm f/5.6-8, high-key | Apple, Muji, Diptyque | "Minimalist modern product, white and pale gray palette, lots of negative space, clean bright studio lighting" |
| Natural Organic | Sage #7b9e89, green #a8d5ba, tan #c9b8a8 | Plants, untreated wood, linen | 50mm f/2.8-4, window/golden 3200-4000K | Patagonia, RMS Beauty | "Organic natural product, sage green and warm tan palette, botanical elements, natural window light" |
| Bold Disruptor | Neon pink #ff00ff, electric blue #0066ff, orange #ff6b35 | Bold graphics, pop art | 50mm f/2.8-4, bright/harsh | Liquid Death, Glossier | "Bold energetic product, vibrant colorful background, neon accents, unconventional youthful aesthetic" |
| Trusted Expert | Navy #001f3f, deep gray #2a2a2a, trust blue #0066cc | Clinical, metal, glass | 85mm f/5.6-8, controlled | CeraVe, Dyson, Olaplex | "Professional expert product, navy and white palette, precise technical lighting, clinical trustworthy aesthetic" |
| Playful Creative | Coral #ff6b6b, sunny yellow #ffd93d, pink #ff8fab | Colorful patterns, playful props | 50mm f/2.8-4, mixed | Lush, Canva, Benefit | "Playful creative product, bright colorful palette, joyful expressive aesthetic, fun dynamic composition" |
| Heritage Classic | Warm brown #8b6f47, navy #001f3f, deep red #8b3a3a, gold #d4af37 | Leather, wood, polished finishes | 85mm f/4-5.6, warm | Ralph Lauren, Rolex, Barbour | "Heritage classic product, navy and gold palette, warm studio lighting, timeless elegant aesthetic" |
| Wellness Guide | Lavender #c9b0d4, pale blue #b3d9ff, soft sage #9cba9f | Soft textures, crystals, spa | 50mm f/2.8-4, soft | Ritual, Calm, Alo Yoga | "Wellness product, soft lavender and sage palette, warm soft lighting, calm meditative aesthetic" |

**Getting brand specs from a client — the 5 questions**:
1. Exact brand colors? Get hex codes ("navy #1B3A57 and gold #D4AF37"), never vague color names like "blue and gold."
2. Warm or cool?
3. Three words for your visual personality?
4. Which brands do you admire visually?
5. What should your images NEVER look like?

**Common brand mistakes**: generic color words instead of hex codes; forgetting to specify temperature (warm vs cool); different brand specs drifting across images in the same set — reusing the identical BRAND block on every image of a project is what actually creates visual cohesion.
