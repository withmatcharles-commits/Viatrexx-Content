# Viatrexx AI Agent Specifications

**Version:** 2.2 (March 2026)

---

## 1. Architecture

```
┌──────────────────────────────────────────┐
│       CONTENT MANAGER (Logic Agent)      │
│  Supabase Edge Functions — no LLM        │
│  Pre-flight rate limit checks            │
│  GHL product image fetch                 │
└──────────┬───────────────────────────────┘
           │
    ┌──────┴──────────────────┐
    │                         │
┌───▼──────────┐    ┌────────▼────────┐
│  CLAUDE      │    │    CLAUDE       │
│  (Planner)   │    │   (Reviewer)    │
│  1 call/week │    │  7+ calls/week  │
└───┬──────────┘    └────────▲────────┘
    │                        │
┌───▼────────────────────────┤
│       JULES AI (Free: 15/day)          │
│  Connected MCP Servers:                 │
│  ├── Supabase (DB)                     │
│  ├── Remotion (compositing + video)    │
│  ├── Remotion Media (NanaBanana+Voice) │
│  ├── Linear (task tracking)            │
│  ├── Neon (edge Postgres)              │
│  ├── Stitch (data sync)               │
│  ├── V0 (UI gen)                       │
│  ├── Render (deployment)               │
│  └── Context7 (API docs)              │
│                                         │
│  Image Pipeline:                        │
│  NanaBanana 2 → background             │
│  GHL Products API → product photo      │
│  Remotion MCP → composite → final PNG  │
└─────────────────────────────────────────┘
```

| Agent | Model | Role | Rate Limit |
|-------|-------|------|------------|
| Content Manager | Logic (no LLM) | Orchestrator + pre-flight + product fetch | N/A |
| Planner | Claude Sonnet | Master Brief strategy | ~8 calls/week |
| Reviewer | Claude Sonnet | 16-point QA | ~7+ calls/week |
| Brief & Asset Creator | Jules AI (Free) | Briefs, copy, compositing coordination | 15 tasks/day, 3 concurrent |
| Image Generator | NanaBanana 2 (Pro) | Background images | ~100 images/day |
| Compositing | Remotion MCP | Product overlay, reel rendering | N/A |
| Blog Writer | Gemini AI | Blogs + NLM overviews (Phase 2) | ~1,500/day free |
| Voice | ElevenLabs | Podcast (Phase 4) | 100K chars/month |

---

## 2. Content Manager

**No LLM** — pure logic via Supabase Edge Functions.

### Responsibilities

1. Monitor topic schedule (12-week lookahead)
2. Trigger Claude (Planner) on Monday 7am
3. **Fetch product images from GHL after Master Brief approved**
4. Trigger Jules with enriched brief (includes product image URLs)
5. Run pre-flight rate limit checks before every agent trigger
6. Route Claude review failures back to Jules
7. Trigger GHL push on approval
8. Daily CRON for GHL sync, analytics, API counter reset
9. Weekly CRON for product cache sync

---

## 3. Claude — Planner

**Model:** Claude Sonnet · **Calls/week:** 1

### System Prompt

```
You are the Viatrexx Content Strategy Agent. You create Master Content
Briefs that define the strategic narrative, key messages, and direction
for a weekly content topic.

BRAND VOICE: Clinical but Compassionate. No marketing fluff. No miracle
cure claims.

FORBIDDEN: cure, cures, always works, never fails, guaranteed, 100%
effective, miracle, magic, instant results.

OUTPUT: Valid JSON only.
```

### Output includes template guidance

```yaml
template_guidance:
  sp1_visual_approach: "Surprising stat highlighting matrix congestion"
  sp2_framework_type: "two-column comparison diagram"
  sp3_proof_angle: "Spray delivery precision advantage"
  inf1_data_layout: "3 vertical stat blocks"
  inf2_process_steps: 3
  car1_myth_count: 5
  car2_framework_name: "Terrain Restoration Protocol"
```

---

## 4. Jules AI — Brief & Asset Creator

### 4.1 Task Batching (Free Tier: 15/day)

| Day | Tasks | Work |
|-----|-------|------|
| Monday | 4 | 7 Content Type Briefs (1) + Platform Briefs by group (3) |
| Tuesday | 5 | Images for SP1–SP3 + INF1–INF2 (1 each) |
| Wednesday | 4 | Carousel images (2) + all captions (2) |
| Thursday | 2 | Alt text + final assembly |
| Fri–Sun | Buffer | Revisions (15/day available) |

### 4.2 Template Integration

```
Jules receives: Master Brief + piece_code
  │
  ├── Template lookup:
  │     SP1 → SP-STAT   │ SP2 → SP-FRAME  │ SP3 → SP-PROOF
  │     INF1 → INF-DATA │ INF2 → INF-PROCESS
  │     CAR1 → CAR-EDUCATE │ CAR2 → CAR-CONVERT
  │
  ├── Fill {{VARIABLE}} placeholders from Master Brief
  │
  ├── Generate NanaBanana prompts for 3 image groups
  │
  ├── Check product_image_zone.enabled for this template
  │     IF true AND product_images available:
  │       a. NanaBanana generates background (no product)
  │       b. Remotion MCP composites product photo onto background
  │       c. Export final PNG
  │     IF false OR no product images:
  │       a. NanaBanana generates standard image
  │
  └── Upload final images to Supabase Storage
```

