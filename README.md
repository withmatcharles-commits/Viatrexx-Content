# Viatrexx Content System

**Version:** Phase 2 (March 2026)
**Purpose:** AI Agent-ready content creation system for Viatrexx Bio Inc.

---

## Overview

This repository contains the complete content creation system for Viatrexx Bio Inc., designed for use by AI agents and human content creators. It provides structured databases, templates, workflows, and diagrams to produce on-brand content that positions Viatrexx as the Protocol Authority in integrative medicine.

### Key Phase 2 Updates
- Added **Reels / Shorts** (15–90s vertical video) as a content type
- Added **Remotion MCP** integration for programmatic video rendering
- Added **NanaBanana 2** integration for AI image and carousel generation
- Added **NotebookLM** integration for knowledge-based content (video explainers, audio explainers, slides, infographics)
- Expanded content types from 7 to 12
- Added content queue system with status tracking
- Added comprehensive tagging and categorization schema

---

## Repository Structure

```
viatrexx-content-system/
├── README.md                           ← You are here
├── AGENT_INSTRUCTIONS.md               ← AI agent operating guide
│
├── docs/
│   ├── CONTENT_CREATION_FLOW.md        ← Master workflow (start here)
│   ├── DATABASE_PILLARS.md             ← 7 Core Topic Pillars
│   ├── DATABASE_CONTENT_TYPES.md       ← 12 Content Types (CT01–CT12)
│   ├── DATABASE_PLATFORMS.md           ← 7 Platforms (PL01–PL07)
│   └── DATABASE_SCHEDULE_QUEUE_CATEGORIES.md  ← Schedule, Queue, Categories
│
├── templates/
│   ├── briefs/
│   │   └── BRIEF_TEMPLATES.md          ← Master Brief templates per content type
│   └── platforms/
│       └── PLATFORM_TEMPLATES.md       ← Platform adaptation templates
│
├── diagrams/
│   └── CONTENT_SYSTEM_DIAGRAMS.md      ← Mermaid flow diagrams
│
└── reference/
    ├── brand-identity/                 ← Brand guides (source docs)
    ├── seo-keywords/                   ← SEO keyword plans (source docs)
    ├── protocols/                      ← Therapeutic protocols (source docs)
    └── topics/                         ← Topic databases (source docs)
```

---

## Quick Start for AI Agents

1. **Read** `AGENT_INSTRUCTIONS.md` for operating context
2. **Read** `docs/CONTENT_CREATION_FLOW.md` for the full workflow
3. **Select** topic from `docs/DATABASE_PILLARS.md` + weekly schedule
4. **Choose** content types from `docs/DATABASE_CONTENT_TYPES.md`
5. **Create** master brief using `templates/briefs/BRIEF_TEMPLATES.md`
6. **Adapt** for platforms using `templates/platforms/PLATFORM_TEMPLATES.md`
7. **Generate** assets using the appropriate AI tool (Remotion MCP / NanaBanana 2 / NotebookLM)

---

## AI Tool Integration

| Tool | Purpose | Content Types |
|------|---------|--------------|
| **Remotion MCP** | Programmatic video rendering, NLM video post-processing | Reels/Shorts, Explainer Videos, Carousel-to-Video, Ad variants, NLM video ending composition |
| **NanaBanana 2** | AI image generation, NLM image watermark removal | Static posts, Carousel slides, Thumbnails, Quote cards, Pins, NLM Infographic/Slide watermark removal |
| **NotebookLM** | Knowledge-based content generation (requires post-processing) | Video Explainers, Audio Explainers, Slide Decks, Infographics |
| **Voice AI API** | Branded ending voiceover generation | NLM Video/Audio Explainer ending replacements |
| **FFmpeg** | Video/audio trimming, stitching | NLM ending removal, audio assembly |

> **⚠️ Important:** All NotebookLM outputs require post-processing before publishing — watermark removal (images), ending replacement (video/audio), and Viatrexx branding. See `AGENT_INSTRUCTIONS.md` and `docs/CONTENT_CREATION_FLOW.md` Section 4.3 for full pipelines.

---

## Content Volume (Weekly Phase 2)

| Content Type | Count | Primary Platforms |
|-------------|-------|-------------------|
| Static Post / Infographic | 3 | FB, IG, LI, Pin |
| Carousel | 2 | FB, IG, LI, Pin |
| Testimonial | 1 | FB, IG, LI |
| Reel / Short | 3 | IG, YT, FB |
| Explainer Video | 2 | YT, FB, LI |
| Podcast | 2 | YT, Web, Audio |
| SEO Blog Post | 1 | Website |
| Email Newsletter | 1 | Email |
| **Total** | **15/week** | |

Plus monthly NotebookLM content (2 video explainers, 2 audio explainers, 1 slide deck, 2 infographics).

---

## Brand Voice Quick Reference

**Tone:** Clinical but compassionate
**Avoid:** "Miracle cure" language, marketing fluff, forbidden claims
**Forbidden words:** "Cure," "Always," "Never," "Guaranteed"
**Required language:** "Supports," "Promotes," "Assists"
**Voice:** Authoritative peer (to practitioners), professional guide (to seekers)
