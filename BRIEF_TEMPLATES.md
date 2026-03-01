# Viatrexx Content Brief Templates

**Version:** Phase 2 (March 2026)
**Usage:** AI agents and content creators use these templates to generate Master Content Briefs for each content type. One brief per Topic × Content Type.

---

## Universal Brief Header (Required for ALL types)

```yaml
# === MASTER CONTENT BRIEF ===
brief_id: ""                    # Format: BRIEF-{year}-W{week}-{content_type}-{seq}
topic_id: ""                    # Reference to Topic Database
pillar: ""                      # P1–P7
topic_title: ""                 # From Topic Database
awareness_level: ""             # TOFU / MOFU / BOFU
target_audience: ""             # B2B / B2C / Both
primary_seo_keywords: []        # 3–5 keywords
secondary_keywords: []          # 5–10 long-tail phrases
condition_cluster: ""           # CC code from Categories
products_referenced: []         # Specific Viatrexx products mentioned
regulatory_notes: ""            # Any compliance considerations
scientific_sources: []          # Sources for claims verification

# === SCIENTIFIC ACCURACY CHECKLIST ===
# [ ] All claims verified against product monographs
# [ ] No forbidden language (cure, always, never, guaranteed)
# [ ] Mandatory disclaimers included where required
# [ ] TCM/emotional claims properly qualified
# [ ] Visual audit passed (no stethoscopes, no "cured" imagery)
```

---

## CT01: Static Post / Infographic Brief

```yaml
type: "CT01 — Static Post / Infographic"

# CREATIVE
headline: ""                    # 5–7 words max
core_message: ""                # 1 key takeaway (1–2 sentences)
visual_direction: ""            # Description of desired visual style
image_generation_prompt: ""     # NanaBanana 2 prompt (detailed, brand-aligned)
  # Style: Clean, clinical-yet-warm, nature-meets-science
  # Colors: Brand palette (deep teal, gold accents, white space)
  # Avoid: Stock clichés, stethoscopes, "cured" imagery
  # Include: Nature elements, prism/light motifs, cellular patterns
color_palette: ""               # Specific hex codes if needed
text_overlay: ""                # Any text to appear on image

# COPY
caption_draft: ""               # 2–3 paragraphs per platform tone
cta: ""                         # e.g., "Save this", "Link in bio", "Comment GUIDE"
hashtags: []                    # 25–30 for IG, fewer for other platforms

# PLATFORM VARIANTS
variants:
  facebook:
    dimensions: "1080×1080"
    caption_tone: "Professional, community-focused"
  instagram:
    dimensions: "1080×1350"
    caption_tone: "Visual-first, educational"
  linkedin:
    dimensions: "1080×1080"
    caption_tone: "B2B, science-forward"
  pinterest:
    dimensions: "1000×1500"
    caption_tone: "Keyword-rich, aspirational"
```

---

## CT02: Carousel Brief

```yaml
type: "CT02 — Carousel"

# CREATIVE
slide_count: 10                 # 5–10 slides
slides:
  - slide_number: 1
    purpose: "HOOK"
    headline: ""                # 3-second rule: must trigger pause/swipe
    visual_notes: ""
    image_prompt: ""            # NanaBanana 2 prompt
  - slide_number: 2
    purpose: "PROBLEM"
    headline: ""
    body_text: ""
    visual_notes: ""
    image_prompt: ""
  - slide_number: 3
    purpose: "VALUE"
    headline: ""
    body_text: ""
    visual_notes: ""
    image_prompt: ""
  # ... slides 4–8: VALUE delivery (stats, steps, framework, proof)
  - slide_number: 9
    purpose: "SUMMARY"
    headline: ""
    body_text: ""
    visual_notes: ""
    image_prompt: ""
  - slide_number: 10
    purpose: "CTA"
    headline: ""
    cta_text: ""                # e.g., "Comment GUIDE for the full protocol"
    product_reference: ""
    visual_notes: ""
    image_prompt: ""

# COPY
caption_draft: ""               # 2–3 paragraphs
cta: ""
hashtags: []

# PLATFORM VARIANTS
variants:
  facebook:
    dimensions: "1080×1080"
    max_slides: 10
  instagram:
    dimensions: "1080×1350"
    max_slides: 10
    hashtag_placement: "first comment"
  linkedin:
    dimensions: "1080×1080"
    format: "PDF upload or native carousel"
  pinterest:
    dimensions: "1000×1500"
    notes: "Individual pins linking to blog"

# REPURPOSE
carousel_to_video: true         # Flag for Remotion MCP conversion
video_duration_target: "30–60s" # Reel version
```

---

## CT03: Testimonial / Quote Post Brief

