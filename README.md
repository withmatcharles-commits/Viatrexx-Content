# Viatrexx Content Dashboard — System Documentation

**Version:** 2.2 · March 2026

---

## Overview

Complete system design for the Viatrexx Bio Inc. AI-powered content dashboard. The system automates weekly social media content production — from topic scheduling through brief generation, asset creation, review, and publishing to GoHighLevel (GHL) Social Planner.

**Stack:** Next.js · Supabase · GHL API · Claude (Anthropic) · Jules AI · Gemini AI · NanaBanana 2 · Remotion MCP · ElevenLabs

---

## Architecture

```
Topic Schedule (Supabase)
  │
  ▼
Master Brief ──── Claude (Planner)
  │
  ▼
Briefs + Images + Copy ──── Jules AI ──► NanaBanana 2 (images)
  │                                   └► Remotion MCP (product compositing)
  │                                   └► GHL Products API (product photos)
  ▼
Review ──── Claude (Reviewer)
  │
  ▼
GHL Push ──► Facebook · Instagram · LinkedIn · Pinterest
  │
  ▼
Analytics (daily collection)
```

---

## Phased Rollout

| Phase | Content | Weekly Volume |
|-------|---------|--------------|
| **Phase 1** | 3 Static Posts + 2 Infographics + 2 Carousels | 28 platform posts |
| **Phase 2** | 7 Blog Posts + 2 Audio + 2 Video Overviews + 7 Blog Promos + 3 Pinterest Pins | +24 platform posts |
| **Phase 3** | 7 Reels/Shorts (daily) + 35 Stories (5/day) | +91 platform posts |
| **Phase 4** | 2 AI Podcast Episodes | +6 platform posts |
| **Total** | 62 content pieces | ~149 platform posts/week |

---

## AI Agent Roles

| Agent | Model | Role |
|-------|-------|------|
| Claude (Planner) | Anthropic Sonnet | Master Brief strategy, weekly narrative |
| Claude (Reviewer) | Anthropic Sonnet | 16-point QA checklist, revision instructions |
| Jules AI | Google Jules (Free tier) | Briefs, copywriting, asset coordination via 9 MCP servers |
| NanaBanana 2 | Google Gemini Image (Pro) | All image generation (75/week, 3 dimension groups) |
| Gemini AI | Google Gemini / NotebookLM | Blog writing, Audio/Video Overviews (Phase 2) |
| Remotion MCP | Remotion | Product image compositing, reel rendering (Phase 3) |
| ElevenLabs | Voice AI | Podcast voiceover (Phase 4) |

---

## Documents

### Core System

| Document | Description |
|----------|-------------|
| [CONTENT_PLAN.md](docs/CONTENT_PLAN.md) | Phased rollout, weekly posting rotation, image optimization, platform distribution |
| [DASHBOARD_ARCHITECTURE.md](docs/DASHBOARD_ARCHITECTURE.md) | Pages, components, modals, workflows, API analytics panel |
| [DATABASE_SCHEMA.md](docs/DATABASE_SCHEMA.md) | All Supabase tables (17), views, storage buckets, edge functions, seed data |
| [CONTENT_CREATION_FLOW.md](docs/CONTENT_CREATION_FLOW.md) | End-to-end pipeline, Jules task batching for free tier, daily CRON schedule |
| [TASKS.md](docs/TASKS.md) | Implementation plan across 5 build phases |

### AI & Integrations

| Document | Description |
|----------|-------------|
| [AI_AGENTS.md](docs/AI_AGENTS.md) | Agent specs, prompts, MCP servers, coordination flow, cost estimates |
| [GHL_INTEGRATION.md](docs/GHL_INTEGRATION.md) | GHL Social Planner + Products API, image group sharing, status sync |
| [GHL_PRODUCT_IMAGES.md](docs/GHL_PRODUCT_IMAGES.md) | Product photo pipeline — GHL fetch, cache, Remotion compositing |
| [JULES_MCP_SERVERS.md](docs/JULES_MCP_SERVERS.md) | 9 MCP servers, Remotion video/image compositing, Linear task tracking |
| [API_RATE_LIMITS.md](docs/API_RATE_LIMITS.md) | Rate limits for all providers, Jules free-tier batching, usage tracking |

### Templates & Content

| Document | Description |
|----------|-------------|
| [CONTENT_TEMPLATES.md](docs/CONTENT_TEMPLATES.md) | Phase 1 templates with NanaBanana prompts in JSON, product image zones |

---

## Quick Start

1. Set up Supabase project and run schema from `DATABASE_SCHEMA.md`
2. Seed pillars, topics, and weekly schedule
3. Configure API keys (see `TASKS.md` → Environment Variables)
4. Connect Jules MCP servers (see `JULES_MCP_SERVERS.md`)
5. Run product cache sync from GHL
6. Enable Phase 1 in settings
7. Content Manager CRON begins weekly production

---

## Directory Structure

```
docs/
  ├── CONTENT_PLAN.md
  ├── DASHBOARD_ARCHITECTURE.md
  ├── DATABASE_SCHEMA.md
  ├── CONTENT_CREATION_FLOW.md
  ├── AI_AGENTS.md
  ├── GHL_INTEGRATION.md
  ├── GHL_PRODUCT_IMAGES.md
  ├── JULES_MCP_SERVERS.md
  ├── API_RATE_LIMITS.md
  ├── CONTENT_TEMPLATES.md
  └── TASKS.md
README.md
```
