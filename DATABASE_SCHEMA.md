# Viatrexx Content Dashboard — Supabase Database Schema

**Version:** 2.2 (March 2026)

---

## 1. Schema Overview

```
pillars
topics
weekly_schedule
briefs
  └── brief_slides
content_pieces
  └── content_assets (shared image groups)
  └── content_copy (per-platform)
  └── content_reviews
blog_posts (Phase 2)
product_cache (GHL product images)
posts
  └── post_analytics
  └── post_comments
api_usage_log
api_rate_limit_status
settings
ai_agent_logs
```

**Total: 17 tables + 4 views + 3 storage buckets + 9 edge functions**

---

## 2. Tables

### `pillars`

```sql
CREATE TABLE pillars (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  code VARCHAR(20) NOT NULL UNIQUE,
  short_code VARCHAR(20) NOT NULL,
  name VARCHAR(100) NOT NULL,
  description TEXT,
  primary_focus TEXT,
  target_audience VARCHAR(20),
  seo_silo VARCHAR(100),
  tier1_keywords TEXT[],
  color_hex VARCHAR(7),
  icon VARCHAR(50),
  overlap_notes JSONB,
  sort_order INTEGER DEFAULT 0,
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);
```

### `topics`

```sql
CREATE TABLE topics (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  pillar_id UUID REFERENCES pillars(id) ON DELETE SET NULL,
  title VARCHAR(255) NOT NULL,
  key_concept TEXT,
  target_audience VARCHAR(20),
  source_references TEXT,
  primary_seo_keywords TEXT[],
  secondary_seo_keywords TEXT[],
  condition_cluster VARCHAR(50),
  products_referenced TEXT[],
  regulatory_notes TEXT,
  scientific_sources TEXT[],
  notes TEXT,
  status VARCHAR(30) DEFAULT 'unscheduled',
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_topics_pillar ON topics(pillar_id);
CREATE INDEX idx_topics_status ON topics(status);
```

### `weekly_schedule`

```sql
CREATE TABLE weekly_schedule (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  year INTEGER NOT NULL,
  week_number INTEGER NOT NULL,
  quarter VARCHAR(5),
  date_start DATE NOT NULL,
  date_end DATE NOT NULL,
  topic_id UUID REFERENCES topics(id) ON DELETE SET NULL,
  pillar_id UUID REFERENCES pillars(id) ON DELETE SET NULL,
  posting_pattern VARCHAR(1),
  production_status VARCHAR(30) DEFAULT 'pending',
  reason TEXT,
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now(),
  UNIQUE(year, week_number)
);
CREATE INDEX idx_schedule_topic ON weekly_schedule(topic_id);
CREATE INDEX idx_schedule_dates ON weekly_schedule(date_start, date_end);
```

### `briefs`

```sql
CREATE TABLE briefs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  brief_code VARCHAR(50) NOT NULL UNIQUE,
  topic_id UUID REFERENCES topics(id) ON DELETE CASCADE,
  schedule_id UUID REFERENCES weekly_schedule(id) ON DELETE SET NULL,
  parent_brief_id UUID REFERENCES briefs(id) ON DELETE SET NULL,
  brief_level VARCHAR(20) NOT NULL,
  content_type_code VARCHAR(10),
  piece_code VARCHAR(10),
  platform_code VARCHAR(10),
  awareness_level VARCHAR(10),
  headline VARCHAR(255),
  core_message TEXT,
  visual_direction TEXT,
  image_generation_prompt TEXT,
  color_palette TEXT,
  text_overlay TEXT,
  caption_draft TEXT,
  cta TEXT,
  hashtags TEXT[],
  dimensions VARCHAR(20),
  image_group VARCHAR(10),
  caption_tone VARCHAR(100),
  platform_notes TEXT,
  slide_count INTEGER,
  brief_data JSONB,
  status VARCHAR(20) DEFAULT 'draft',
  generated_by VARCHAR(20),
  approved_by VARCHAR(100),
  approved_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_briefs_topic ON briefs(topic_id);
CREATE INDEX idx_briefs_schedule ON briefs(schedule_id);
CREATE INDEX idx_briefs_level ON briefs(brief_level);
CREATE INDEX idx_briefs_status ON briefs(status);
```

