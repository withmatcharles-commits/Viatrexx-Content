# Viatrexx Platform Adaptation Templates

**Version:** Phase 2 (March 2026)
**Usage:** After a Master Brief is created, use these templates to adapt content for each target platform. Each section defines platform-specific requirements by content type.

---

## PL01: Facebook Adaptations

### Facebook × Static Post

```yaml
platform: "Facebook"
content_type: "CT01 — Static Post"
dimensions: "1080×1080"
aspect_ratio: "1:1"
file_format: "JPG or PNG"

caption:
  tone: "Professional, community-focused"
  length: "100–300 words"
  structure: |
    [Opening hook — relatable question or surprising stat]
    [2–3 sentences expanding on the core message]
    [Follow-up question to encourage comments]
  cta_style: "Conversational — 'What's your experience with...?'"

engagement:
  pinned_comment: "Pin peer social proof or clinical testimonial"
  response_strategy: "Reply to every comment within 2 hours during Golden Hour"
  golden_hour: "First 60 minutes after posting — prioritize engagement"
```

### Facebook × Carousel

```yaml
platform: "Facebook"
content_type: "CT02 — Carousel"
dimensions: "1080×1080"
aspect_ratio: "1:1"
max_slides: 10
file_format: "JPG or PNG per slide"

caption:
  tone: "Educational, warm"
  length: "150–400 words"
  structure: |
    [Hook summarizing the carousel value]
    [Key takeaway from the slides]
    [CTA: "Swipe through for the full breakdown"]
```

### Facebook × Testimonial

```yaml
platform: "Facebook"
content_type: "CT03 — Testimonial"
dimensions: "1080×1080"
aspect_ratio: "1:1"

caption:
  tone: "Empathetic, trust-building"
  structure: |
    [Brief context about the person's journey]
    [Quote or key result]
    [Soft CTA: "Have you experienced something similar?"]
  pinned_comment: "Pin additional testimonials or clinical context"
```

### Facebook × Reel

```yaml
platform: "Facebook"
content_type: "CT04 — Reel"
dimensions: "1080×1920"
aspect_ratio: "9:16"
duration: "15–90 seconds"
file_format: "MP4"

caption:
  tone: "Casual, educational"
  length: "50–150 words"
  hashtags: "5–10 relevant tags"
  cta: "Follow for more" or "Comment GUIDE"

rendering_via_remotion:
  resolution: "1080×1920"
  fps: 30
  brand_overlay: true
  captions: "Burned-in subtitles required"
```

### Facebook × Explainer Video

```yaml
platform: "Facebook"
content_type: "CT05 — Explainer Video"
dimensions: "1920×1080 or 1080×1080"
aspect_ratio: "16:9 or 1:1"
duration: "5–15 minutes"
file_format: "MP4"
upload: "Native upload (not YouTube link)"

caption:
  tone: "Educational"
  length: "100–300 words"
  cta: "Link to full article/protocol in comments"
  captions: "Auto-captions enabled, verify accuracy"
```

---

## PL02: Instagram Adaptations

### Instagram × Static Post

```yaml
platform: "Instagram"
content_type: "CT01 — Static Post"
dimensions: "1080×1350"
aspect_ratio: "4:5"
file_format: "JPG or PNG"

caption:
  tone: "Educational, warm, visual-first"
  length: "100–400 words"
  structure: |
    [Hook line — bold or surprising]
    [2–3 paragraphs of value]
    [CTA — "Save this for later" / "Tag someone who needs this"]
  hashtags:
    count: "25–30"
    placement: "First comment (not in caption)"
    categories:
      brand: ["#Viatrexx", "#BioIncorporated", "#ProtocolAuthority"]
      condition: ["#DrainageFirst", "#MatrixHealing", "#TerrainTheory"]
      audience: ["#NaturopathicDoctor", "#IntegrativeMedicine", "#HolisticHealth"]
      general: ["#RootCause", "#GutHealth", "#DetoxNaturally"]

design_rules:
  safe_zone: "Keep critical text in center 80% of frame"
  three_second_rule: "Visual must trigger pause within 3 seconds"
  text_contrast: "High contrast for readability on mobile"
```

### Instagram × Carousel

