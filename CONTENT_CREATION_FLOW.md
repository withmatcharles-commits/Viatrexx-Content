# Viatrexx Content Creation Flow

**Version:** Phase 2 (March 2026)
**Goal:** Equip AI agents and content creators with a repeatable, tool-integrated process for producing on-brand content that positions Viatrexx as the Protocol Authority in integrative medicine.

---

## 1. Strategic Foundation: The 7 Core Topic Pillars

All content ties back to one or more of these pillars.

| # | Pillar | Primary Focus |
|---|--------|---------------|
| 1 | Brand Philosophy & Origins | The "Why" — trust, story, emotional connection |
| 2 | Product Education & Usage | Practical how-to's for 99+ products |
| 3 | Integrative & Holistic Health | Root-cause thinking bridging conventional + complementary |
| 4 | Metabolic Factors & Optimization | Science of low-dose micro-nutrients and sarcodes |
| 5 | Detoxification, Repair, & Regeneration | Mechanics of terrain healing |
| 6 | Services for Practitioners (B2B) | Tools and support for licensed partners |
| 7 | Innovative Manufacturing | Quality differentiation via proprietary processes |

**Rule:** Every piece of content must answer: "Which pillar does this serve?" Overlaps are encouraged.

---

## 2. Content Types (Phase 2 — Full Format Set)

Phase 2 expands beyond Phase 1 evergreen formats to include short-form video and AI-powered production.

### Static & Image-Based
- **Infographic / Static Post** — Single-image education (save-worthy stats, diagrams)
- **Carousel** — 5–10 slide swipe-through (Hook → Problem → Solution → CTA)
- **Testimonial / Quote Post** — Social proof quote cards or transformation stories

### Video — Short-Form (NEW in Phase 2)
- **Reel / Short (15–90s)** — Vertical 9:16, hook-driven micro-content
  - Formats: Quick tips, myth-busters, product demos, before/after reveals, protocol snippets
  - Platforms: Instagram Reels, YouTube Shorts, Facebook Reels, TikTok (future)

### Video — Long-Form
- **Explainer Video (~5–15 min)** — Horizontal 16:9, educational lectures, whiteboard explanations
- **Video Explainer (NotebookLM)** — AI-generated visual explainer from knowledge base content

### Audio & Long-Form
- **Podcast Episode** — Audio/video deep dives (interviews, case studies, guest experts)
- **Audio Explainer (NotebookLM)** — AI-generated audio summary/overview from source documents

### Written
- **SEO Blog Post** — 1,500+ word articles (source of truth, keyword-targeted)
- **Email Newsletter** — Segmented recaps/promotions (Public / Practitioner / Partner)

### Presentation & Infographic (NEW in Phase 2)
- **Slide Deck (NotebookLM)** — AI-generated educational slides from knowledge base
- **Infographic (NotebookLM)** — AI-generated data visualization / process diagrams

---

## 3. Awareness Level Framework

Every content piece maps to a stage in the buyer journey:

| Level | Stage | Content Goal | Content Types |
|-------|-------|-------------|---------------|
| 1 | Unaware (TOFU) | Surprise with problems/stats | Static Post 1, Carousel 1, Explainer Video 1, Podcast 1, Reel (hook) |
| 2 | Problem-aware (MOFU) | Explain frameworks/misconceptions | Static Post 2, Carousel 2, Explainer Video 2, Reel (education) |
| 3 | Solution-aware (BOFU) | Show proof, protocols, CTAs | Static Post 3, Testimonial, Podcast 2, Reel (proof/demo) |

---

## 4. AI Tool Integration Map

### 4.1 Remotion MCP — Video Production

**Purpose:** Programmatic video creation for Reels, Shorts, Explainer Videos, and video ads.

**Capabilities via Remotion MCP:**
- Compose video scenes from code (React-based video components)
- Render to MP4/WebM at any resolution (1080x1920 vertical, 1920x1080 horizontal)
- Animate text overlays, transitions, logo reveals, data visualizations
- Sequence image slides with Ken Burns effects for carousels-to-video
- Add audio tracks (voiceover, music beds)
- Batch render multiple variants (A/B hook testing, platform-specific cuts)

**Use Cases:**
| Content Type | Remotion Workflow |
|-------------|-------------------|
| Reel / Short | Compose 15–90s vertical video with animated text, product shots, CTA overlay |
| Explainer Video | Sequence slides + voiceover + animated diagrams into 5–15 min horizontal video |
| Carousel-to-Video | Convert static carousel slides into animated video with transitions |
| Testimonial Video | Animate quote cards with brand styling and background music |
| Ad Variants | Batch render 3 hook variants for A/B testing (3-2-2 method) |

