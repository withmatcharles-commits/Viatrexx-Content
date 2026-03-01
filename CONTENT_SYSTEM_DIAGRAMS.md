# Viatrexx Content Creation System — Flow Diagram

**Version:** Phase 2 (March 2026)

---

## System Architecture Diagram

```mermaid
graph TB
    subgraph DATABASES["📊 DATABASES"]
        direction TB
        DB_PILLARS["🏛️ Pillars DB<br/>7 Core Pillars<br/>P1–P7"]
        DB_TOPICS["📋 Topics DB<br/>140 Topics<br/>Mapped to Pillars"]
        DB_TYPES["🎬 Content Types DB<br/>12 Content Types<br/>CT01–CT12"]
        DB_PLATFORMS["📱 Platforms DB<br/>7 Platforms<br/>PL01–PL07"]
        DB_CATEGORIES["🏷️ Categories DB<br/>Audience, Condition,<br/>Purpose, Product, SEO"]
        DB_SCHEDULE["📅 Schedule DB<br/>Weekly Calendar<br/>Q1 2026 – Q1 2027"]
        DB_QUEUE["📬 Queue DB<br/>Content Pipeline<br/>Status Tracking"]
    end

    subgraph PLANNING["📝 PLANNING LAYER"]
        WEEKLY["🗓️ Weekly Topic Selection<br/>Pillar + Topic + Week"]
        ASSIGN["📌 Content Assignment<br/>Types × Platforms × Awareness"]
    end

    subgraph BRIEFING["📄 BRIEFING LAYER"]
        BRIEF["✍️ Master Content Brief<br/>One per Topic × Type"]
        BRIEF_STATIC["Brief: Static Post"]
        BRIEF_CAROUSEL["Brief: Carousel"]
        BRIEF_REEL["Brief: Reel/Short"]
        BRIEF_VIDEO["Brief: Explainer Video"]
        BRIEF_PODCAST["Brief: Podcast"]
        BRIEF_BLOG["Brief: SEO Blog"]
        BRIEF_EMAIL["Brief: Email"]
        BRIEF_NLM["Brief: NotebookLM<br/>(Video/Audio/Slides/Infographic)"]
        BRIEF_TESTIMONIAL["Brief: Testimonial"]
    end

    subgraph PRODUCTION["🏭 PRODUCTION LAYER (AI Tools)"]
        direction TB
        NANA["🖼️ NanaBanana 2<br/>━━━━━━━━━━━<br/>• Static images<br/>• Carousel slides<br/>• Thumbnails<br/>• Quote cards<br/>• Pinterest pins<br/>• NLM watermark removal"]
        NLM["🧠 NotebookLM<br/>━━━━━━━━━━━<br/>• Video explainers<br/>• Audio explainers<br/>• Slide decks<br/>• Infographics<br/>• Blog drafts<br/>⚠️ Raw output only"]
        REMOTION["🎬 Remotion MCP<br/>━━━━━━━━━━━<br/>• Reels/Shorts (9:16)<br/>• Explainer videos (16:9)<br/>• Carousel → video<br/>• Animated overlays<br/>• A/B hook variants<br/>• Batch rendering"]
    end

    subgraph POSTPROC["🔧 NLM POST-PROCESSING LAYER"]
        direction TB
        PP_IMG["🖼️ Image Cleanup<br/>NanaBanana 2<br/>━━━━━━━━━━━<br/>Remove watermark<br/>(Infographics & Slides)<br/>Add Viatrexx branding"]
        PP_VID["🎬 Video Cleanup<br/>Remotion MCP + Video API<br/>━━━━━━━━━━━<br/>1. Trim NLM ending<br/>2. Remove video watermark<br/>3. Add branded ending<br/>(Voice AI + Remotion)"]
        PP_AUD["🔊 Audio Cleanup<br/>FFmpeg + Voice AI<br/>━━━━━━━━━━━<br/>1. Trim NLM ending<br/>2. Add branded ending<br/>(Voice AI VO + music)"]
        VOICE["🗣️ Voice AI API<br/>━━━━━━━━━━━<br/>ElevenLabs / Play.ht<br/>Branded ending VO<br/>Match NLM narrator tone"]
    end

    subgraph ADAPTATION["🔄 PLATFORM ADAPTATION"]
        direction TB
        FB["📘 Facebook<br/>1080×1080 / 1080×1920"]
        IG["📸 Instagram<br/>1080×1350 / 1080×1920"]
        LI["💼 LinkedIn<br/>1080×1080 / PDF"]
        PIN["📌 Pinterest<br/>1000×1500"]
        YT["▶️ YouTube<br/>1920×1080 / 1080×1920"]
        WEB["🌐 Website<br/>SEO Blog / Embeds"]
        EMAIL["📧 Email<br/>Segmented Sends"]
    end

    subgraph PUBLISHING["🚀 PUBLISH & TRACK"]
        REVIEW["✅ Quality Gates<br/>Science | Brand | Legal | Visual | SEO"]
        SCHEDULE_PUB["📅 Schedule & Publish"]
        TRACK["📊 Performance Tracking<br/>Impressions | Engagement | Saves | Clicks"]
        REPURPOSE["♻️ Repurpose Pipeline"]
    end

    %% Flow connections
    DB_PILLARS --> WEEKLY
    DB_TOPICS --> WEEKLY
    DB_SCHEDULE --> WEEKLY
    WEEKLY --> ASSIGN
    DB_TYPES --> ASSIGN
    DB_PLATFORMS --> ASSIGN
    DB_CATEGORIES --> ASSIGN

    ASSIGN --> BRIEF
    BRIEF --> BRIEF_STATIC
    BRIEF --> BRIEF_CAROUSEL
    BRIEF --> BRIEF_REEL
    BRIEF --> BRIEF_VIDEO
    BRIEF --> BRIEF_PODCAST
    BRIEF --> BRIEF_BLOG
    BRIEF --> BRIEF_EMAIL
    BRIEF --> BRIEF_NLM
    BRIEF --> BRIEF_TESTIMONIAL

    BRIEF_STATIC --> NANA
    BRIEF_CAROUSEL --> NANA
    BRIEF_TESTIMONIAL --> NANA
    BRIEF_REEL --> REMOTION
    BRIEF_VIDEO --> REMOTION
    BRIEF_NLM --> NLM
    BRIEF_PODCAST --> REMOTION
    BRIEF_CAROUSEL --> REMOTION

    %% NLM Post-Processing flow
    NLM -->|"Infographics & Slides"| PP_IMG
    NLM -->|"Video Explainers"| PP_VID
    NLM -->|"Audio Explainers"| PP_AUD
    VOICE --> PP_VID
    VOICE --> PP_AUD

    %% Clean outputs to platform adaptation
    NANA --> FB
    NANA --> IG
    NANA --> LI
    NANA --> PIN
    PP_IMG --> FB
    PP_IMG --> IG
    PP_IMG --> LI
    PP_IMG --> PIN
    PP_VID --> YT
    PP_VID --> WEB
    PP_VID --> LI
    PP_AUD --> WEB
    REMOTION --> IG
    REMOTION --> YT
    REMOTION --> FB

    BRIEF_BLOG --> WEB
    BRIEF_EMAIL --> EMAIL

    FB --> REVIEW
    IG --> REVIEW
    LI --> REVIEW
    PIN --> REVIEW
    YT --> REVIEW
    WEB --> REVIEW
    EMAIL --> REVIEW

    REVIEW --> SCHEDULE_PUB
    SCHEDULE_PUB --> TRACK
    TRACK --> REPURPOSE
    REPURPOSE --> DB_QUEUE

    DB_QUEUE --> ASSIGN

    %% Styling
    classDef database fill:#E8F4FD,stroke:#2196F3,stroke-width:2px
    classDef planning fill:#FFF3E0,stroke:#FF9800,stroke-width:2px
    classDef briefing fill:#F3E5F5,stroke:#9C27B0,stroke-width:2px
    classDef production fill:#E8F5E9,stroke:#4CAF50,stroke-width:2px
    classDef postproc fill:#FFF9C4,stroke:#F9A825,stroke-width:2px
    classDef platform fill:#FBE9E7,stroke:#FF5722,stroke-width:2px
    classDef publish fill:#E0F2F1,stroke:#009688,stroke-width:2px

    class DB_PILLARS,DB_TOPICS,DB_TYPES,DB_PLATFORMS,DB_CATEGORIES,DB_SCHEDULE,DB_QUEUE database
    class WEEKLY,ASSIGN planning
    class BRIEF,BRIEF_STATIC,BRIEF_CAROUSEL,BRIEF_REEL,BRIEF_VIDEO,BRIEF_PODCAST,BRIEF_BLOG,BRIEF_EMAIL,BRIEF_NLM,BRIEF_TESTIMONIAL briefing
    class NANA,NLM,REMOTION production
    class PP_IMG,PP_VID,PP_AUD,VOICE postproc
    class FB,IG,LI,PIN,YT,WEB,EMAIL platform
    class REVIEW,SCHEDULE_PUB,TRACK,REPURPOSE publish
```

