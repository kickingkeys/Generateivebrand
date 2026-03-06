# Notes and Research

Working notes for the generative brand identity prototype. What we tried, what worked, what to explore next.

## The core idea

A brand identity is traditionally a set of static files: logo, colors, type specs. This prototype treats the brand as a **grammar** instead. There are rules and constraints (invariants) and open slots (variables) that get filled at render time based on context signals.

The flower-replacing-the-F approach is one instance of this. The generalizable version: any brand element that can be parameterized (color, texture, shape, illustration, motion) can be driven by context (who the audience is, where they are, what time it is, what the touchpoint is for).

Nobody owns this idea cleanly yet. The design world talks about "dynamic identity" and "fluid logos." The AI/agent world talks about "context engineering." But the two conversations haven't merged. This prototype sits in that gap.

## What we built

### Image generation
- Used Gemini 3.1 Flash Image (via nano-banana-pro) to generate 10 monochrome ink flower illustrations
- Prompt pattern: "stylized elegant [flower] illustration, monochrome black ink on pure white background, minimal clean lines, suitable as a luxury brand mark logo element, no text, centered composition, botanical art style, high contrast"
- Consistent style across all 10 species, which is important for brand coherence

### Background removal
- Used `rembg` (Python, CPU mode) for local background removal
- Clean results on these high-contrast ink illustrations
- Considered using Replicate's 851-labs/background-remover API but didn't have a token handy. Worth revisiting for batch processing or higher quality needs.

### Procedural rendering
- Canvas 2D API with bezier curves for petal shapes
- Seeded PRNG (mulberry32) so the same seed always produces the same flower
- 10 flower type renderers, each with parametric variation (petal count, angle jitter, color blending, size variation)
- All variation stays within per-location color constraints

### Composition
- The flower replaces the "F" in FLOWERS, acting as a dropcap
- Wordmark is Playfair Display, 400 weight, 0.18em letter spacing
- A rule line and uppercase location label anchor the mark below
- Accent color (from the flower's palette) tints the page subtly

## Things to try next

- Generate multiple AI images per location (not just one canonical mark) and randomize selection
- Add more context axes beyond location: season, time of day, audience segment
- Try SVG vectorization of the AI images (following Gwern's recraft.ai workflow) for smaller file sizes
- Animate transitions between locations/variants
- Export the composed mark as a single PNG/SVG
- Try ControlNet or style-transfer to generate flowers that match a specific brand aesthetic more tightly
- Build an agent that selects the right variant based on structured context input
- Dark mode support (invert the ink illustrations, test if they hold up)

## Tools used

- **Image generation**: Gemini 3.1 Flash Image (Google) via nano-banana-pro skill
- **Background removal**: rembg (Python, open source, runs locally)
- **Procedural rendering**: Canvas 2D API, vanilla JS
- **Typography**: Playfair Display (Google Fonts), Inter, JetBrains Mono
- **No frameworks, no build tools** - single HTML file

## References

### Generative identity in practice

- MIT Media Lab identity by E Roon Kang (2010) - 40,000+ algorithmic logo permutations, each person gets a unique shape. The original case study for this approach. http://www.eroonkang.com/projects/MIT-Media-Lab-Identity
- City of Melbourne logo (Landor, 2009) - M shape filled with different content depending on context
- Nordkyn identity - logo shape driven by live weather data
- Pentagram's MIT Media Lab redesign (2014) - pulled back to a fixed grid, interesting as a counter-example

### Gwern's dropcap work

- Dropcap Generation With AI (2023-2024) - detailed writeup on using MJ/DALL-E for web dropcaps, SVG workflows, the Dropcap Workshop editor. Direct inspiration for this prototype. https://gwern.net/dropcap
- Key insight: the "flower as F" approach is essentially a historiated initial, bringing dropcaps back to their medieval origins where each one was customized to its context

### AI and brand systems (2025-2026)

- "The End of Static Brands" - Web Designer Depot, January 2026. Names the shift from pre-defined to probabilistic brand systems.
- SLO-PaletteGAN - SAGE journals 2025 paper on GAN-driven color scheme generation for brand identity, using style-aware loss functions and semantic constraints
- "Order Matters: Learning Element Ordering for Graphic Design Generation" - SIGGRAPH 2025
- "DesignManager: An Agent-Powered Copilot for Designers" - SIGGRAPH 2025
- Generative visual design creation method - Springer/Discover Applied Sciences 2025, neural network expert systems for packaging design

### Background removal

- rembg - https://github.com/danielgatis/rembg - open source, runs locally, good enough for high-contrast illustrations
- 851 Labs background remover on Replicate - https://replicate.com/851-labs/background-remover/api - API option for batch processing

### Related concepts

- Design tokens and context-switching (Figma Variables)
- Programmatic SVG generation (p5.js, Paper.js, d3)
- The "brand as grammar" framing connects to computational linguistics (generative grammars applied to visual language)
- Nike's regional tone modulation: modifies motivational tone by region, but for copy, not visual form