```yaml
platform: "Instagram"
content_type: "CT02 — Carousel"
dimensions: "1080×1350"
aspect_ratio: "4:5"
max_slides: 10
file_format: "JPG or PNG per slide"

slide_strategy:
  slide_1: "HOOK — Must trigger immediate pause/swipe signal"
  slides_2_to_8: "VALUE — Teaching, stats, steps, framework, proof"
  slide_9: "SUMMARY — Key takeaway"
  slide_10: "CTA — 'Comment GUIDE for the full protocol' / product link"

caption:
  tone: "Educational AIDA structure"
  length: "200–500 words"
  structure: |
    [Attention: Bold hook restating Slide 1]
    [Interest: Why this matters]
    [Desire: What they'll learn/gain]
    [Action: Save, share, comment keyword]
  hashtags:
    count: "25–30"
    placement: "First comment"

comment_to_dm:
  enabled: true
  keyword: ""                   # e.g., "GUIDE", "PROTOCOL", "DOSING"
  dm_content: ""                # Link to lead magnet or protocol PDF
```

### Instagram × Testimonial

```yaml
platform: "Instagram"
content_type: "CT03 — Testimonial"
dimensions: "1080×1350"
aspect_ratio: "4:5"

design_style: "Authentic, lo-fi 'ugly ad era' aesthetic — real, not polished"
caption:
  tone: "Empathetic, real"
  structure: |
    [Their journey in 2–3 sentences]
    [The quote or result]
    [Soft CTA: "Double tap if you relate"]
```

### Instagram × Reel

```yaml
platform: "Instagram Reels"
content_type: "CT04 — Reel"
dimensions: "1080×1920"
aspect_ratio: "9:16"
duration: "15–90 seconds (sweet spot: 30–60s)"
file_format: "MP4"

hook_rules:
  first_3_seconds: "Must stop the scroll — use text overlay + visual surprise"
  hook_types: ["Question", "Bold claim", "Myth bust", "Before/after", "Relatable pain"]

caption:
  tone: "Casual, direct"
  length: "50–200 words"
  hashtags:
    count: "15–20"
    placement: "In caption (Reels differ from feed posts)"

cover_image: "Custom thumbnail matching brand aesthetic"
audio: "Trending audio when relevant, original VO preferred for authority"

remotion_rendering:
  resolution: "1080×1920"
  fps: 30
  burned_in_captions: true      # Essential for sound-off viewers
  brand_lower_third: true
  end_card_cta: true
```

### Instagram × Infographic

```yaml
platform: "Instagram"
content_type: "CT01 — Infographic variant"
dimensions: "1080×1350"
aspect_ratio: "4:5"

design_rules:
  safe_zone: "Center 80% for text, avoid edges"
  three_second_rule: "High contrast visual hook"
  text_density: "Scannable — bullet points OK on infographics"
  data_viz: "Simple charts, process flows, comparison tables"
```

---

## PL03: LinkedIn Adaptations

### LinkedIn × Static Post

```yaml
platform: "LinkedIn"
content_type: "CT01 — Static Post"
dimensions: "1080×1080"
aspect_ratio: "1:1"
file_format: "JPG or PNG"

caption:
  tone: "B2B, science-forward, authoritative"
  length: "200–600 words"
  structure: |
    [Opening insight or provocative question for practitioners]
    [Data/evidence paragraph]
    [Framework or methodology mention]
    [CTA: "Agree? Share your clinical experience below."]
  identity_signaling: "Speak directly to NDs, MDs, clinic owners, med-spa owners"
```

### LinkedIn × PDF Carousel

```yaml
platform: "LinkedIn"
content_type: "CT02 — Carousel (PDF)"
dimensions: "1080×1080 or A4/Letter"
format: "PDF upload (creates swipeable document)"
max_pages: 10

caption:
  tone: "Professional, thought-leadership"
  length: "200–500 words"
  identity_signaling: "Direct address to target role (NDs, Clinical Directors, etc.)"
  cta: "Download the full protocol — link in comments"

design_rules:
  cover_page: "Bold title + Viatrexx branding"
  interior_pages: "Clean, data-rich, minimal decoration"
  final_page: "CTA + contact/link information"
```