### `brief_slides`

```sql
CREATE TABLE brief_slides (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  brief_id UUID REFERENCES briefs(id) ON DELETE CASCADE,
  slide_number INTEGER NOT NULL,
  purpose VARCHAR(20),
  headline VARCHAR(255),
  body_text TEXT,
  visual_notes TEXT,
  image_prompt TEXT,
  cta_text VARCHAR(255),
  product_reference VARCHAR(255),
  sort_order INTEGER,
  created_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_brief_slides_brief ON brief_slides(brief_id);
```

### `content_pieces`

```sql
CREATE TABLE content_pieces (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  topic_id UUID REFERENCES topics(id) ON DELETE CASCADE,
  schedule_id UUID REFERENCES weekly_schedule(id) ON DELETE SET NULL,
  brief_id UUID REFERENCES briefs(id) ON DELETE SET NULL,
  piece_code VARCHAR(10) NOT NULL,
  content_type_code VARCHAR(10) NOT NULL,
  awareness_level VARCHAR(10),
  target_platforms TEXT[],
  phase INTEGER DEFAULT 1,
  status VARCHAR(30) DEFAULT 'draft',
  review_attempts INTEGER DEFAULT 0,
  last_review_at TIMESTAMPTZ,
  scheduled_date DATE,
  scheduled_time TIME,
  posting_pattern VARCHAR(1),
  day_of_week VARCHAR(10),
  tags TEXT[],
  utm_parameters JSONB,
  link_url TEXT,
  linked_blog_id UUID,
  notes TEXT,
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_content_topic ON content_pieces(topic_id);
CREATE INDEX idx_content_schedule ON content_pieces(schedule_id);
CREATE INDEX idx_content_status ON content_pieces(status);
CREATE INDEX idx_content_phase ON content_pieces(phase);
```

### `content_assets`

```sql
CREATE TABLE content_assets (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  content_piece_id UUID REFERENCES content_pieces(id) ON DELETE CASCADE,
  image_group VARCHAR(10),
  shared_platforms TEXT[],
  asset_type VARCHAR(20) NOT NULL,
  file_url TEXT NOT NULL,
  file_name VARCHAR(255),
  mime_type VARCHAR(50),
  width INTEGER,
  height INTEGER,
  file_size_bytes BIGINT,
  duration_seconds INTEGER,
  alt_text TEXT,
  slide_number INTEGER,
  sort_order INTEGER DEFAULT 0,
  generation_prompt TEXT,
  generated_by VARCHAR(20),
  has_product_overlay BOOLEAN DEFAULT false,
  product_image_url TEXT,
  created_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_assets_content ON content_assets(content_piece_id);
CREATE INDEX idx_assets_group ON content_assets(image_group);
```

### `content_copy`

```sql
CREATE TABLE content_copy (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  content_piece_id UUID REFERENCES content_pieces(id) ON DELETE CASCADE,
  platform_code VARCHAR(10) NOT NULL,
  caption TEXT,
  hashtags TEXT[],
  cta_text TEXT,
  first_comment TEXT,
  alt_text TEXT,
  link_url TEXT,
  link_text TEXT,
  meta_description TEXT,
  subject_line TEXT,
  tone_notes TEXT,
  generated_by VARCHAR(20),
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_copy_content ON content_copy(content_piece_id);
CREATE INDEX idx_copy_platform ON content_copy(platform_code);
```

### `content_reviews`

```sql
CREATE TABLE content_reviews (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  content_piece_id UUID REFERENCES content_pieces(id) ON DELETE CASCADE,
  reviewer_type VARCHAR(10) NOT NULL,
  reviewer_name VARCHAR(100),
  overall_result VARCHAR(20) NOT NULL,
  checklist_results JSONB NOT NULL,
  summary_notes TEXT,
  revision_instructions TEXT,
  review_iteration INTEGER DEFAULT 1,
  created_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_reviews_content ON content_reviews(content_piece_id);
```

### `blog_posts` (Phase 2)

