# Viatrexx Content Creation Flow — End-to-End Pipeline

**Version:** 2.2 (March 2026)

---

## 1. Pipeline Overview

```
TOPIC (Scheduled)
  │
  ▼
MASTER BRIEF ──────────── CLAUDE (Planner)
  │
  ▼
PRODUCT IMAGE FETCH ────── GHL Products API → product_cache
  │
  ▼
JULES AI (15 tasks/day free tier — batched Mon–Thu)
  ├── Content Type Briefs (1 task → 7 briefs, using Content Templates)
  ├── Platform Briefs (3 tasks → by image group)
  ├── NanaBanana Images (7 tasks → 75 images)
  ├── Remotion MCP → composite product photos onto backgrounds
  ├── Copywriting (3 tasks → batched)
  └── Assembly (1 task → 7 complete pieces)
  │
  ▼
CONTENT REVIEW ────────── CLAUDE (Reviewer, 16-point checklist)
  ├── PASS → GHL PUSH → SCHEDULED → POSTED → ANALYTICS
  └── FAIL → JULES REVISION (Fri–Sun buffer, max 3×)
```

---

## 2. Stage 1: Master Brief — Claude (Planner)

**Trigger:** Weekly CRON (Monday 7am MST)
**Agent:** Claude Sonnet via Anthropic API
**Input:** Topic + Pillar + SEO + Protocols + Previous weeks + Active phases
**Output:** Master Brief JSON → Supabase `briefs` table

---

## 3. Stage 2: Product Image Fetch

**Trigger:** Master Brief approved
**Handler:** Content Manager Edge Function

```
1. Read products_referenced from Master Brief
2. For each product name:
   a. Check product_cache (Supabase) for cached image
   b. If cache miss: Call GHL Products API
      GET /products/?locationId={id}&search={product_name}&limit=1
   c. Cache result (7-day TTL)
3. Store product_images array in brief context:
   [{ name: "Systemic Dx", url: "https://...webp" }, ...]
4. Pass enriched brief to Jules
```

---

## 4. Stage 3: Jules Executes (Free Tier: 15 tasks/day)

### Monday: Briefs (4 tasks)

| Task | Description | Output |
|------|-------------|--------|
| T1 | Generate 7 Content Type Briefs using Content Templates (SP-STAT, SP-FRAME, SP-PROOF, INF-DATA, INF-PROCESS, CAR-EDUCATE, CAR-CONVERT) | 7 briefs |
| T2 | Platform Briefs — Group A (FB+LI, 1080×1080) | 7 briefs |
| T3 | Platform Briefs — Group B (IG, 1080×1350) | 7 briefs |
| T4 | Platform Briefs — Group C (Pin, 1000×1500) | 7 briefs |

### Tuesday: Static & Infographic Images (5 tasks)

| Task | Description | NanaBanana Images |
|------|-------------|-------------------|
| T5 | SP1 → 3 group prompts from SP-STAT template | 3 |
| T6 | SP2 → 3 group prompts from SP-FRAME template | 3 |
| T7 | SP3 → 3 group prompts from SP-PROOF template + Remotion product overlay | 3 |
| T8 | INF1 → 3 group prompts from INF-DATA template | 3 |
| T9 | INF2 → 3 group prompts from INF-PROCESS template | 3 |

For any piece with `product_image_zone.enabled = true`: after NanaBanana generates the background, Jules calls Remotion MCP to composite the real product photo onto it, then exports the final PNG.

### Wednesday: Carousel Images + Captions (4 tasks)

| Task | Description | NanaBanana Images |
|------|-------------|-------------------|
| T10 | CAR1 all 10 slides × 3 groups (CAR-EDUCATE template) | 30 |
| T11 | CAR2 all 10 slides × 3 groups (CAR-CONVERT template) + product overlays | 30 |
| T12 | Captions for SP1–SP3, INF1–INF2 (5 pieces × 4 platforms) | — |
| T13 | Captions for CAR1 + CAR2 (2 pieces × 4 platforms) | — |

### Thursday: Assembly (2 Jules tasks + 7 Claude calls)

| Task | Description |
|------|-------------|
| T14 | Alt text + metadata assembly |
| T15 | Final assembly → 7 content_pieces → status: ready_for_review |
| — | Claude (Reviewer) reviews all 7 pieces (7 API calls) |

### Friday–Sunday: Revision Buffer

Jules has 15 tasks/day available for revisions. Each revision = 1 task targeting only failed components. Max 3 loops per piece.

---

## 5. Stage 4: Claude Reviews

16-point checklist (R01–R16). See AI_AGENTS.md.

Failed pieces return to Jules with specific revision instructions. After 3 failures → human escalation.

---

## 6. Stage 5: GHL Push

Image group sharing: FB and LI reference the same Group A media upload. See GHL_INTEGRATION.md.

---

## 7. Phase 2 Parallel Pipeline

```
Mon:  Gemini → 3 core blog posts
Tue:  Gemini → 2 Audio Overviews (NLM) + 2 Video Overviews (NLM)
Wed:  Gemini → 4 companion blog posts from transcripts
Thu:  Jules → 7 blog promo images (2 tasks) + 3 Pinterest pins (Group C)
      Jules → 21 promo captions + 3 Pinterest descriptions (1 task)
Fri:  Claude reviews all Phase 2 content → GHL push
```

---

## 8. Phase 3 Pipeline

```
Jules → 7 Reel scripts from Master Brief reel_hooks
  └── Remotion MCP renders each reel (1080×1920, 30fps)
      └── Product photos composited via Remotion layers

Jules → 35 Story templates (repurposed images + text overlays)
Claude spot-checks sample of reels
All pushed to GHL: Reels → IG+FB+YT Shorts, Stories → IG+FB
```

---

## 9. Phase 4 Pipeline

```
Jules → 2 podcast scripts → Claude reviews → ElevenLabs generates audio
Gemini → 2 transcript blog posts
Distribution: YouTube + Website + Spotify + Apple + RSS
```

---

## 10. CRON Schedule

| Job | Frequency | Time (MST) |
|-----|-----------|-----------|
| Topic Check | Weekly | Monday 6am |
| Master Brief (Claude) | Weekly | Monday 7am |
| GHL Status Sync | Daily | 6am |
| Analytics Collection | Daily | Midnight |
| Analytics 7d Snapshot | Weekly | Sunday midnight |
| Analytics 30d Snapshot | Monthly | 1st, midnight |
| API Counter Reset | Daily | Midnight PT |
| Product Cache Sync | Weekly | Sunday midnight |
| Weekly Report | Weekly | Monday 8am |

---

## 11. Weekly Production Summary (Phase 1)

| Item | Count | Agent |
|------|-------|-------|
| Master Brief | 1 | Claude |
| Content Type Briefs | 7 | Jules |
| Platform Briefs | 21 | Jules |
| Images (NanaBanana) | 75 | Jules → NanaBanana |
| Product Overlays (Remotion) | ~5–10 | Jules → Remotion MCP |
| Captions | 28 | Jules |
| Reviews | 7 | Claude |
| GHL Posts | 28 | Content Manager |
| **Jules Tasks Used** | **15** (Mon–Thu) | — |