---

## Repurposing Flow Diagram

```mermaid
graph LR
    subgraph SOURCE["📹 Source Content"]
        PODCAST_SRC["Podcast Episode<br/>(60 min)"]
        VIDEO_SRC["Explainer Video<br/>(10 min)"]
        BLOG_SRC["SEO Blog Post<br/>(1,800 words)"]
        CAROUSEL_SRC["Carousel<br/>(10 slides)"]
    end

    subgraph REMOTION_PROC["🎬 Remotion MCP Processing"]
        CLIP["Extract Key Clips"]
        ANIMATE["Animate Slides"]
        RENDER["Multi-Format Render"]
    end

    subgraph NANA_PROC["🖼️ NanaBanana 2 Processing"]
        QUOTE_IMG["Generate Quote Cards"]
        THUMB["Generate Thumbnails"]
        PIN_IMG["Generate Pin Graphics"]
    end

    subgraph NLM_PROC["🧠 NotebookLM Processing"]
        AUDIO_SUM["Audio Summary"]
        SLIDE_GEN["Slide Generation"]
    end

    subgraph OUTPUTS["📤 Repurposed Outputs"]
        REEL_OUT["3× Reels/Shorts<br/>(30–60s each)"]
        QUOTE_OUT["Quote Cards<br/>(Static Posts)"]
        CAROUSEL_VID["Carousel-to-Video<br/>(Animated)"]
        TRANSCRIPT["Blog Transcript<br/>(SEO)"]
        AUDIO_OUT["Audio Clip<br/>(Podcast teaser)"]
        SLIDES_OUT["Slide Deck<br/>(Practitioner)"]
        EMAIL_OUT["Email Excerpt"]
    end

    PODCAST_SRC --> CLIP --> REEL_OUT
    PODCAST_SRC --> QUOTE_IMG --> QUOTE_OUT
    PODCAST_SRC --> TRANSCRIPT
    PODCAST_SRC --> AUDIO_SUM --> AUDIO_OUT
    PODCAST_SRC --> EMAIL_OUT

    VIDEO_SRC --> CLIP
    VIDEO_SRC --> THUMB
    VIDEO_SRC --> SLIDE_GEN --> SLIDES_OUT

    BLOG_SRC --> CAROUSEL_SRC
    BLOG_SRC --> PIN_IMG

    CAROUSEL_SRC --> ANIMATE --> CAROUSEL_VID
    CAROUSEL_SRC --> RENDER --> REEL_OUT
```

