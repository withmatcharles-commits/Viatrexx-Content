# Viatrexx Content Types Database

**Version:** Phase 2 (March 2026)

---

## Content Type Registry

| ID | Content Type | Category | Duration/Length | Aspect Ratio | Primary Tool | Awareness Levels |
|----|-------------|----------|----------------|-------------|-------------|-----------------|
| CT01 | Static Post / Infographic | Image | 1 image | 1:1 / 4:5 / 2:3 | NanaBanana 2 | All levels |
| CT02 | Carousel | Image (multi-slide) | 5–10 slides | 1:1 / 4:5 | NanaBanana 2 | All levels |
| CT03 | Testimonial / Quote Post | Image | 1 image | 1:1 / 4:5 | NanaBanana 2 | BOFU |
| CT04 | Reel / Short | Video (short) | 15–90 seconds | 9:16 | Remotion MCP | All levels |
| CT05 | Explainer Video | Video (long) | 5–15 minutes | 16:9 | Remotion MCP | TOFU–MOFU |
| CT06 | Video Explainer (NotebookLM) | Video (AI-generated) | 3–10 minutes | 16:9 | NotebookLM | TOFU–MOFU |
| CT07 | Podcast Episode | Audio/Video | 20–60 minutes | 16:9 (video) | Recording + Remotion | All levels |
| CT08 | Audio Explainer (NotebookLM) | Audio (AI-generated) | 5–15 minutes | N/A | NotebookLM | TOFU–MOFU |
| CT09 | SEO Blog Post | Written | 1,500+ words | N/A | AI writing + human edit | All levels |
| CT10 | Email Newsletter | Written | 300–800 words | N/A | Email platform | All levels |
| CT11 | Slide Deck (NotebookLM) | Presentation | 10–25 slides | 16:9 | NotebookLM | MOFU–BOFU |
| CT12 | Infographic (NotebookLM) | Data visualization | 1 asset | Varies | NotebookLM | All levels |

---

## Content Type Details

### CT01: Static Post / Infographic

**Purpose:** Single-image education — save-worthy stats, diagrams, quick facts.
**Production Tool:** NanaBanana 2 for image generation
**Awareness Alignment:**
- Post 1 (TOFU): Highlight hidden/unknown problem with surprising stats
- Post 2 (MOFU): Explain core concepts/frameworks
- Post 3 (BOFU): Show proof, address objections, subtle CTA

**Specs by Platform:**
| Platform | Dimensions | Notes |
|----------|-----------|-------|
| Facebook | 1080×1080 | Square, community-focused caption |
| Instagram | 1080×1350 | Portrait, 25–30 hashtags in first comment |
| LinkedIn | 1080×1080 | Professional tone, text-heavy caption |
| Pinterest | 1000×1500 | Tall pin, keyword-rich description |

---

### CT02: Carousel

**Purpose:** Multi-slide swipe-through education (Hook → Problem → Solution → CTA).
**Production Tool:** NanaBanana 2 for slide images, optional Remotion MCP for carousel-to-video
**Structure:**
- Slide 1: Hook (3-second rule — must trigger pause/swipe)
- Slides 2–8: Value delivery (myths, steps, framework, proof)
- Slide 9: Summary / Key takeaway
- Slide 10: CTA + product/action prompt

**Awareness Alignment:**
- Carousel 1 (TOFU→MOFU): Broad teaching, myths, stats, concepts
- Carousel 2 (MOFU→BOFU): Framework breakdown, quick wins, before/after, stronger CTA

**Specs by Platform:**
| Platform | Dimensions | Notes |
|----------|-----------|-------|
| Facebook | 1080×1080 | Square, max 10 slides |
| Instagram | 1080×1350 | Portrait preferred, max 10 slides |
| LinkedIn | 1080×1080 or PDF | PDF carousel option for B2B depth |
| Pinterest | 1000×1500 | Individual pins linking to blog |

---

### CT03: Testimonial / Quote Post

**Purpose:** Social proof — practitioner or patient success story.
**Production Tool:** NanaBanana 2 for styled quote card
**Structure:** Quote/result + source attribution + soft CTA
**Awareness Level:** Solution/Brand-aware (BOFU)

---

### CT04: Reel / Short (NEW — Phase 2)