```yaml
type: "CT03 — Testimonial / Quote Post"

# CONTENT
quote_text: ""                  # Exact quote from source
quote_source: ""                # Name, title, credentials
source_type: ""                 # "practitioner" / "patient" / "partner"
transformation_summary: ""      # Brief before/after narrative
authenticity_verified: false    # Must be true before publish

# CREATIVE
image_generation_prompt: ""     # NanaBanana 2 quote card design
visual_style: ""                # "Professional trust-building" / "Authentic lo-fi"
background_treatment: ""        # Solid color, gradient, nature imagery

# COPY
caption_draft: ""
cta: ""                         # Soft CTA: "Have you experienced this?"

# PLATFORM VARIANTS
variants:
  facebook:
    dimensions: "1080×1080"
    notes: "Pin peer social proof in comments"
  instagram:
    dimensions: "1080×1350"
    notes: "Authentic, lo-fi 'ugly ad era' aesthetic"
  linkedin:
    dimensions: "1080×1080"
    notes: "Professional transformation narrative"
  pinterest:
    dimensions: "1000×1500"
    notes: "Tall inspirational graphic"
```

---

## CT04: Reel / Short Brief

```yaml
type: "CT04 — Reel / Short"

# VIDEO
duration_seconds: 45            # 15–90 seconds (sweet spot: 30–60)
format_type: ""                 # quick_tip / myth_buster / product_demo / before_after / protocol_snippet / talking_head
aspect_ratio: "9:16"
resolution: "1080×1920"

# SCRIPT
hook: ""                        # First 3 seconds — must stop scroll
  # Hook types: Question, bold statement, myth, relatable pain, visual surprise
body_segments:
  - timestamp: "0:03"
    content: ""
    visual: ""                  # What's on screen
    text_overlay: ""            # Animated text
  - timestamp: "0:15"
    content: ""
    visual: ""
    text_overlay: ""
  # ... additional segments
cta_end: ""                     # Final 3–5 seconds: CTA overlay
  # Options: "Follow for more", "Comment GUIDE", "Save this", "Link in bio"

# AUDIO
voiceover_script: ""            # Full VO script
music_bed: ""                   # Style/mood for background music
sound_effects: []               # Any specific SFX needed

# REMOTION MCP
remotion_composition: ""        # Description for Remotion rendering
input_assets: []                # Images, footage clips, product shots
text_animations: []             # Animated text overlays and timings
brand_elements:                 # Standard brand overlays
  lower_third: true             # Viatrexx branding bar
  end_card: true                # CTA end card
  logo_watermark: true          # Small logo placement

# A/B TESTING (3-2-2 Method)
hook_variants:
  - variant_a: ""               # Hook version A
  - variant_b: ""               # Hook version B
  - variant_c: ""               # Hook version C

# PLATFORM DISTRIBUTION
platforms:
  - platform: "Instagram Reels"
    caption: ""
    hashtags: []
  - platform: "YouTube Shorts"
    title: ""
    description: ""
  - platform: "Facebook Reels"
    caption: ""
```

---

## CT05: Explainer Video Brief

```yaml
type: "CT05 — Explainer Video"

# VIDEO
duration_minutes: 10            # 5–15 minutes
aspect_ratio: "16:9"
resolution: "1920×1080"

# TITLES & THUMBNAIL
title_options:                  # 3 SEO-friendly options
  - ""
  - ""
  - ""
thumbnail_concept: ""           # Description for NanaBanana 2
thumbnail_prompt: ""            # NanaBanana 2 image prompt

# SCRIPT OUTLINE
intro:
  hook: ""                      # First 30 seconds — must retain viewer
  context: ""                   # Problem/context setup (1–2 min)
core_points:
  - point_number: 1
    title: ""
    key_message: ""
    visual_treatment: ""        # Whiteboard, slides, B-roll, animation
    timestamp_start: ""
  - point_number: 2
    title: ""
    key_message: ""
    visual_treatment: ""
    timestamp_start: ""
  - point_number: 3
    title: ""
    key_message: ""
    visual_treatment: ""
    timestamp_start: ""
  # ... up to 5 core points
conclusion:
  summary: ""
  cta: ""                       # Subscribe, visit website, download protocol
  next_video_tease: ""

# YOUTUBE OPTIMIZATION
description_draft: ""           # With keyword-rich text, links, timestamps
tags: []                        # Mix of brand, condition, general
cards: []                       # In-video card placements
end_screen: ""                  # Subscribe + next video

# REMOTION MCP (if composited)
remotion_notes: ""              # Animated diagrams, text overlays, transitions
input_assets: []                # Slides, diagrams, footage, product shots

# REPURPOSE
reel_clips:                     # Key moments to extract as Reels
  - clip_timestamp: ""
    clip_duration: ""
    reel_hook: ""
```

---

## CT06: Video Explainer (NotebookLM) Brief