---

## Content Queue State Machine

```mermaid
stateDiagram-v2
    [*] --> IDEATION : Topic identified
    IDEATION --> QUEUED : Assigned to calendar
    QUEUED --> BRIEF_CREATED : Master brief written
    BRIEF_CREATED --> IN_PRODUCTION : Assets generation started
    IN_PRODUCTION --> IN_REVIEW : Production complete
    IN_REVIEW --> READY : Approved
    IN_REVIEW --> IN_PRODUCTION : Revisions requested
    READY --> SCHEDULED : Loaded in scheduler
    SCHEDULED --> LIVE : Published
    LIVE --> ARCHIVED : Performance logged

    ARCHIVED --> IDEATION : Repurpose trigger
```

---

## NotebookLM Post-Processing Pipeline Diagram

```mermaid
graph TB
    subgraph NLM_OUT["🧠 NotebookLM Raw Outputs"]
        NLM_INFOG["📊 Infographic<br/>⚠️ Watermark (bottom-right)"]
        NLM_SLIDES["📑 Slide Deck<br/>⚠️ Watermark (each slide)"]
        NLM_VIDEO["🎬 Video Explainer<br/>⚠️ Watermark + NLM Ending"]
        NLM_AUDIO["🔊 Audio Explainer<br/>⚠️ NLM Ending"]
    end

    subgraph IMG_PIPE["🖼️ Image Pipeline"]
        IMG_EXPORT["Export as PNG/JPG"]
        IMG_NANA["NanaBanana 2<br/>Inpaint/remove<br/>bottom-right watermark"]
        IMG_BRAND["Optional: Add<br/>Viatrexx footer/logo"]
        IMG_ASSEMBLE["Re-assemble<br/>(slides only)"]
    end

    subgraph VID_PIPE["🎬 Video Pipeline"]
        VID_TRIM["Step 1: Trim NLM Ending<br/>Remotion MCP / FFmpeg"]
        VID_WM["Step 2: Remove Watermark<br/>Video Inpainting API<br/>or Remotion Overlay<br/>or FFmpeg delogo"]
        VID_VOICE["Step 3: Generate Ending VO<br/>🗣️ Voice AI API<br/>(ElevenLabs / Play.ht)"]
        VID_ENDING["Step 4: Compose Ending<br/>🎬 Remotion MCP<br/>VO + Logo + CTA<br/>(8–15 seconds)"]
        VID_STITCH["Step 5: Final Stitch<br/>Remotion MCP<br/>Cleaned video + ending"]
    end

    subgraph AUD_PIPE["🔊 Audio Pipeline"]
        AUD_TRIM["Step 1: Trim NLM Ending<br/>FFmpeg"]
        AUD_VOICE["Step 2: Generate Ending VO<br/>🗣️ Voice AI API"]
        AUD_STITCH["Step 3: Stitch<br/>FFmpeg / Remotion<br/>+ optional music bed"]
    end

    subgraph FINAL["✅ Publish-Ready"]
        FINAL_IMG["Clean Infographic"]
        FINAL_SLIDES["Clean Slide Deck"]
        FINAL_VID["Branded Video Explainer"]
        FINAL_AUD["Branded Audio Explainer"]
    end

    NLM_INFOG --> IMG_EXPORT --> IMG_NANA --> IMG_BRAND --> FINAL_IMG
    NLM_SLIDES --> IMG_EXPORT
    IMG_BRAND --> IMG_ASSEMBLE --> FINAL_SLIDES

    NLM_VIDEO --> VID_TRIM --> VID_WM --> VID_ENDING --> VID_STITCH --> FINAL_VID
    VID_VOICE --> VID_ENDING

    NLM_AUDIO --> AUD_TRIM --> AUD_STITCH --> FINAL_AUD
    AUD_VOICE --> AUD_STITCH

    classDef nlm fill:#FFECB3,stroke:#FF8F00,stroke-width:2px
    classDef imgpipe fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px
    classDef vidpipe fill:#E3F2FD,stroke:#1565C0,stroke-width:2px
    classDef audpipe fill:#F3E5F5,stroke:#7B1FA2,stroke-width:2px
    classDef final fill:#E0F2F1,stroke:#00695C,stroke-width:2px
    classDef voice fill:#FCE4EC,stroke:#C62828,stroke-width:2px

    class NLM_INFOG,NLM_SLIDES,NLM_VIDEO,NLM_AUDIO nlm
    class IMG_EXPORT,IMG_NANA,IMG_BRAND,IMG_ASSEMBLE imgpipe
    class VID_TRIM,VID_WM,VID_ENDING,VID_STITCH vidpipe
    class AUD_TRIM,AUD_STITCH audpipe
    class VID_VOICE,AUD_VOICE voice
    class FINAL_IMG,FINAL_SLIDES,FINAL_VID,FINAL_AUD final
```