**Purpose:** Hook-driven micro-content for maximum reach and discovery.
**Production Tool:** Remotion MCP (primary), can also use raw footage + Remotion overlays
**Duration:** 15–90 seconds (sweet spot: 30–60 seconds)
**Aspect Ratio:** 9:16 vertical (1080×1920)

**Reel Format Types:**
| Format | Structure | Example |
|--------|----------|---------|
| Quick Tip | Hook (3s) → Tip (20s) → CTA (5s) | "Most people detox wrong. Here's why." |
| Myth Buster | Myth statement → "Actually..." → Truth → CTA | "Supplements don't work? Actually, it's your terrain." |
| Product Demo | Problem (5s) → Product intro (10s) → Demo (20s) → Result (5s) | "1 squirt = 5 drops. Watch how easy this is." |
| Before/After | Before state → Protocol hint → After state → CTA | Aesthetics transformation (compliant imagery) |
| Protocol Snippet | "Step 1 of the Detox Protocol..." → Quick walkthrough | Drainage vs. Detox in 45 seconds |
| Talking Head | Direct-to-camera education, high authenticity | Founder or practitioner explaining concept |

**Remotion MCP Rendering:**
```
Input: Script + images/footage + audio
Output: 1080×1920 MP4 at 30fps
Features: Animated text overlays, brand lower thirds, CTA end cards
Variants: Render 3 hook variants for A/B testing
```

**Platforms:** Instagram Reels, YouTube Shorts, Facebook Reels

---

### CT05: Explainer Video (Long-Form)

**Purpose:** Educational deep-dive — whiteboard, lecture, protocol walkthrough.
**Production Tool:** Remotion MCP for composition, recording equipment for raw footage
**Duration:** 5–15 minutes
**Aspect Ratio:** 16:9 horizontal (1920×1080)

**Structure:**
1. Hook (first 30 seconds — must retain)
2. Problem/Context (1–2 min)
3. Core education points (3–5 segments with timestamps)
4. Protocol/solution demonstration
5. Conclusion + CTA

**Awareness Alignment:**
- Explainer 1 (TOFU→MOFU): Why the topic matters, core definitions, misconceptions
- Explainer 2 (MOFU→BOFU): How it works, real examples, path to action

---

### CT06: Video Explainer (NotebookLM)

**Purpose:** AI-generated visual explainer from knowledge base content.
**Production Tool:** NotebookLM → **Post-processing required**
**Input:** Source documents (protocols, brand guides, product monographs)
**Output:** Narrated video with AI-generated visuals
**Duration:** 3–10 minutes
**Use Cases:** Protocol overviews, product category education, brand philosophy explainers

**⚠️ Required Post-Processing:**
NotebookLM video outputs are NOT publish-ready. Every video must go through:

| Step | Tool | Action |
|------|------|--------|
| 1. Trim ending | Remotion MCP / FFmpeg | Detect and remove NLM branded outro segment |
| 2. Remove watermark | Video inpainting API or Remotion overlay | Remove persistent bottom-right NLM watermark |
| 3. Generate ending VO | Voice AI API (ElevenLabs, Play.ht, etc.) | Generate Viatrexx branded sign-off voiceover |
| 4. Compose ending | Remotion MCP | Build 8–15s branded ending (VO + logo + CTA) |
| 5. Final render | Remotion MCP | Stitch cleaned video + branded ending → MP4 |

See `CONTENT_CREATION_FLOW.md` Section 4.3.2 for full pipeline and ending script templates.

---

### CT07: Podcast Episode

**Purpose:** Long-form audio/video deep-dive — interviews, case studies, thought leadership.
**Production Tool:** Recording + Remotion MCP for video version
**Duration:** 20–60 minutes

**Structure:**
- Intro + topic framing (2 min)
- Main discussion / interview (15–45 min)
- Key takeaways recap (3 min)
- CTA + next episode teaser (2 min)

**Repurposing Pipeline:**
```
Podcast Episode
    ├── YouTube video version (16:9 with thumbnail)
    ├── Audio-only (Spotify, Apple, RSS)
    ├── Website transcript (SEO blog post)
    ├── 3× Reels from key moments (via Remotion MCP)
    ├── Quote cards from insights (via NanaBanana 2)
    └── Email newsletter excerpt
```

---

### CT08: Audio Explainer (NotebookLM)