```yaml
type: "CT06 — Video Explainer (NotebookLM)"

# SOURCE MATERIAL
notebooklm_sources: []          # Document paths to upload to NotebookLM
  # e.g., Protocol document, brand guide section, product monograph
focus_topic: ""                 # Specific angle to cover
target_duration_minutes: 5      # 3–10 minutes

# GUIDANCE
key_points_to_cover: []         # Priority points for the AI to address
tone: ""                        # "Educational overview" / "Clinical deep-dive"
audience_level: ""              # "Beginner-friendly" / "Practitioner-level"

# POST-PROCESSING (Required — NLM outputs are NOT publish-ready)
post_processing:
  watermark_removal:
    tool: "Video inpainting API or Remotion MCP overlay"
    location: "Bottom-right corner"
    method: ""                  # "inpainting_api" / "remotion_overlay" / "ffmpeg_delogo"
    # Options:
    #   inpainting_api: Use external video watermark removal service
    #   remotion_overlay: Cover with branded lower-third bar
    #   ffmpeg_delogo: Use FFmpeg delogo filter (simple overlays only)

  ending_trim:
    tool: "Remotion MCP / FFmpeg"
    action: "Detect and remove NotebookLM branded outro segment"
    trim_method: ""             # "manual_timestamp" / "auto_detect"
    trim_point: ""              # Timestamp where NLM outro begins (if known)

  branded_ending:
    tool: "Remotion MCP + Voice AI API"
    duration_seconds: 10        # 8–15 seconds
    ending_template: ""         # "general" / "b2b_practitioner" / "b2c_seeker" / "condition_specific"
    # See CONTENT_CREATION_FLOW.md Section 4.3.4 for ending script templates
    voiceover_script: ""        # Custom script, or leave blank to use template
    cta_text: ""                # On-screen CTA text
    cta_url: ""                 # URL to display
    product_reference: ""       # Product/protocol to feature in CTA

  voice_ai:
    api: ""                     # "elevenlabs" / "playht" / "amazon_polly" / "google_tts"
    voice_style: "Warm, clinical, authoritative — not salesy"
    match_nlm_narrator: true    # Attempt to match the NLM narrator gender/tone
    output_format: "WAV 44.1kHz"

# OUTPUT
publish_platforms: []           # YouTube, Website, LinkedIn
final_render_format: "MP4 1920×1080 30fps"
```

---

## CT07: Podcast Episode Brief

```yaml
type: "CT07 — Podcast Episode"

# EPISODE
title_options:
  - ""
  - ""
  - ""
episode_type: ""                # solo / interview / panel / case_study
guest_info:                     # If interview
  name: ""
  credentials: ""
  bio: ""
thumbnail_prompt: ""            # NanaBanana 2 for video version

# OUTLINE
intro:
  topic_framing: ""             # 2 minutes
  guest_intro: ""               # If applicable
discussion_points:
  - point: ""
    key_questions: []
    target_duration_minutes: 0
  - point: ""
    key_questions: []
    target_duration_minutes: 0
  # ... up to 5 discussion points
conclusion:
  key_takeaways: []
  cta: ""
  next_episode_tease: ""

# DISTRIBUTION
youtube_description: ""
website_show_notes: ""
email_excerpt: ""               # For newsletter inclusion
transcript_to_blog: true        # Flag for SEO blog conversion

# REPURPOSE
reel_clips:                     # Key moments for Reels (via Remotion MCP)
  - clip_description: ""
    estimated_timestamp: ""
quote_cards: []                 # Key quotes for NanaBanana 2 → static posts
```

---

## CT08: Audio Explainer (NotebookLM) Brief

```yaml
type: "CT08 — Audio Explainer (NotebookLM)"

# SOURCE MATERIAL
notebooklm_sources: []
focus_topic: ""
target_duration_minutes: 8      # 5–15 minutes

# GUIDANCE
key_points_to_cover: []
tone: "Conversational podcast-style"
audience_level: ""

# POST-PROCESSING (Required — NLM outputs are NOT publish-ready)
post_processing:
  ending_trim:
    tool: "FFmpeg / audio editor"
    action: "Detect and remove NotebookLM branded audio outro"
    trim_point: ""              # Timestamp where NLM outro begins (if known)

  branded_ending:
    tool: "Voice AI API + FFmpeg / Remotion MCP"
    duration_seconds: 12        # 8–15 seconds
    ending_template: ""         # "general" / "condition_specific"
    # See CONTENT_CREATION_FLOW.md Section 4.3.4 for ending script templates
    voiceover_script: ""        # Custom script, or leave blank to use template
    music_bed: ""               # Optional subtle music sting for sign-off
    product_reference: ""       # Product/protocol to mention in CTA

  voice_ai:
    api: ""                     # "elevenlabs" / "playht" / "amazon_polly" / "google_tts"
    voice_style: "Warm, clinical, authoritative — not salesy"
    match_nlm_narrator: true    # Attempt to match the NLM narrator gender/tone
    output_format: "WAV 44.1kHz"

# OUTPUT
publish_platforms: []           # Website, Email (linked)
transcript_to_blog: true
final_render_format: "MP3 192kbps"
```