---

## AI Tool Decision Tree

```mermaid
graph TD
    START["Content Brief Ready"] --> TYPE_CHECK{"What content type?"}

    TYPE_CHECK -->|"Static Post<br/>Carousel<br/>Testimonial<br/>Thumbnail<br/>Pin"| NANA["🖼️ NanaBanana 2<br/>Image Generation"]

    TYPE_CHECK -->|"Reel/Short<br/>Explainer Video<br/>Carousel-to-Video<br/>Ad Variants"| REMOTION["🎬 Remotion MCP<br/>Video Rendering"]

    TYPE_CHECK -->|"Video Explainer<br/>Audio Explainer<br/>Slide Deck<br/>Infographic"| NLM["🧠 NotebookLM<br/>Knowledge-Based Gen"]

    TYPE_CHECK -->|"SEO Blog<br/>Email Newsletter"| WRITING["✍️ AI Writing<br/>+ Human Edit"]

    TYPE_CHECK -->|"Podcast"| RECORD["🎙️ Recording<br/>+ Remotion Post"]

    NANA --> ADAPT["🔄 Platform Adaptation"]
    REMOTION --> ADAPT
    NLM --> ADAPT
    WRITING --> ADAPT
    RECORD --> ADAPT

    ADAPT --> REVIEW["✅ Quality Gates"]
    REVIEW -->|Pass| PUBLISH["🚀 Publish"]
    REVIEW -->|Fail| REVISE["🔧 Revise"] --> ADAPT
```