**Purpose:** AI-generated podcast-style audio overview from source documents.
**Production Tool:** NotebookLM → **Post-processing required**
**Input:** Source documents from knowledge base
**Output:** Conversational audio summary
**Duration:** 5–15 minutes
**Use Cases:** Quick protocol overviews, topic primers, "listen while you commute" content

**⚠️ Required Post-Processing:**
NotebookLM audio outputs are NOT publish-ready. Every audio must go through:

| Step | Tool | Action |
|------|------|--------|
| 1. Trim ending | FFmpeg / audio editor | Detect and remove NLM branded audio outro |
| 2. Generate ending VO | Voice AI API (ElevenLabs, Play.ht, etc.) | Generate Viatrexx branded sign-off voiceover |
| 3. Stitch | FFmpeg / Remotion MCP | Append branded ending + optional music bed |

See `CONTENT_CREATION_FLOW.md` Section 4.3.3 for full pipeline and ending script templates.

---

### CT09: SEO Blog Post

**Purpose:** Source of truth — keyword-targeted long-form article.
**Production Tool:** AI writing (from brief) + human editing
**Length:** 1,500+ words
**Structure:**
- H1: [Product/Topic] — [Primary Search Term]
- H2: The Science / The Framework
- H3: Specific Benefits / Applications
- Internal links (silo strategy)
- Meta description, alt text, schema markup

---

### CT10: Email Newsletter

**Purpose:** Retention and education via segmented email.
**Segments:**
- Public (empathetic tone, root-cause education)
- Practitioners (clinical tone, protocol details)
- Partners (exclusive tone, business metrics)

---

### CT11: Slide Deck (NotebookLM)

**Purpose:** AI-generated educational presentation from knowledge base.
**Production Tool:** NotebookLM → **Post-processing required**
**Slides:** 10–25
**Use Cases:** Practitioner education, webinar decks, protocol presentations

**⚠️ Required Post-Processing:**
NotebookLM slide outputs include a watermark in the bottom-right corner of each slide.

| Step | Tool | Action |
|------|------|--------|
| 1. Export slides | Manual / script | Export each slide as individual PNG/JPG |
| 2. Remove watermark | NanaBanana 2 (inpaint/remove) | Remove bottom-right NLM watermark from each slide image |
| 3. Brand replacement | NanaBanana 2 (optional) | Add subtle Viatrexx logo or footer in cleaned area |
| 4. Re-assemble | Slide tool / Remotion MCP | Rebuild slide deck from cleaned images |

---

### CT12: Infographic (NotebookLM)

**Purpose:** AI-generated data visualization or process diagram.
**Production Tool:** NotebookLM → **Post-processing required**
**Use Cases:** Protocol flowcharts, comparison charts, statistics visualizations

**⚠️ Required Post-Processing:**
NotebookLM infographic outputs include a watermark in the bottom-right corner.

| Step | Tool | Action |
|------|------|--------|
| 1. Remove watermark | NanaBanana 2 (inpaint/remove) | Remove bottom-right NLM watermark |
| 2. Brand replacement | NanaBanana 2 (optional) | Add Viatrexx branded footer/logo in cleaned area |

---

## Content Type × Awareness Level Matrix

| Content Type | Unaware (TOFU) | Problem-aware (MOFU) | Solution-aware (BOFU) |
|-------------|----------------|---------------------|-----------------------|
| Static Post | ✅ Surprise stats | ✅ Frameworks | ✅ Proof/CTA |
| Carousel | ✅ Myths/concepts | ✅ Deep steps | ✅ Conversion |
| Testimonial | | | ✅ Social proof |
| Reel / Short | ✅ Hook/surprise | ✅ Quick education | ✅ Demo/proof |
| Explainer Video | ✅ Why it matters | ✅ How it works | |
| Video Explainer (NLM) | ✅ Overview | ✅ Deep-dive | |
| Podcast | ✅ Foundational | ✅ Actionable | ✅ Case studies |
| Audio Explainer (NLM) | ✅ Primer | ✅ Summary | |
| SEO Blog Post | ✅ Problem | ✅ Framework | ✅ Protocol |
| Email Newsletter | ✅ Educate | ✅ Nurture | ✅ Convert |
| Slide Deck (NLM) | | ✅ Education | ✅ Practitioner |
| Infographic (NLM) | ✅ Visual data | ✅ Process maps | |