**Render Specs:**
| Format | Resolution | Aspect | FPS | Use |
|--------|-----------|--------|-----|-----|
| Reel / Short | 1080×1920 | 9:16 | 30 | IG Reels, YT Shorts, FB Reels |
| Standard Video | 1920×1080 | 16:9 | 30 | YouTube, Website, LinkedIn |
| Square Video | 1080×1080 | 1:1 | 30 | Facebook Feed, LinkedIn Feed |

### 4.2 NanaBanana 2 — Image & Carousel Generation

**Purpose:** AI image generation for static posts, carousel slides, and visual assets.

**Use Cases:**
| Content Type | NanaBanana Workflow |
|-------------|---------------------|
| Static Post / Infographic | Generate brand-aligned hero image from prompt |
| Carousel Slides | Generate individual slide backgrounds/illustrations |
| Thumbnail | Create YouTube/podcast thumbnails from topic brief |
| Quote Card | Generate styled background for testimonial overlays |
| Pinterest Pin | Generate tall-format (2:3) visual assets |
| **NLM Watermark Removal (Image)** | **Remove NotebookLM watermark from Infographics and Slide Decks (bottom-right corner)** |

**NanaBanana 2 — NotebookLM Post-Processing:**
NotebookLM outputs (Infographics, Slide Decks) include a watermark in the bottom-right corner. NanaBanana 2 handles removal via inpainting/removal:
1. Export each slide or infographic as individual image files
2. Use NanaBanana 2 image editing/inpainting to remove the bottom-right watermark
3. Optionally replace the watermark area with Viatrexx branding (subtle logo or tagline)
4. Re-assemble cleaned slides into final deck if applicable

**Prompt Structure for Viatrexx:**
```
Style: Clean, clinical-yet-warm, nature-meets-science aesthetic
Colors: Brand palette (deep teal, gold accents, white space)
Avoid: Stock photo clichés, stethoscopes near products, "cured" patient imagery
Include: Nature elements, prism/light motifs, flowing water, cellular/matrix patterns
```

### 4.3 NotebookLM — Knowledge Base Content

**Purpose:** AI-powered content generation from the Viatrexx knowledge base (protocols, brand docs, SEO plans).

**Use Cases:**
| Output Type | NotebookLM Workflow |
|------------|---------------------|
| Video Explainer | Upload source docs → Generate narrated visual explainer → **Post-process (see below)** |
| Audio Explainer | Upload source docs → Generate podcast-style audio overview → **Post-process (see below)** |
| Infographic | Upload data/protocols → Generate visual data summary → **Remove watermark (NanaBanana 2)** |
| Slide Deck | Upload topic brief → Generate educational presentation → **Remove watermark (NanaBanana 2)** |
| Blog Draft | Upload protocols + SEO keywords → Generate article skeleton |

**⚠️ CRITICAL: NotebookLM Post-Processing Pipeline**

All NotebookLM outputs require post-processing before they are publish-ready. NotebookLM adds watermarks and a branded ending that must be removed and replaced with Viatrexx branding.

#### 4.3.1 Infographic & Slide Deck Post-Processing

**Problem:** NotebookLM places a watermark in the bottom-right corner of generated images/slides.
**Solution:** NanaBanana 2 watermark removal.

```
NotebookLM Output (Infographic/Slides)
    │
    ▼
Export as individual image files (PNG/JPG)
    │
    ▼
NanaBanana 2: Inpaint/remove bottom-right watermark from each image
    │
    ▼
(Optional) Add Viatrexx branded footer/logo in cleaned area
    │
    ▼
Re-assemble into final slide deck or publish infographic
```

#### 4.3.2 Video Explainer Post-Processing

**Problems:**
1. NotebookLM places a video watermark in the bottom-right corner throughout
2. NotebookLM appends a branded ending/outro that must be removed
3. Video needs a new Viatrexx-branded ending with CTA

**Solution:** Multi-step pipeline using Remotion MCP + external video processing + Voice AI.

