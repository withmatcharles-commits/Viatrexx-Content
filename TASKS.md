# Viatrexx Content Dashboard — Implementation Plan

**Version:** 2.2 (March 2026)

---

## Phase 1: Foundation — Database & Backend

### 1.1 Supabase Setup

- Create Supabase project
- Create all 17 tables from DATABASE_SCHEMA.md
- Set up Row-Level Security policies
- Create Storage buckets (content-assets, blog-assets, brand-assets)
- Create 4 database views
- Seed pillar data (7 pillars)
- Import topic data (~140 topics)
- Import weekly schedule (2026 W11 through 2027 W52)
- Seed API rate limit status for all 5 providers
- Seed settings (brand kit, platform configs, image dimension groups, posting defaults)

### 1.2 Edge Functions

- `generate-master-brief` — Claude API for Master Brief
- `jules-create-content` — Jules AI with task batching + Content Template loading
- `gemini-create-blogs` — Gemini for blogs + NLM overviews (Phase 2)
- `review-content` — Claude API for 16-point review
- `push-to-ghl` — GHL Social Planner API with image group sharing
- `sync-ghl-status` — Daily GHL status polling
- `collect-analytics` — Daily analytics collection
- `sync-product-cache` — Weekly GHL Products → product_cache sync + on-demand
- `reset-api-counters` — Daily midnight PT counter reset
- `pre-flight-check` — Rate limit validation before agent triggers
- `weekly-report` — Weekly performance summary

### 1.3 AI Agent Setup

- Configure Claude API (Anthropic) — Build Tier 1
- Configure Jules AI — Free tier, verify 15 tasks/day
- Configure NanaBanana 2 API — AI Pro ($19.99/mo)
- Load Content Templates (CONTENT_TEMPLATES.md) into settings/storage
- Configure Gemini API (Phase 2 prep)
- Configure ElevenLabs API (Phase 4 prep)
- Implement pre-flight rate limit checks
- Implement API usage logging to api_usage_log
- Implement API counter updates to api_rate_limit_status

### 1.4 Jules MCP Server Connections

- Connect Supabase MCP (database access)
- Set up Remotion MCP server (local or Render-hosted)
- Connect Remotion Media MCP (NanaBanana + ElevenLabs)
- Connect Linear MCP (task tracking)
- Connect Neon MCP (edge Postgres)
- Connect Stitch MCP (data sync)
- Connect V0 MCP (UI gen)
- Connect Render MCP (deployment)
- Connect Context7 MCP (API docs)

### 1.5 GHL Integration

- Set up GHL Private Integration Token
- Map social media account IDs (FB, IG, LI, Pinterest)
- Implement image group → platform mapping
- Implement GHL Products API integration (List + Get by ID)
- Create product_cache sync function
- Test full cycle: upload → post → status sync
- Implement rate limiting and backoff

### 1.6 Product Image Pipeline

- Implement product_cache table and sync edge function
- Build product image lookup function (cache-first with GHL fallback)
- Implement Remotion MCP compositing (background + product overlay → PNG)
- Add product image zones to Content Templates
- Test end-to-end: brief references product → GHL fetch → cache → Remotion composite → final image

---

## Phase 2: Dashboard Core — Pages & Navigation

### 2.1 App Shell

- Next.js project with Supabase client
- Authentication (Supabase Auth)
- Sidebar navigation, global header, notifications
- Responsive layout, brand theme

### 2.2 Dashboard Page

- This Week Card, Pipeline Summary, Next 4 Weeks Strip
- Quick Stats, Activity Feed, Agent Status Panel
- API Health Strip (compact provider status bars)

### 2.3 Topics Pages

- Pillars grid with expand-to-detail
- Topic data table with filters/sort
- Week schedule with 5 visual zones and drag-drop
- Topic detail with Briefs + Content + product image badges

### 2.4 Drafts Pages

- Brief table with agent attribution
- Content card grid with image group labels
- Blog post table (Phase 2)
- Content detail with Group A/B/C preview, product overlay indicator, platform mockups

### 2.5 Remaining Pages

- Scheduled (calendar + list with GHL status)
- Posted (card grid with metrics and lineage)
- Analytics (multi-panel with phase filtering)
- Content Flow (timeline with multi-filters)

### 2.6 Settings Page

- Brand Kit, Platform Connections
- GHL Products panel (cache status, sync button, product list)
- AI API Analytics panel (per-provider cards with gauges, sparklines, budgets)
- Alert configuration toggles
- Phase Control, Review Settings, User Management

---

## Phase 3: AI Agent Integration

### 3.1 Claude — Planner

- System prompt for Master Brief generation
- Input context assembly (topic, pillar, SEO, protocols, previous weeks)
- Phase-aware output fields (blog_angles, reel_hooks, podcast_outline)