```sql
CREATE TABLE blog_posts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  topic_id UUID REFERENCES topics(id) ON DELETE CASCADE,
  schedule_id UUID REFERENCES weekly_schedule(id) ON DELETE SET NULL,
  blog_type VARCHAR(20) NOT NULL,
  piece_code VARCHAR(10),
  linked_overview_piece_id UUID,
  title VARCHAR(255),
  slug VARCHAR(255),
  h1_title VARCHAR(255),
  meta_description TEXT,
  body_html TEXT,
  body_markdown TEXT,
  word_count INTEGER,
  featured_image_url TEXT,
  featured_image_alt TEXT,
  primary_keyword VARCHAR(255),
  secondary_keywords TEXT[],
  internal_links JSONB,
  schema_type VARCHAR(50),
  aeo_answer TEXT,
  status VARCHAR(20) DEFAULT 'draft',
  published_url TEXT,
  published_at TIMESTAMPTZ,
  generated_by VARCHAR(20),
  reviewed_by VARCHAR(20),
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_blog_topic ON blog_posts(topic_id);
CREATE INDEX idx_blog_type ON blog_posts(blog_type);
CREATE INDEX idx_blog_status ON blog_posts(status);
```

### `product_cache` (GHL Product Images)

```sql
CREATE TABLE product_cache (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  ghl_product_id VARCHAR(100) NOT NULL UNIQUE,
  product_name VARCHAR(255) NOT NULL,
  product_name_normalized VARCHAR(255),
  primary_image_url TEXT,
  media_urls JSONB,
  description TEXT,
  cached_at TIMESTAMPTZ DEFAULT now(),
  expires_at TIMESTAMPTZ DEFAULT (now() + interval '7 days')
);
CREATE INDEX idx_product_cache_name ON product_cache(product_name_normalized);
CREATE INDEX idx_product_cache_ghl ON product_cache(ghl_product_id);
```

### `posts`

```sql
CREATE TABLE posts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  content_piece_id UUID REFERENCES content_pieces(id) ON DELETE CASCADE,
  platform_code VARCHAR(10) NOT NULL,
  ghl_post_id VARCHAR(100),
  platform_post_id VARCHAR(100),
  platform_post_url TEXT,
  posted_at TIMESTAMPTZ,
  ghl_status VARCHAR(30),
  ghl_error_message TEXT,
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_posts_content ON posts(content_piece_id);
CREATE INDEX idx_posts_platform ON posts(platform_code);
CREATE INDEX idx_posts_posted ON posts(posted_at);
```

### `post_analytics`

```sql
CREATE TABLE post_analytics (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  post_id UUID REFERENCES posts(id) ON DELETE CASCADE,
  snapshot_type VARCHAR(20) NOT NULL,
  impressions INTEGER DEFAULT 0,
  reach INTEGER DEFAULT 0,
  likes INTEGER DEFAULT 0,
  comments INTEGER DEFAULT 0,
  shares INTEGER DEFAULT 0,
  saves INTEGER DEFAULT 0,
  clicks INTEGER DEFAULT 0,
  engagement_rate DECIMAL(5,4),
  follower_change INTEGER DEFAULT 0,
  video_views INTEGER,
  video_watch_time_seconds INTEGER,
  pin_saves INTEGER,
  profile_visits INTEGER,
  custom_metrics JSONB,
  collected_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_analytics_post ON post_analytics(post_id);
CREATE INDEX idx_analytics_type ON post_analytics(snapshot_type);
```

### `post_comments`

```sql
CREATE TABLE post_comments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  post_id UUID REFERENCES posts(id) ON DELETE CASCADE,
  platform_comment_id VARCHAR(100),
  author_name VARCHAR(255),
  author_handle VARCHAR(255),
  comment_text TEXT,
  is_reply BOOLEAN DEFAULT false,
  parent_comment_id UUID REFERENCES post_comments(id),
  sentiment VARCHAR(20),
  auto_reply_sent BOOLEAN DEFAULT false,
  auto_reply_text TEXT,
  commented_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_comments_post ON post_comments(post_id);
```

### `api_usage_log`