```
NotebookLM Video Output
    │
    ▼
Step 1: TRIM ENDING
    Remotion MCP (or FFmpeg): Detect and slice off the NotebookLM
    branded ending segment. Identify the frame where original
    content ends and NLM outro begins → trim at that point.
    │
    ▼
Step 2: REMOVE VIDEO WATERMARK
    External API solution (video inpainting/watermark removal API):
    Process trimmed video to remove persistent bottom-right watermark.
    Options:
    • Video inpainting API (e.g., Remove.bg Video, HitPaw, or similar)
    • FFmpeg delogo filter for simple overlays
    • Remotion MCP overlay: Cover watermark region with branded
      lower-third bar or clean overlay strip
    │
    ▼
Step 3: ADD BRANDED ENDING
    Remotion MCP: Compose and append a new Viatrexx-branded
    ending sequence (5–15 seconds) containing:
    • Brand sign-off line (voiced)
    • Product/protocol CTA relevant to topic
    • Viatrexx logo animation
    • Website URL / "Find a Practitioner" link
    • Subscribe/follow prompt
    │
    Voice Generation (for ending VO):
    • Voice AI API (e.g., ElevenLabs, Play.ht, or similar TTS)
    • Generate branded sign-off voiceover matching NLM narrator tone
    • Script template (see Ending Scripts below)
    │
    ▼
Step 4: FINAL RENDER
    Remotion MCP: Stitch cleaned video + branded ending → final MP4
    │
    ▼
Clean, branded Video Explainer ready for publish
```

#### 4.3.3 Audio Explainer Post-Processing

**Problems:**
1. NotebookLM appends a branded audio ending/outro
2. Audio needs a new Viatrexx-branded ending with CTA

**Solution:** Audio trimming + Voice AI for new ending.

```
NotebookLM Audio Output
    │
    ▼
Step 1: TRIM ENDING
    FFmpeg (or audio editor): Detect and slice off the NotebookLM
    branded ending. Trim at the point where original content ends.
    │
    ▼
Step 2: ADD BRANDED ENDING
    Voice AI API: Generate Viatrexx sign-off voiceover
    • Match tone/style of NLM narrator voice
    • Script from Ending Templates (see below)
    │
    ▼
Step 3: STITCH
    FFmpeg / Remotion MCP: Append branded audio ending to trimmed content
    • Optional: Add subtle music bed under sign-off
    │
    ▼
Clean, branded Audio Explainer ready for publish
```

#### 4.3.4 Branded Ending Script Templates

These scripts replace the NotebookLM outro. Select and customize based on topic/pillar.

**Video Explainer Ending (General):**
```
[Voiceover — warm, authoritative tone]
"That's the science behind [TOPIC]. To go deeper into the protocol
and explore how Bio-Incorporated medicine can support your practice
or your healing journey, visit viatrexx.com.

Practitioners — join the Partner Program for full protocol access
and wholesale pricing.

This is Viatrexx — the pathway through the matrix."

[Visual: Viatrexx logo animation → URL → "Follow us" social icons]
[Duration: 10–12 seconds]
```

**Video Explainer Ending (B2B / Practitioner Focus):**
```
[Voiceover]
"Ready to implement this protocol with your patients?
Access the full therapeutic index and clinical roadmaps
in the Viatrexx Practitioner Portal at viatrexx.com/partners.

Solve your most difficult cases. Join the Protocol Authority."

[Visual: Viatrexx logo → Partner Program CTA → URL]
[Duration: 8–10 seconds]
```

**Video Explainer Ending (B2C / Seeker Focus):**
```
[Voiceover]
"Your body already knows how to heal — it just needs the right
signals. Explore the full Viatrexx range and find a practitioner
near you at viatrexx.com.

Stop chasing symptoms. Optimize the terrain."

[Visual: Viatrexx logo → Product range → "Find a Practitioner" CTA]
[Duration: 8–10 seconds]
```

**Audio Explainer Ending (General):**
```
[Voiceover]
"Thanks for listening. To learn more about [TOPIC] and explore
the full protocol, visit viatrexx.com. If you're a licensed
practitioner, ask about our Partner Program for exclusive access
to clinical protocols and wholesale pricing.

This has been a Viatrexx Bio Inc. production — the science of
flow, for systemic regeneration."

[Optional: Subtle music sting — 3 seconds]
[Duration: 12–15 seconds]
```

**Audio Explainer Ending (Condition-Specific):**
```
[Voiceover]
"If [CONDITION] is something you or your patients are navigating,
the [PRODUCT_NAME] protocol offers a terrain-first pathway
to support. Full details at viatrexx.com.

This has been a Viatrexx Bio Inc. production."

[Duration: 8–10 seconds]
```

#### 4.3.5 Voice AI Configuration

For generating branded ending voiceovers:

| Parameter | Setting |
|-----------|---------|
| Voice style | Warm, clinical, authoritative — not salesy |
| Gender | Match the NLM narrator gender when possible |
| Pace | Medium — slightly slower than conversational |
| Tone | Professional guide, not announcer |
| API options | ElevenLabs, Play.ht, Amazon Polly (neural), Google Cloud TTS |
| Output format | WAV or MP3 at 44.1kHz |

**Voice cloning note:** If a consistent Viatrexx brand voice is established, clone it in the Voice AI platform and reuse across all endings for consistency.

**Knowledge Base Sources:**
- Brand Identity & Positioning Guides
- Therapeutic Protocols Breakdown (11 protocols)
- SEO Keyword & Content Architecture Plans
- Content Topics Database (140 topics)
- Product monographs and therapeutic index

---

## 5. Step-by-Step Content Creation Flow

### Step 1: Topic Selection & Assignment

**Input:** Weekly topic from the Content Calendar (one core topic per week).

**Action:**
1. Select the weekly Pillar + Topic from the Topic Database
2. Assign awareness level (TOFU / MOFU / BOFU)
3. Determine content types to produce (minimum set per week)
4. Assign to Content Queue with status "Queued"

**Minimum Weekly Output:**
| Type | Count | Platforms |
|------|-------|-----------|
| Static Post | 3 | FB, IG, LI, Pin |
| Carousel | 2 | FB, IG, LI, Pin |
| Reel / Short | 3 | IG, YT, FB |
| Explainer Video | 1 | YT, FB, LI |
| Podcast Episode | 1 | YT, Website, Email |
| Testimonial | 1 | FB, IG, LI |
| SEO Blog Post | 1 | Website |
| Email Newsletter | 1 | Email |

### Step 2: Create Master Content Brief

Create **one reusable brief per topic + content type**. This is the core asset. Use the Brief Templates in `/templates/briefs/`.

Every brief must include:
- Topic ID & Pillar reference
- Goal & Awareness Level
- Target Audience (B2B / B2C / Both)
- Primary SEO Keywords
- Scientific Accuracy Checklist
- Regulatory Compliance Notes

### Step 3: AI Asset Generation

Use the tool integration pipeline:

```
Master Brief
    ├── NanaBanana 2 → Static images, carousel slides, thumbnails
    ├── NotebookLM → Audio explainer, video explainer, slides, infographic
    │       └── POST-PROCESSING (Required for all NLM outputs)
    │           ├── Images (Infographic/Slides): NanaBanana 2 watermark removal
    │           ├── Video: Trim ending → Remove watermark → Add branded ending (Remotion + Voice AI)
    │           └── Audio: Trim ending → Add branded ending (Voice AI + FFmpeg)
    └── Remotion MCP → Reels/Shorts, animated videos, carousel-to-video
```

**Workflow:**
1. **Images first** — Generate all static visual assets via NanaBanana 2
2. **Knowledge content** — Generate NotebookLM outputs (audio, slides, infographics)
3. **NLM post-processing** — Remove watermarks (NanaBanana 2 for images, video API for video), trim NLM endings, generate and append Viatrexx branded endings (Voice AI + Remotion MCP). See Section 4.3 for full pipeline.
4. **Video assembly** — Use Remotion MCP to compose final video outputs using generated assets + scripts
5. **Review** — Human review for scientific accuracy, brand tone, regulatory compliance

### Step 4: Platform-Specific Adaptation

Adapt the Master Brief and generated assets for each target platform. Use Platform Templates in `/templates/platforms/`.

| Platform | Key Adaptations |
|----------|----------------|
| Facebook | Professional tone, square images (1080×1080), community captions, Reels (9:16) |
| Instagram | Visual-first, portrait (1080×1350), 25–30 hashtags in first comment, Reels (9:16) |
| LinkedIn | B2B/science tone, text-heavy posts, PDF carousels, native video (16:9 or 1:1) |
| Pinterest | Tall pins (1000×1500), keyword-rich descriptions, link to blog |
| YouTube | Timestamps, cards, end screens, optimized description, Shorts (9:16) |
| Website | Full SEO (headers, meta, internal links, schema markup) |
| Email | Segment: Public (empathetic), Practitioners (clinical), Partners (exclusive) |

### Step 5: Production Queue & Publishing

1. **Queue:** Move completed assets to "Ready" status in Content Queue
2. **Review:** Final check — science, disclaimers, CTA clarity, regulatory compliance
3. **Schedule:** Publish via scheduling tool according to weekly rhythm
4. **Track:** Log performance metrics for optimization