### LinkedIn × Article

```yaml
platform: "LinkedIn"
content_type: "Long-form Article"
format: "Native LinkedIn article"

structure:
  title: "SEO-friendly, B2B focused"
  length: "800–2,000 words"
  tone: "Professional Usefulness format"
  author_bio: "Double-E-A-T framework (credentials, experience, links)"
  cta: "Protocol download, webinar registration, partner program"

seo_notes: "LinkedIn articles are indexed by Google — include target keywords"
```

### LinkedIn × Video

```yaml
platform: "LinkedIn"
content_type: "CT05 — Video"
dimensions: "1920×1080 or 1080×1080"
aspect_ratio: "16:9 or 1:1"
duration: "3–10 minutes optimal"
upload: "Native upload"

caption:
  tone: "B2B, clinical authority"
  captions: "Auto-generated, verify for accuracy"
```

---

## PL04: Pinterest Adaptations

### Pinterest × Standard Pin

```yaml
platform: "Pinterest"
content_type: "CT01 — Standard Pin"
dimensions: "1000×1500"
aspect_ratio: "2:3"
file_format: "JPG or PNG"

description:
  tone: "Keyword-rich, aspirational, educational"
  length: "100–300 characters"
  keywords: "Target unbranded intent (e.g., 'natural scar treatment', 'lymphatic drainage tips')"
  link: "Always link to corresponding blog post or product page"

design_rules:
  safe_zone: "Text in upper 2/3 of pin"
  imagery: "Lo-fi mobile imagery for 8.7× engagement multiplier"
  text_overlay: "Large, readable title text"
  branding: "Subtle Viatrexx logo, not dominant"
```

### Pinterest × Carousel Pin

```yaml
platform: "Pinterest"
content_type: "CT02 — Carousel Pin"
dimensions: "1000×1500"
aspect_ratio: "2:3"
max_slides: 5

description:
  keywords: "Heavy keyword optimization"
  link: "Each slide can link to different URLs"
```

### Pinterest × Video Pin

```yaml
platform: "Pinterest"
content_type: "CT04 — Video Pin"
dimensions: "1080×1920"
aspect_ratio: "9:16 or 2:3"
duration: "15–60 seconds"
file_format: "MP4"

notes: "Auto-plays in feed, must work without sound"
captions: "Burned-in text overlays required"
```

---

## PL05: YouTube Adaptations

### YouTube × Explainer Video

```yaml
platform: "YouTube"
content_type: "CT05 — Explainer Video"
dimensions: "1920×1080"
aspect_ratio: "16:9"
duration: "5–15 minutes"
file_format: "MP4"

optimization:
  title: "SEO-friendly, include primary keyword"
  thumbnail:
    dimensions: "1280×720"
    prompt: ""                  # NanaBanana 2 thumbnail prompt
    rules: "High contrast, readable text, face if possible"
  description:
    structure: |
      [2–3 sentence summary with primary keyword]
      [Timestamps/chapters]
      [Product links]
      [Social media links]
      [Hashtags: 3–5]
    length: "500–1,500 characters"
  tags: "15–30 mix of brand, condition, and general wellness"
  cards: "Place at key moments linking to related content"
  end_screen: "Subscribe button + next video suggestion"

five_three_one_rule:
  description: "For AI-assisted content, ensure human authenticity signals"
  five: "5 seconds of authentic human footage in first 30 seconds"
  three: "3 unique personal anecdotes or clinical examples"
  one: "1 moment of genuine, unscripted reaction"
```

### YouTube × Shorts

```yaml
platform: "YouTube Shorts"
content_type: "CT04 — Short"
dimensions: "1080×1920"
aspect_ratio: "9:16"
duration: "15–60 seconds"
file_format: "MP4"

optimization:
  title: "Short, hook-driven, include keyword"
  description: "Brief, with link to full video if applicable"
  hashtags: "#Shorts + 2–3 relevant tags"

remotion_rendering:
  burned_in_captions: true
  brand_overlay: true
  loop_friendly: "Design for seamless loop if under 30s"
```

### YouTube × Podcast