```sql
CREATE TABLE api_usage_log (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  provider VARCHAR(30) NOT NULL,
  api_key_id VARCHAR(50),
  action VARCHAR(100) NOT NULL,
  endpoint VARCHAR(255),
  request_tokens INTEGER,
  response_tokens INTEGER,
  images_generated INTEGER DEFAULT 0,
  characters_used INTEGER DEFAULT 0,
  cost_usd DECIMAL(8,4),
  status VARCHAR(20),
  error_message TEXT,
  latency_ms INTEGER,
  created_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_usage_provider ON api_usage_log(provider);
CREATE INDEX idx_usage_created ON api_usage_log(created_at);
CREATE INDEX idx_usage_status ON api_usage_log(status);
```

### `api_rate_limit_status`

```sql
CREATE TABLE api_rate_limit_status (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  provider VARCHAR(30) NOT NULL UNIQUE,
  tier VARCHAR(30) NOT NULL,
  current_daily_usage INTEGER DEFAULT 0,
  daily_limit INTEGER,
  current_minute_usage INTEGER DEFAULT 0,
  minute_limit INTEGER,
  current_concurrent INTEGER DEFAULT 0,
  concurrent_limit INTEGER,
  current_monthly_chars INTEGER DEFAULT 0,
  monthly_char_limit INTEGER,
  current_month_cost DECIMAL(8,2) DEFAULT 0,
  monthly_budget_limit DECIMAL(8,2),
  daily_reset_at TIMESTAMPTZ,
  monthly_reset_at TIMESTAMPTZ,
  last_rate_limited_at TIMESTAMPTZ,
  updated_at TIMESTAMPTZ DEFAULT now()
);
```

### `ai_agent_logs`

```sql
CREATE TABLE ai_agent_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  agent_name VARCHAR(50) NOT NULL,
  action VARCHAR(100) NOT NULL,
  target_type VARCHAR(50),
  target_id UUID,
  input_summary TEXT,
  output_summary TEXT,
  model_used VARCHAR(50),
  tokens_input INTEGER,
  tokens_output INTEGER,
  duration_ms INTEGER,
  status VARCHAR(20),
  error_message TEXT,
  created_at TIMESTAMPTZ DEFAULT now()
);
CREATE INDEX idx_agent_logs_agent ON ai_agent_logs(agent_name);
CREATE INDEX idx_agent_logs_target ON ai_agent_logs(target_type, target_id);
CREATE INDEX idx_agent_logs_created ON ai_agent_logs(created_at);
```

### `settings`

```sql
CREATE TABLE settings (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  category VARCHAR(50) NOT NULL,
  key VARCHAR(100) NOT NULL,
  value JSONB NOT NULL,
  updated_at TIMESTAMPTZ DEFAULT now(),
  UNIQUE(category, key)
);
```

---

## 3. Views

