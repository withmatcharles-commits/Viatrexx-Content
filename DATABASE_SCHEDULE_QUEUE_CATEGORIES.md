# Viatrexx Content Schedule, Queue & Categories

**Version:** Phase 2 (March 2026)

---

## 1. Weekly Schedule Template

### Standard Week

| Day | Content Types | Platform Focus | Theme Slot |
|-----|--------------|----------------|------------|
| Monday | Static Post 1 + Explainer Video 1 + Reel 1 | FB, IG, LI, YT | Educate / "The Why" |
| Tuesday | Carousel 1 + Testimonial + Reel 2 | FB, IG, LI, Pin, YT | Problem → Solution + Proof |
| Wednesday | Static Post 2 + Podcast 1 | FB, IG, LI, YT, Web | Deep Science Dive |
| Thursday | Carousel 2 + Explainer Video 2 + Reel 3 | FB, IG, LI, YT, Pin | Condition-Specific Protocol |
| Friday | Static Post 3 | FB, IG, LI | Lifestyle Tip / Soft Sell |
| Saturday | Email Newsletter | Email | Weekly Recap + Education |
| Sunday | Podcast 2 | YT, Web, Audio | Thought Leadership |

### Weekly Totals (Phase 2)

| Content Type | Weekly Count |
|-------------|-------------|
| Static Post / Infographic | 3 |
| Carousel | 2 |
| Testimonial / Quote Post | 1 |
| Reel / Short | 3 |
| Explainer Video | 2 |
| Podcast Episode | 2 |
| SEO Blog Post | 1 |
| Email Newsletter | 1 |
| **Total pieces** | **15** |

### NotebookLM Supplemental Content (Monthly)

| Content Type | Monthly Count | Notes |
|-------------|-------------|-------|
| Video Explainer (NLM) | 2 | Protocol overviews, brand philosophy |
| Audio Explainer (NLM) | 2 | Topic primers, protocol summaries |
| Slide Deck (NLM) | 1 | Practitioner education decks |
| Infographic (NLM) | 2 | Process diagrams, comparison charts |

---

## 2. Content Queue System

### Queue Status Flow

```
IDEATION → QUEUED → BRIEF_CREATED → IN_PRODUCTION → IN_REVIEW → READY → SCHEDULED → LIVE → ARCHIVED
```

### Status Definitions

| Status | Definition | Next Action |
|--------|-----------|-------------|
| `IDEATION` | Topic identified, not yet formally assigned | Create brief |
| `QUEUED` | Assigned to calendar week, brief pending | Write master brief |
| `BRIEF_CREATED` | Master brief approved | Generate assets |
| `IN_PRODUCTION` | Assets being generated (NanaBanana / Remotion / NLM) | Complete production |
| `IN_REVIEW` | Pending science/brand/regulatory review | Approve or request revisions |
| `READY` | Approved, awaiting scheduling | Schedule for publish date |
| `SCHEDULED` | Loaded in scheduling tool with publish date/time | Auto-publish |
| `LIVE` | Published and active | Monitor performance |
| `ARCHIVED` | Performance logged, content retired or evergreen-tagged | Reference for repurposing |

### Queue Record Schema

```yaml
queue_item:
  id: "Q-2026-W10-CT04-01"     # Queue ID format: Q-{year}-W{week}-{content_type}-{seq}
  topic_id: "T-P5-04"           # Reference to Topic Database
  pillar_id: "P5"               # Pillar reference
  content_type: "CT04"          # Content Type reference
  awareness_level: "TOFU"       # TOFU / MOFU / BOFU
  target_platforms:              # Platform references
    - "PL02"                    # Instagram
    - "PL05"                    # YouTube
  status: "IN_PRODUCTION"       # Current status
  brief_url: ""                 # Link to master brief
  assets: []                    # Generated asset file paths
  assigned_to: ""               # Agent or human owner
  review_notes: ""              # Review feedback
  publish_date: "2026-03-04"    # Target publish date
  performance:                  # Post-publish metrics
    impressions: 0
    engagement_rate: 0
    saves: 0
    shares: 0
    clicks: 0
```