---

## 6. Weekly Content Rhythm (Phase 2)

| Day | Content Pieces | Focus |
|-----|---------------|-------|
| Monday | Static Post 1 + Explainer Video 1 + Reel 1 | Educate / "The Why" |
| Tuesday | Carousel 1 + Testimonial + Reel 2 | Problem → Solution + Proof |
| Wednesday | Static Post 2 + Podcast 1 | Deep Science Dive |
| Thursday | Carousel 2 + Explainer Video 2 + Reel 3 | Condition-Specific Protocol |
| Friday | Static Post 3 | Lifestyle Tip / Soft Sell |
| Sunday | Podcast 2 | Thought Leadership |

**Weekly Email:** Sent Saturday or Monday (segmented).

---

## 7. Content Flow Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    TOPIC DATABASE                         │
│  (140 Topics × 7 Pillars × Awareness Levels)            │
└──────────────────────┬──────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────┐
│               WEEKLY TOPIC SELECTION                      │
│  (Calendar assigns Pillar + Topic + Week)                │
└──────────────────────┬──────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────┐
│              MASTER CONTENT BRIEF                         │
│  (One brief per Topic × Content Type)                    │
│  Brief Templates: /templates/briefs/                     │
└──────────┬───────────┬───────────┬──────────────────────┘
           │           │           │
           ▼           ▼           ▼
    ┌──────────┐ ┌──────────┐ ┌──────────────┐
    │NanaBanana│ │NotebookLM│ │ Remotion MCP │
    │    2     │ │          │ │              │
    │──────────│ │──────────│ │──────────────│
    │• Images  │ │• Audio   │ │• Reels/Shorts│
    │• Slides  │ │• Video   │ │• Explainers  │
    │• Thumbs  │ │• Slides  │ │• Animations  │
    │• Pins    │ │• Infogr. │ │• Ad variants │
    └────┬─────┘ └────┬─────┘ └──────┬───────┘
         │            │              │
         └────────────┼──────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────┐
│           PLATFORM ADAPTATION LAYER                       │
│  Platform Templates: /templates/platforms/                │
│  FB | IG | LI | Pin | YT | Website | Email              │
└──────────────────────┬──────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────┐
│               CONTENT QUEUE                               │
│  Status: Queued → In Production → Review → Ready → Live  │
└──────────────────────┬──────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────┐
│            PUBLISH & TRACK                                │
│  Schedule → Publish → Monitor → Optimize                 │
└─────────────────────────────────────────────────────────┘
```

---

## 8. Repurposing Strategy

One Master Brief feeds multiple outputs:

```
Master Video Brief (Explainer Video)
    ├── YouTube native upload (16:9)
    ├── Podcast audio extract
    ├── Blog transcript (SEO post)
    ├── 3× Reels/Shorts (key moments, vertical 9:16)
    ├── Carousel from key slides
    ├── Quote cards from key insights
    └── Email newsletter excerpt
```

**Remotion MCP enables automated repurposing:**
- Extract 15–90s segments from long-form video → render as Reels
- Convert carousel slides → animated video with transitions
- Batch render platform-specific aspect ratios from single source

---

## 9. Quality Gates

Every piece must pass before publishing:

| Gate | Check | Owner |
|------|-------|-------|
| Scientific Accuracy | Claims verified against protocols and product monographs | Subject Matter Expert |
| Brand Voice | Clinical but compassionate, no "miracle cure" language | Brand Lead |
| Regulatory Compliance | No forbidden claims ("cure", "always", "guaranteed"), mandatory disclaimers | Compliance |
| Visual Audit | No stethoscopes near products, no "cured patient" imagery | Design Lead |
| SEO Alignment | Target keywords present, internal links planned | SEO Lead |
| Platform Specs | Correct dimensions, hashtags, descriptions per platform | Content Manager |

---

## 10. Regulatory Compliance Quick Reference

**Forbidden:** "Always," "Never," "Cure," "Guaranteed"
**Required:** "Supports," "Promotes," "Assists"
**Mandatory Disclaimer (Homeopathic):** "This claim is based on traditional homeopathic references and not modern scientific evidence."
**Nosode Disclaimer:** "Neither a vaccine nor an alternative to vaccination."
**Visual Rule:** No stethoscopes, "cured" patient images, or medical device imagery near product links.
**DSHEA:** Educational blogs hosted on separate URL structure from e-commerce checkout.
