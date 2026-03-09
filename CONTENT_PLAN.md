# Viatrexx Content Plan — Updated System Design

**Version:** 2.2 (March 2026)

---

## 1. Phased Rollout Strategy

### Phase 1: Image-Based Posts (Launch)

**Content Types (7 pieces/week):**

| Piece | Content Type | Awareness Level | Day Pattern (see rotation) |
|-------|-------------|----------------|---------------------------|
| SP1 | Static Post / Infographic | TOFU (Unaware) | Varies by week pattern |
| SP2 | Static Post / Infographic | MOFU (Problem-aware) | Varies by week pattern |
| SP3 | Static Post / Infographic | BOFU (Solution-aware) | Varies by week pattern |
| INF1 | Infographic (Data Visual) | TOFU–MOFU | Varies by week pattern |
| INF2 | Infographic (Data Visual) | MOFU–BOFU | Varies by week pattern |
| CAR1 | Carousel (5–10 slides) | TOFU→MOFU | Varies by week pattern |
| CAR2 | Carousel (5–10 slides) | MOFU→BOFU | Varies by week pattern |

**Platforms:** Facebook, Instagram, LinkedIn, Pinterest

---

### Phase 2: Blog, Audio/Video Overviews & Social Proof (Add-on)

**Weekly Content Production:**

| Piece | Content Type | Notes |
|-------|-------------|-------|
| BLOG1–3 | SEO Blog Post (Core) | 3 original long-form articles |
| AO1–2 | Audio Overview (NotebookLM/Gemini) | 2 AI-generated audio explainers |
| VO1–2 | Video Overview (NotebookLM/Gemini) | 2 AI-generated video explainers |
| BLOG4–7 | Blog Post (Companion) | 4 posts from AO/VO transcripts |

**Total: 7 Blog Posts + 2 Audio + 2 Video = 11 content pieces/week**

**Blog Promo Social Posts (7 per blog × 3 platforms):**

| Piece | Platforms | Link Target |
|-------|-----------|-------------|
| BP1–BP7 | FB, IG, LI | Blog post URL |

**Pinterest Blog Pins (Core 3 only):**

| Piece | Link Target |
|-------|-------------|
| PIN1–PIN3 | Core blog post URLs |

**Phase 2 Weekly Totals:** 24 social posts + 7 blogs + 2 audio + 2 video

---

### Phase 3: Short-Form Video & Stories (Add-on)

| Piece | Frequency | Platforms |
|-------|-----------|-----------|
| REEL1–7 | 1 per day (7/week) | IG Reels, FB Reels, YT Shorts |
| STORY×5 | 5 per day, every day (35/week) | IG Stories, FB Stories |

---

### Phase 4: AI Podcast (Add-on)

| Piece | Content Type | Awareness Level |
|-------|-------------|----------------|
| POD1 | AI Podcast Episode (Voice AI) | TOFU→MOFU |
| POD2 | AI Podcast Episode (Voice AI) | MOFU→BOFU |

**Distribution:** YouTube, Website (transcript), Spotify, Apple Podcasts, RSS, Email

---

## 2. Weekly Posting Rotation (Phase 1)

Patterns cycle A→B→C→D→A→... so content types land on different days each month.

### Pattern A

| Day | Content |
|-----|---------|
| Monday | SP1 (TOFU) |
| Tuesday | INF1 (TOFU/MOFU) |
| Wednesday | SP2 (MOFU) |
| Thursday | CAR1 (TOFU→MOFU) |
| Friday | SP3 (BOFU) |
| Saturday | INF2 (MOFU/BOFU) |
| Sunday | CAR2 (MOFU→BOFU) |

### Pattern B

| Day | Content |
|-----|---------|
| Monday | CAR1 | Tuesday | SP1 | Wednesday | INF1 | Thursday | SP2 | Friday | CAR2 | Saturday | SP3 | Sunday | INF2 |

### Pattern C

| Day | Content |
|-----|---------|
| Monday | INF1 | Tuesday | CAR1 | Wednesday | SP1 | Thursday | INF2 | Friday | CAR2 | Saturday | SP2 | Sunday | SP3 |

### Pattern D

| Day | Content |
|-----|---------|
| Monday | SP2 | Tuesday | CAR2 | Wednesday | INF2 | Thursday | SP1 | Friday | INF1 | Saturday | CAR1 | Sunday | SP3 |