### 3.2 Jules — Brief & Asset Creator

- Jules API integration with task batching (15/day budget)
- Content Template loading and variable replacement
- NanaBanana prompt assembly (template + variables + negative prompt + style)
- Product image compositing via Remotion MCP
- Day scheduling: Mon (4) → Tue (5) → Wed (4) → Thu (2) → Fri–Sun (buffer)
- Concurrent management (max 3)
- Revision handling from Claude review feedback

### 3.3 Claude — Reviewer

- 16-point checklist (R01–R16 including image group validation)
- Revision loop management (max 3, then human escalation)

### 3.4 Content Manager (Orchestrator)

- Weekly CRON: topic check, Master Brief trigger
- Product image fetch after Master Brief approved
- Pre-flight rate limit checks before every agent trigger
- Daily CRON: GHL sync, analytics, API counter reset
- Weekly CRON: product cache sync
- Alert dispatch for limits and failures
- Linear task auto-creation via Jules MCP

---

## Phase 4: Modals, Components & Polish

### 4.1 Modals

- Topic Quick-Add, Schedule Topic, Brief Generator
- Content Review (16-point checklist), GHL Push
- Platform Preview, Image Group Preview
- API Limit Warning

### 4.2 Components

- PillarBadge, StatusBadge, ContentTypeIcon, PlatformChips
- AwarenessTag, PhaseBadge, ImageGroupLabel, ProductImageBadge
- AgentAttributionChip, APIUsageGauge, APIHealthStrip
- APIProviderCard, UsageSparkline, BudgetBar, TierBadge
- WeekCard, ContentPreviewCard, PlatformMockup
- BriefAccordion, ReviewChecklistPanel, APILimitWarningModal

### 4.3 Real-time

- Supabase Realtime for status changes
- Live progress during AI generation
- Toast notifications, dashboard auto-refresh

---

## Phase 5: Content Phases 2–4 Expansion

### 5.1 Phase 2 — Blog + Audio/Video + Promos

- Gemini integration for 3 core + 4 companion blog posts
- NotebookLM for 2 Audio + 2 Video Overviews
- NLM post-processing (trim, watermark removal, branded ending)
- Blog promo posts via Jules (7 promos × 3 platforms + 3 Pinterest pins)
- Claude review for all Phase 2 content

### 5.2 Phase 3 — Reels + Stories

- Reel creation: Jules scripts → Remotion MCP renders (1080×1920, 30fps)
- Product photos composited into reels via Remotion layers
- Story creation: repurposed images + text overlays + link stickers
- Claude spot-check review

### 5.3 Phase 4 — AI Podcast

- Jules creates podcast scripts from Claude's outline
- Claude reviews scripts for accuracy
- ElevenLabs generates audio, Gemini writes transcripts
- Distribution: YouTube + Website + Spotify + Apple + RSS

---

## Environment Variables

```
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=
ANTHROPIC_API_KEY=
JULES_API_KEY=
GEMINI_API_KEY=
NANABANANA_API_KEY=
GHL_PRIVATE_INTEGRATION_TOKEN=
GHL_LOCATION_ID=
ELEVENLABS_API_KEY=
```

---

## Document Index

| Document | Description |
|----------|-------------|
| [CONTENT_PLAN.md](CONTENT_PLAN.md) | Phased rollout, rotation patterns, image optimization |
| [DASHBOARD_ARCHITECTURE.md](DASHBOARD_ARCHITECTURE.md) | Pages, components, modals, workflows, API panel |
| [DATABASE_SCHEMA.md](DATABASE_SCHEMA.md) | 17 Supabase tables, 4 views, storage, edge functions |
| [CONTENT_CREATION_FLOW.md](CONTENT_CREATION_FLOW.md) | Pipeline with Jules batching, product fetch, daily CRON |
| [AI_AGENTS.md](AI_AGENTS.md) | Agent specs, prompts, MCP servers, coordination, costs |
| [GHL_INTEGRATION.md](GHL_INTEGRATION.md) | Social Planner + Products API, image sharing, sync |
| [GHL_PRODUCT_IMAGES.md](GHL_PRODUCT_IMAGES.md) | Product photo pipeline, cache, Remotion compositing |
| [JULES_MCP_SERVERS.md](JULES_MCP_SERVERS.md) | 9 MCP servers, Remotion integration, Linear tracking |
| [API_RATE_LIMITS.md](API_RATE_LIMITS.md) | All provider limits, Jules batching, usage tracking |
| [CONTENT_TEMPLATES.md](CONTENT_TEMPLATES.md) | 7 templates with NanaBanana prompts, product zones |
| [TASKS.md](TASKS.md) | This document — implementation plan |
