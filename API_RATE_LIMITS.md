# Viatrexx AI API Rate Limits & Tracking

**Version:** 1.1 (March 2026)

---

## 1. Rate Limits by Provider

### Jules AI (Free Tier)

| Metric | Limit | Reset |
|--------|-------|-------|
| Daily Tasks | 15 | Rolling 24h |
| Concurrent | 3 | Slot frees on task completion |

Paid: AI Pro (~75/day, $19.99/mo) · AI Ultra (~300/day, $124.99/mo)

### NanaBanana 2 (AI Pro)

| Metric | Limit | Reset |
|--------|-------|-------|
| Daily Images | ~100 | Midnight PT |
| Max Resolution | 2K (2048×2048) | — |
| RPM (API) | 10–60 | Per-minute rolling |

### Claude (Anthropic, Build Tier 1)

| Metric | Limit | Reset |
|--------|-------|-------|
| RPM | 50 | Per-minute rolling |
| TPM | 40,000 | Per-minute rolling |

Sonnet pricing: ~$3/M input, ~$15/M output tokens. Weekly usage: ~8 calls, ~36K tokens ≈ $0.50.

### Gemini AI (Free Studio, Phase 2)

| Metric | Limit | Reset |
|--------|-------|-------|
| Daily Requests | 1,500 | Midnight PT |
| RPM | 10 | Per-minute rolling |

### ElevenLabs (Creator, Phase 4)

| Metric | Limit | Reset |
|--------|-------|-------|
| Monthly Characters | 100,000 | Monthly billing |

### GHL Products API

| Metric | Limit |
|--------|-------|
| Burst | 100 requests / 10 seconds |
| Daily | 200,000 requests / day |

Product image fetching: ~10 calls/week (cached). Negligible usage.

---

## 2. Phase 1 Jules Free-Tier Task Budget

### Weekly Task Distribution

| Day | Tasks | Description |
|-----|-------|-------------|
| Monday | 4 | 7 Content Type Briefs (1) + Platform Briefs by group (3) |
| Tuesday | 5 | Images: SP1, SP2, SP3, INF1, INF2 (1 each, includes Remotion compositing) |
| Wednesday | 4 | Carousel images (2) + captions (2) |
| Thursday | 2 | Alt text + assembly |
| Fri–Sun | 0 (buffer) | Revision tasks if needed (15/day available) |
| **Total** | **15** + 45 buffer | — |

### NanaBanana Image Budget

| Day | Images | Description |
|-----|--------|-------------|
| Tuesday | 15 | 5 pieces × 3 groups |
| Wednesday | 60 | 2 carousels × 10 slides × 3 groups |
| **Total** | **75** | Within ~100/day limit (spread across 2 days) |

---

## 3. Supabase Tracking Tables

### `api_usage_log`

Logs every API call: provider, action, tokens, images, cost, status, latency.

### `api_rate_limit_status`

Live counters per provider: current daily usage vs. limit, concurrent count, monthly cost vs. budget, reset timers.

See DATABASE_SCHEMA.md for full table definitions.

---

## 4. Settings Page: API Analytics Panel

Each provider gets a monitoring card:

```
┌──────────────────────────────────────┐
│  JULES AI                [Free]     │
│  Daily: ████████░░░░░  12/15 (80%) │
│  Concurrent: ██░░░░░░  2/3         │
│  Resets in: 6h 23m                  │
│  This week: 47 tasks | 0 rate hits  │
│  [7-day sparkline chart]            │
└──────────────────────────────────────┘
```

Similar cards for NanaBanana, Claude, Gemini, ElevenLabs.

**Dashboard Health Strip:**
```
API: Jules 12/15 ██████░░ | NanaBanana 62/100 ██████░ | Claude ✅ | Gemini — | Voice —
```

Color: Green (<60%), Yellow (60–85%), Red (>85%), Gray (inactive).

**Alerts:** >80% daily limit, rate limit hit, >80% monthly budget, auth error.

---

## 5. Pre-Flight Check

```javascript
async function canExecuteTask(provider, taskCount = 1) {
  const status = await supabase.from('api_rate_limit_status')
    .select('*').eq('provider', provider).single();
  if (status.daily_limit && (status.current_daily_usage + taskCount) > status.daily_limit)
    return { allowed: false, reason: 'daily_limit', resets_at: status.daily_reset_at };
  if (status.concurrent_limit && status.current_concurrent >= status.concurrent_limit)
    return { allowed: false, reason: 'concurrent_limit' };
  if (status.monthly_budget_limit && status.current_month_cost >= status.monthly_budget_limit)
    return { allowed: false, reason: 'budget_exceeded' };
  return { allowed: true };
}
```

On daily limit: queue for tomorrow. On concurrent limit: wait 60s + retry.

---

## 6. Minimum Viable Stack (Phase 1)

| Provider | Tier | Monthly Cost |
|----------|------|-------------|
| Jules | Free | $0 |
| NanaBanana | AI Pro | $19.99 |
| Claude | Build T1 | ~$2 usage |
| GHL Products | Included | $0 |
| Remotion | Self-hosted | $0 |
| **Total** | — | **~$22/month** |