**Rotation Assignment:** Cycles across the 7-week pillar rotation, then repeats.

---

## 3. Pillar Rotation (7-Week Cycle)

```
Week N+0: P1 — Brand Philosophy & Origins
Week N+1: P2 — Product Education & Usage
Week N+2: P5 — Detoxification, Repair, & Regeneration
Week N+3: P3 — Integrative & Holistic Health
Week N+4: P4 — Metabolic Factors & Optimization
Week N+5: P6 — Services for Practitioners (B2B)
Week N+6: P7 — Innovative Manufacturing
→ Repeat
```

---

## 4. Image Optimization Strategy

Platforms that share the same dimensions use the **same image file**.

| Group | Dimensions | Platforms |
|-------|-----------|-----------|
| **Group A** | 1080×1080 (1:1) | Facebook + LinkedIn |
| **Group B** | 1080×1350 (4:5) | Instagram |
| **Group C** | 1000×1500 (2:3) | Pinterest |

**Phase 1 Weekly Image Totals:**

| Content | Pieces | Images/Piece | Total |
|---------|--------|-------------|-------|
| Static Posts (SP1–3) | 3 | 3 | 9 |
| Infographics (INF1–2) | 2 | 3 | 6 |
| Carousels (CAR1–2) × 10 slides | 2 | 30 | 60 |
| **TOTAL** | **7** | — | **75** |

Product images from GHL are composited via Remotion MCP without additional NanaBanana calls.

---

## 5. AI Tool & Agent Assignments

| Role | Tool / Model | Used For |
|------|-------------|----------|
| Planning & Strategy | Claude (Anthropic API) | Master Brief strategy, content planning |
| Review & QA | Claude (Anthropic API) | 16-point review checklist, revision instructions |
| Brief & Asset Creation | Jules AI | Content Type/Platform Briefs, copywriting, asset coordination via 9 MCP servers |
| Image Generation | NanaBanana 2 | All image assets |
| Image Compositing | Remotion MCP | Layer real product photos onto NanaBanana backgrounds |
| Product Images | GHL Products API | Fetch actual Viatrexx product photos for compositing |
| Task Tracking | Linear (via Jules MCP) | Weekly production task tracking per agent |
| Audio/Video Overviews | Gemini (NotebookLM) | Phase 2 Audio/Video Overviews |
| Blog Writing | Gemini AI | Phase 2 SEO blog posts + companion posts |
| Voice AI | ElevenLabs / Play.ht | Phase 4 AI Podcast voiceovers |

---

## 6. Phase 2+ Weekly Schedule Expansion

### Phase 2

| Day | Additional Content |
|-----|-------------------|
| Monday | BLOG1 + AO1 + BLOG4 published · BP1+BP4 promo (FB,IG,LI) |
| Tuesday | BLOG2 + VO1 + BLOG6 published · BP2+BP6 promo (FB,IG,LI) |
| Wednesday | BLOG3 + AO2 + BLOG5 published · BP3+BP5 promo (FB,IG,LI) |
| Thursday | VO2 + BLOG7 published · BP7 promo (FB,IG,LI) |
| Friday | Email Newsletter (segmented) |
| Mon/Wed/Fri | PIN1–PIN3 Pinterest blog pins (core 3) |

### Phase 3

| Day | Additional Content |
|-----|-------------------|
| Mon–Sun | 1 Reel/Short per day (IG Reels + FB Reels + YT Shorts) |
| Mon–Sun | 5 Stories per day (IG Stories + FB Stories) |

### Phase 4

| Day | Additional Content |
|-----|-------------------|
| Wednesday | AI Podcast Ep 1 (YouTube, Audio, Website transcript) |
| Saturday | AI Podcast Ep 2 (YouTube, Audio, Website transcript) |

---

## 7. Cumulative Weekly Volume (All Phases)

| Phase | Content Pieces | Platform Posts |
|-------|---------------|---------------|
| Phase 1 | 7 image pieces | 28 |
| Phase 2 | 7 blogs + 2 audio + 2 video | 24 |
| Phase 3 | 7 reels + 35 stories | 91 |
| Phase 4 | 2 podcasts | 6 |
| **TOTAL** | **62** | **~149** |