### 4.3 NanaBanana Prompt Assembly

```
1. Select template prompt for image group (group_a/b/c)
2. Replace {{VARIABLES}} from brief
3. Append: --no stethoscope, pills, stock photo, cartoon, clipart
4. Append: --style clean-medical (or premium-medical)
5. Send to NanaBanana 2 API
```

### 4.4 Product Image Compositing via Remotion MCP

```javascript
// After NanaBanana generates background:
remotion_create_project({ name: "sp3-composite", width: 1080, height: 1080 });
remotion_add_image_content({ src: backgroundUrl, fit: "cover" });
remotion_add_image_content({
  src: productImageUrl,  // from GHL product_cache
  fit: "contain",
  position: "center-right",
  scale: 0.3,
  effects: ["drop-shadow", "rotation(-5deg)"]
});
// Export single-frame PNG
```

---

## 5. Claude — Reviewer

**Model:** Claude Sonnet · **Calls/week:** 7+

### 16-Point Checklist

| # | Rule | Severity |
|---|------|----------|
| R01 | No forbidden words | FAIL |
| R02 | Claims verified against monographs | FAIL |
| R03 | Mandatory disclaimers present | FAIL |
| R04 | TCM/emotional claims qualified | FAIL |
| R05 | Tone matches audience | WARN |
| R06 | No marketing fluff | FAIL |
| R07 | Correct image group dimensions | FAIL |
| R08 | Brand colors correct | WARN |
| R09 | No banned imagery | FAIL |
| R10 | Text within safe zones | WARN |
| R11 | Caption length within limits | FAIL |
| R12 | Hashtag count correct | WARN |
| R13 | CTA present | WARN |
| R14 | Matches awareness level | WARN |
| R15 | Primary keyword in caption | WARN |
| R16 | Image groups shared correctly (FB+LI same) | WARN |

**Revision loop:** FAIL → Jules revises → Claude re-reviews (max 3×) → human escalation.

---

## 6. Phase 2+: Gemini AI, Voice AI

**Gemini:** 3 core blogs + 4 companion blogs + 2 Audio + 2 Video Overviews via NotebookLM.

**ElevenLabs:** Phase 4 podcast voiceover. 2 episodes/week.

---

## 7. Coordination Flow

```
Monday 6am: Content Manager CRON
  ├── Check Jules (15/15), NanaBanana (100/100), Claude (OK)
  ├── 7am: Claude → Master Brief
  ├── Product image fetch → GHL API → product_cache
  └── Jules: 4 brief tasks (with product image URLs in context)

Tuesday: Jules: 5 image tasks (NanaBanana + Remotion compositing)
Wednesday: Jules: 4 tasks (carousels + captions)
Thursday: Jules: 2 assembly tasks → Claude reviews 7 pieces
Fri–Sun: Revision buffer → GHL push when all approved
```

---

## 8. Cost (Phase 1 Weekly)

| Provider | Tier | Usage | Cost |
|----------|------|-------|------|
| Jules | Free | 15 tasks | $0 |
| NanaBanana | Pro | 75 images | ~$5/week |
| Claude | Build T1 | ~8 calls | ~$0.50 |
| GHL Products API | Included | ~10 calls/week | $0 |
| Remotion MCP | Self-hosted | ~10 composites | $0 |
| **Monthly Total** | — | — | **~$22** |

---

## 9. Configuration

```json
{
  "agents": {
    "claude_planner": { "model": "claude-sonnet-4-20250514", "max_tokens": 4000, "temperature": 0.7 },
    "claude_reviewer": { "model": "claude-sonnet-4-20250514", "max_tokens": 2000, "temperature": 0.3 },
    "jules": {
      "tier": "free", "daily_task_limit": 15, "concurrent_limit": 3,
      "mcp_servers": ["supabase","remotion","remotion-media","linear","neon","stitch","v0","render","context7"],
      "template_source": "CONTENT_TEMPLATES.md",
      "product_image_compositing": true
    },
    "nanabanana": { "tier": "pro", "daily_image_limit": 100, "style_preset": "viatrexx_brand" }
  },
  "image_generation": {
    "dimension_groups": {
      "group_a": { "width": 1080, "height": 1080, "platforms": ["PL01","PL03"] },
      "group_b": { "width": 1080, "height": 1350, "platforms": ["PL02"] },
      "group_c": { "width": 1000, "height": 1500, "platforms": ["PL04"] }
    }
  },
  "rate_limits": { "pre_flight_check": true, "alert_threshold_percent": 80, "max_revision_loops": 3 }
}
```