```sql
CREATE VIEW v_pipeline_summary AS
SELECT
  ws.year, ws.week_number, ws.date_start, ws.date_end,
  t.title as topic_title,
  p.name as pillar_name, p.color_hex,
  ws.production_status,
  COUNT(cp.id) FILTER (WHERE cp.status = 'draft') as drafts,
  COUNT(cp.id) FILTER (WHERE cp.status IN ('in_review','ready_for_review')) as in_review,
  COUNT(cp.id) FILTER (WHERE cp.status = 'approved') as approved,
  COUNT(cp.id) FILTER (WHERE cp.status IN ('ghl_queued','ghl_scheduled')) as scheduled,
  COUNT(cp.id) FILTER (WHERE cp.status = 'posted') as posted,
  COUNT(cp.id) as total_pieces
FROM weekly_schedule ws
LEFT JOIN topics t ON ws.topic_id = t.id
LEFT JOIN pillars p ON ws.pillar_id = p.id
LEFT JOIN content_pieces cp ON cp.schedule_id = ws.id
GROUP BY ws.id, t.title, p.name, p.color_hex;

CREATE VIEW v_content_flow AS
SELECT
  cp.id, cp.piece_code, cp.content_type_code,
  cp.awareness_level, cp.status, cp.phase,
  cp.scheduled_date, cp.day_of_week,
  t.title as topic_title,
  p.name as pillar_name, p.color_hex as pillar_color,
  ws.year, ws.week_number,
  (SELECT file_url FROM content_assets ca
   WHERE ca.content_piece_id = cp.id AND ca.image_group = 'group_a'
   AND ca.slide_number IS NULL LIMIT 1) as preview_image
FROM content_pieces cp
JOIN topics t ON cp.topic_id = t.id
JOIN pillars p ON t.pillar_id = p.id
LEFT JOIN weekly_schedule ws ON cp.schedule_id = ws.id
ORDER BY cp.scheduled_date DESC NULLS LAST;

CREATE VIEW v_analytics_overview AS
SELECT
  po.platform_code, cp.content_type_code, cp.phase,
  p.name as pillar_name, cp.awareness_level,
  AVG(pa.engagement_rate) as avg_engagement_rate,
  SUM(pa.impressions) as total_impressions,
  SUM(pa.likes + pa.comments + pa.shares + pa.saves) as total_engagement,
  COUNT(DISTINCT po.id) as post_count
FROM post_analytics pa
JOIN posts po ON pa.post_id = po.id
JOIN content_pieces cp ON po.content_piece_id = cp.id
JOIN topics t ON cp.topic_id = t.id
JOIN pillars p ON t.pillar_id = p.id
WHERE pa.snapshot_type = '7d'
GROUP BY po.platform_code, cp.content_type_code, cp.phase, p.name, cp.awareness_level;

CREATE VIEW v_api_usage_daily AS
SELECT
  provider, DATE(created_at) as usage_date,
  COUNT(*) as total_calls,
  COUNT(*) FILTER (WHERE status = 'success') as successful,
  COUNT(*) FILTER (WHERE status = 'rate_limited') as rate_limited,
  COUNT(*) FILTER (WHERE status = 'error') as errors,
  SUM(images_generated) as images,
  SUM(request_tokens + response_tokens) as total_tokens,
  SUM(cost_usd) as total_cost
FROM api_usage_log
GROUP BY provider, DATE(created_at)
ORDER BY usage_date DESC;
```

---

## 4. Storage Buckets

```
content-assets/
  ├── images/{content_piece_id}/
  │   ├── group_a.png
  │   ├── group_b.png
  │   ├── group_c.png
  │   └── carousel/
  │       ├── slide-01-group_a.png ...
  ├── videos/
  ├── audio/
  └── thumbnails/
blog-assets/
  ├── featured-images/
  └── inline-images/
brand-assets/
  ├── logos/
  ├── templates/
  └── fonts/
```

---

## 5. Edge Functions

| Function | Trigger | Purpose |
|----------|---------|---------|
| `generate-master-brief` | CRON (weekly Mon 7am) | Claude → Master Brief |
| `jules-create-content` | Master Brief approved | Jules → briefs + images + copy |
| `gemini-create-blogs` | Master Brief approved | Gemini → blogs + overviews (Phase 2) |
| `review-content` | Content ready | Claude → 16-point review |
| `push-to-ghl` | Content approved | Create GHL posts |
| `sync-ghl-status` | CRON (daily 6am) | Poll GHL for status |
| `collect-analytics` | CRON (daily midnight) | Pull analytics from GHL |
| `sync-product-cache` | CRON (weekly Sun midnight) + on-demand | GHL Products → product_cache |
| `reset-api-counters` | CRON (daily midnight PT) | Reset NanaBanana/Gemini daily counters |
| `weekly-report` | CRON (weekly Mon 8am) | Performance summary |

---

## 6. Seed Data

```sql
-- API rate limit status
INSERT INTO api_rate_limit_status
  (provider, tier, daily_limit, concurrent_limit, minute_limit, monthly_char_limit, monthly_budget_limit)
VALUES
  ('jules', 'free', 15, 3, NULL, NULL, 0),
  ('nanabanana', 'pro', 100, NULL, 60, NULL, 19.99),
  ('claude', 'build_tier1', NULL, NULL, 50, NULL, 50.00),
  ('gemini', 'free_studio', 1500, NULL, 10, NULL, 0),
  ('elevenlabs', 'creator', NULL, NULL, NULL, 100000, 22.00);

-- Pillars: seed 7 from DATABASE_PILLARS.md
-- Topics: import ~140 from Content_Topics.tsv
-- Weekly Schedule: import from Weekly_Topic.tsv
-- Settings: brand kit, platform configs, image dimension groups, posting defaults
```