```yaml
platform: "YouTube"
content_type: "CT07 — Podcast"
dimensions: "1920×1080"
aspect_ratio: "16:9"
duration: "20–60 minutes"

optimization:
  thumbnail: "Guest photo or topic visual"
  timestamps: "Required — full chapter markers"
  description: "Show notes, guest links, product references"
  cards: "Link to mentioned products/protocols at relevant timestamps"

repurpose_via_remotion:
  reel_clips: 3                 # Key moments → Shorts/Reels
  clip_duration: "30–60 seconds each"
```

---

## PL06: Website (Blog) Adaptations

### Website × SEO Blog Post

```yaml
platform: "Website"
content_type: "CT09 — SEO Blog Post"

seo_implementation:
  h1: "[Product/Topic] — [Primary Search Term]"
  h2_h3: "Follow keyword-mapped outline from brief"
  meta_description: "[Problem] + [Solution] + [Viatrexx Difference] (155 characters)"
  url_slug: "keyword-rich, descriptive"
  internal_links: "Minimum 3 within content silo"
  schema_markup: "FAQ, HowTo, or MedicalOrganization as applicable"
  aeo: "Direct answer in first 2 sentences for Google featured snippets"

content_rules:
  word_count: "1,500+ words"
  images: "Minimum 2 with descriptive alt text"
  protocol_bridge: "Call-out box linking to pillar page + product conversion"
  disclaimer: "Mandatory homeopathic disclaimer where required"
  dshea_compliance: "Educational content on separate URL structure from e-commerce"
```

### Website × Podcast Transcript

```yaml
platform: "Website"
content_type: "CT07 — Podcast (Transcript)"

implementation:
  embedded_player: "Audio/video player at top"
  full_transcript: "Below player, formatted with speaker labels"
  seo_optimization: "H2 headers for key topics discussed"
  internal_links: "Link to products/protocols mentioned"
  show_notes: "Summary, guest links, resources"
```

### Website × Video Embed

```yaml
platform: "Website"
content_type: "CT05/CT06 — Video (Embed)"

implementation:
  youtube_embed: "Responsive embed from YouTube upload"
  transcript: "Full text below video for SEO"
  related_content: "Links to related blog posts and products"
```

---

## PL07: Email Adaptations

### Email × Newsletter

```yaml
platform: "Email"
content_type: "CT10 — Email Newsletter"

segments:
  public_b2c:
    tone: "Empathetic, educational"
    subject_prefix: ""
    content_focus: "Root-cause education, lifestyle tips, product discovery"
    cta_style: "Explore, Learn more, Discover"
  practitioners_b2b:
    tone: "Clinical, data-driven"
    subject_prefix: "[Clinical Update]"
    content_focus: "Protocol updates, clinical data, case studies, new products"
    cta_style: "View protocol, Access clinical data, Join webinar"
  partners_b2b:
    tone: "Exclusive, business-focused"
    subject_prefix: "[Partner Exclusive]"
    content_focus: "Wholesale updates, new SKUs, margin data, manufacturing news"
    cta_style: "Order now, Schedule call, Access partner portal"

technical:
  layout: "Mobile-optimized, single column"
  images: "Lightweight, compressed, ALT text required"
  cta_tracking: "UTM parameters on all links"
  subject_line_testing: "A/B test 2 variants minimum"
  send_optimization: "Time-zone optimized delivery"
```

---

## Cross-Platform Quick Reference

| Spec | FB | IG Feed | IG Reel | LI | Pin | YT Video | YT Short |
|------|----|---------|---------|----|-----|----------|----------|
| **Image** | 1080×1080 | 1080×1350 | — | 1080×1080 | 1000×1500 | — | — |
| **Video** | 16:9/1:1 | 4:5 | 9:16 | 16:9/1:1 | 9:16 | 16:9 | 9:16 |
| **Reel/Short** | 1080×1920 | 1080×1920 | 1080×1920 | — | 1080×1920 | — | 1080×1920 |
| **Captions** | Auto | In 1st comment | In caption | In caption | N/A | Description | Description |
| **Hashtags** | 5–10 | 25–30 | 15–20 | 3–5 | Keywords | Tags | #Shorts |
| **Max duration** | — | — | 90s | — | 60s | — | 60s |
| **Burned subs** | Optional | No | Yes | No | Yes | No | Yes |