---

## 3. Content Categories

Content is categorized across multiple dimensions for filtering, reporting, and AI agent routing.

### Category: Audience

| Code | Audience | Description |
|------|----------|-------------|
| `AUD-B2B` | Practitioners (B2B) | Licensed healthcare professionals |
| `AUD-B2C` | Informed Seekers (B2C) | Patients and wellness enthusiasts |
| `AUD-BOTH` | Both | Content relevant to both audiences |
| `AUD-B2B-SVC` | Business Partners | Private label / contract manufacturing prospects |

### Category: Condition Cluster

| Code | Condition Cluster | Related Products |
|------|------------------|-----------------|
| `CC-AESTH` | Aesthetics & Skin | ConnectissueXX, Glow Cream, Collagen, Derma, Pigmentation |
| `CC-BIOGU` | Biological & Gut | CandidaXX, P'sitesXX, GI, B'teria, F'gus |
| `CC-DETOX` | Systemic Detox & Drainage | Systemic Dx, Mesenchyme, Lymph 1, Intra Cell |
| `CC-ENDOC` | Endocrine & Metabolic | Adipose, Thyro, Fem+, Male+, Intra Cell |
| `CC-INFLA` | Inflammation & Pain | InflaXX, OuCHXX, MuSkel, Articula, Connectissue |
| `CC-NEURO` | Neurological | Neuro 3, ANS-CNS, MuSkel, BDNF, Prolo-Neural |
| `CC-IMMUN` | Immune Support | Immunexx, Aller Balance, Arthro, Systemic Dx |
| `CC-EMOTI` | Emotional & TCM | Relief+, MuSkel, OuCH, Systemic |
| `CC-ENVIR` | Environmental Toxins | H Metals, Radiation, Environmental, G'path, D'ntl |

### Category: Content Purpose

| Code | Purpose | Description |
|------|---------|-------------|
| `PUR-EDUC` | Educate | Build awareness, explain concepts |
| `PUR-INFO` | Inform | Deepen understanding, show frameworks |
| `PUR-CONV` | Convert | Drive action, demonstrate proof |
| `PUR-RETA` | Retain | Keep audience engaged, nurture relationship |
| `PUR-AUTH` | Authority | Establish thought leadership and expertise |

### Category: Product Line

| Code | Product Line | Description |
|------|-------------|-------------|
| `PL-ORAL` | Oral Sprays | Standard calibrated spray delivery products |
| `PL-TOPI` | Topicals | Creams and topical applications |
| `PL-INJC` | Injectables | Sterile ampoules for practitioner use |
| `PL-KITS` | Protocol Kits | Multi-product bundled protocols (AAP series) |
| `PL-SERV` | Services | Contract manufacturing, private label, education |

### Category: SEO Tier

| Code | Tier | Description | Example Keywords |
|------|------|-------------|-----------------|
| `SEO-T1` | Tier 1 — Brand | Core brand/methodology keywords | Bio-Incorporated Medicine, Viatrexx protocols |
| `SEO-T2` | Tier 2 — Condition | High-intent condition/solution clusters | Natural scar deactivation, lymphatic drainage |
| `SEO-T3` | Tier 3 — Long-Tail | Specific question-based phrases | "How to clear stored emotional baggage from cellular memory" |

---

## 4. Tagging Schema

Every content item should be tagged across all applicable category dimensions:

```yaml
tags:
  pillar: ["P5"]
  audience: ["AUD-BOTH"]
  condition_cluster: ["CC-DETOX"]
  content_purpose: ["PUR-EDUC"]
  product_line: ["PL-ORAL"]
  seo_tier: ["SEO-T2"]
  awareness_level: "MOFU"
  products_referenced: ["Systemic Dx", "Mesenchyme", "Lymph 1"]
  keywords: ["drainage vs detox", "extracellular matrix", "opening emunctories"]
```

This enables:
- AI agents to select appropriate topics and templates
- Automated content gap analysis
- Performance reporting by category
- Smart repurposing suggestions
