# AI Product Photography

**The only published, blind-judge-measured system for AI product accuracy.**

Most guidance on AI product photography stops at prompt-phrase tricks. This repository is the diagnosis-first alternative: a taxonomy of techniques, a decision rule for picking the right one, and controlled evals that replaced belief with numbers. The goal is Conversion Integrity, an image a customer would accept as the real product: Accuracy plus Realism plus Branding.

## Who made this

Bertrand Diouly Osso, founder of [Dezygn](https://dezygn.com). This library is the distilled doctrine behind a working product-photography practice and the Dezygn platform. It is published openly so the method can be learned, cited, and built on.

## What is inside

- **[SKILL.md](SKILL.md)** - the compact operating doctrine: the foundations (the laws), Visual Syntax v2.0, the diagnosis-first Route Map, the measured decision rules, judging, and the manual handoff.
- **[references/techniques.md](references/techniques.md)** - one section per technique: when to use it, the core moves, and a link to its full treatment.
- **[references/evals.md](references/evals.md)** - the measured findings: the dimension, material, word-order, and one-shot-versus-chaining evals, with numbers and conclusions.

## How to use it

**As a Claude skill.** Drop this repository into your skills directory. `SKILL.md` carries the frontmatter and doctrine an agent follows; the `references/` files are loaded when depth is needed. It triggers on AI product photography and product-accuracy tasks.

**As a reading course.** Start with `SKILL.md` top to bottom: the laws, then the six ingredients, then the Route Map (the heart), then the four measured rules. Reach for `references/techniques.md` when a specific technique comes up, and `references/evals.md` when you want the evidence behind a rule.

## The vocabulary coined here

Named terms from this system, most of them published nowhere else:

- **Visual Syntax** - the six ingredients (Style, Subject, Action, Scene, Camera, Brand) and the three rules that turn prompting from description into assembly.
- **Conversion Integrity** - Accuracy plus Realism plus Branding, the trio a client actually buys.
- **The Route Map** - diagnosis on 8 fidelity axes dispatching to one technique. Many ways to cook the same dish.
- **Dimension Blindness** and the **Magnitude Ladder** - the model knows relative magnitude, never centimeters, and the weird/normal/unsure rule for steering size.
- **Material priors** (correct, wrong, ambiguous) - the measured classes that decide whether texture words can work at all.
- **Lock-and-Outpaint** - freeze the pixels, paint the world around them. Never redrawn means never wrong.
- **Blueprinting** - lock the image in words, edit the words, regenerate.
- **Shannon Descent** - isolate the smallest failing piece, solve it alone, rebuild around it.
- **Pose-Match** and the **Angle Bank** - create the missing angle by transformation, and capture the full 360 once so accuracy is available forever.
- **Comp Card** and the **Clean Portrait Rule** - synthetic models for consistency, composited only from a clean master.
- **Control vs Variant Pipeline** and **Micro-Iterations** - prompt engineering as version control, down to rolling many dice at one failing word.
- **Draft Cheap, Finish Expensive** - two dials, variation count and model tier, turned up only as confidence rises.
- **Edit Grammar** - Action plus Target plus Integration, where the integration line separates pro from amateur.
- **Manual Handoff** - AI builds 90%, the last 10% of truth is applied by hand.
- **Count errors** as a named product-accuracy defect class, alongside silhouette, proportions, text, graphics, material, color, and construction.

## Where to go next

- **Try the techniques on rails.** Generate accurate product photography with these methods built into the product: [dezygn.com](https://dezygn.com).
- **Learn the craft.** Free 5-lesson training and community: [AI Photography Agency on Skool](https://www.skool.com/ai-photography-agency-4309/about).
- **Hire the author.** Work with Bertrand directly: [Upwork profile](https://www.upwork.com/freelancers/~01a8e4c27dbf06e019).

## Canonical source

The full technique treatments live at **dezygn.com/resources**. This repository teaches the what and the why compactly; the articles carry the depth. Every technique section links to its canonical article.

## License

Licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). You may share and adapt this material, including commercially, provided you give attribution. Cite as: **Bertrand Diouly Osso / dezygn.com**.