---

## CT09: SEO Blog Post Brief

```yaml
type: "CT09 — SEO Blog Post"

# SEO
target_keyword_primary: ""      # Tier 1–3
target_keywords_secondary: []   # 5–10 long-tail phrases
search_intent: ""               # informational / transactional / navigational
word_count_target: 1800         # Minimum 1,500

# STRUCTURE
h1_title: ""                    # [Topic] — [Primary Search Term]
outline:
  - h2: ""
    h3s: []
    key_points: []
  - h2: ""
    h3s: []
    key_points: []
  # ... additional sections

# SEO IMPLEMENTATION
meta_description: ""            # [Problem] + [Solution] + [Viatrexx Difference]
internal_links_planned: []      # Silo strategy links
external_references: []         # Authoritative sources to cite
schema_type: ""                 # FAQ, HowTo, MedicalOrganization
aeo_answer: ""                  # Direct answer in first 2 sentences (for Google snippets)

# MEDIA
featured_image_prompt: ""       # NanaBanana 2 hero image
alt_text: ""                    # Descriptive, keyword-rich

# CTA
primary_cta: ""                 # Email signup, product link, protocol download
protocol_bridge: ""             # Call-out box linking to pillar page + product
```

---

## CT10: Email Newsletter Brief

```yaml
type: "CT10 — Email Newsletter"

# SEGMENTATION
segments:
  - segment: "Public (B2C)"
    tone: "Empathetic, educational"
    focus: ""
  - segment: "Practitioners (B2B)"
    tone: "Clinical, data-driven"
    focus: ""
  - segment: "Partners (B2B)"
    tone: "Exclusive, business-focused"
    focus: ""

# CONTENT
subject_line_options:           # 3–5 options for A/B testing
  - ""
  - ""
  - ""
preview_text: ""
body_structure:
  recap: ""                     # This week's content summary
  education: ""                 # Key insight or protocol tip
  promotion: ""                 # Product spotlight or offer
  cta: ""                       # Clear, tracked link

# TECHNICAL
utm_parameters: ""
mobile_optimized: true
send_date: ""
send_time: ""                   # Optimal by segment
```

---

## CT11: Slide Deck (NotebookLM) Brief

```yaml
type: "CT11 — Slide Deck (NotebookLM)"

# SOURCE MATERIAL
notebooklm_sources: []
focus_topic: ""
target_slide_count: 15          # 10–25 slides

# GUIDANCE
key_points_to_cover: []
audience: ""                    # "Practitioner webinar" / "Patient education"
visual_style: ""                # Brand-aligned, clean, clinical-yet-warm

# POST-PROCESSING (Required — NLM outputs are NOT publish-ready)
post_processing:
  watermark_removal:
    tool: "NanaBanana 2"
    location: "Bottom-right corner of each slide"
    workflow:
      - "Export each slide as individual PNG/JPG"
      - "NanaBanana 2: inpaint/remove bottom-right NLM watermark"
      - "Optional: Add Viatrexx branded footer/logo in cleaned area"
      - "Re-assemble cleaned slides into final presentation"
  brand_replacement:
    add_viatrexx_footer: true   # Add subtle Viatrexx logo where watermark was
    footer_style: ""            # "logo_only" / "logo_with_url" / "none"

# OUTPUT
publish_platforms: []           # LinkedIn (PDF), Website, Email (attachment)
final_format: "PDF or PPTX"
```

---

## CT12: Infographic (NotebookLM) Brief

```yaml
type: "CT12 — Infographic (NotebookLM)"

# SOURCE MATERIAL
notebooklm_sources: []
focus_topic: ""
infographic_type: ""            # flowchart / comparison / timeline / statistics / process

# GUIDANCE
data_points: []                 # Key data/stats to visualize
visual_style: ""                # Brand-aligned
dimensions_target: ""           # Varies by platform use

# POST-PROCESSING (Required — NLM outputs are NOT publish-ready)
post_processing:
  watermark_removal:
    tool: "NanaBanana 2"
    location: "Bottom-right corner"
    workflow:
      - "NanaBanana 2: inpaint/remove bottom-right NLM watermark"
      - "Optional: Add Viatrexx branded footer/logo in cleaned area"
  brand_replacement:
    add_viatrexx_footer: true   # Add subtle Viatrexx logo where watermark was
    footer_style: ""            # "logo_only" / "logo_with_url" / "none"

# OUTPUT
publish_platforms: []           # FB, IG, LI, Pin, Website, Email
final_format: "PNG or JPG"
```
