# Viatrexx GHL Integration Specification

**Version:** 2.2 (March 2026)

---

## 1. Overview

```
Dashboard (Supabase) ──── push ────► GHL Social Planner ────► Platforms
                     ◄── sync ────   (FB, IG, LI, Pin)
Dashboard (Supabase) ──── fetch ───► GHL Products API ────► product_cache
```

---

## 2. Authentication

```
Method: Private Integration Token (PIT)
Header: Authorization: Bearer {GHL_PIT_TOKEN}
Version: 2021-07-28
Base URL: https://services.leadconnectorhq.com
```

---

## 3. API Endpoints

### Social Media

| Action | Method | Endpoint |
|--------|--------|----------|
| List Accounts | GET | `/social-media-posting/oauth/{locationId}` |
| Create Post | POST | `/social-media-posting/post` |
| Get Post | GET | `/social-media-posting/post/{postId}` |
| Delete Post | DELETE | `/social-media-posting/post/{postId}` |
| Upload Media | POST | `/medias/upload` |

### Products

| Action | Method | Endpoint |
|--------|--------|----------|
| List Products | GET | `/products/` |
| Get Product by ID | GET | `/products/{productId}` |

**Products Query Parameters:** `locationId`, `search` (name filter), `limit`, `offset`

**Products Response (key fields):**
```json
{
  "products": [{
    "_id": "prod_abc123",
    "name": "Viatrexx-Systemic Dx",
    "description": "...",
    "image": "https://storage.googleapis.com/.../systemic-dx.webp",
    "medias": [{ "url": "...", "type": "image", "title": "Front View" }]
  }]
}
```

---

## 4. Image Group Handling

FB and LI share the same Group A image (1080×1080). One upload serves both platforms.

```javascript
async function pushContentPieceToGHL(piece, assets, copyRecords) {
  const mediaByGroup = {};
  for (const asset of assets) {
    if (!mediaByGroup[asset.image_group]) {
      mediaByGroup[asset.image_group] = await uploadMediaToGHL(asset.file_url, asset.file_name, LOCATION_ID);
    }
  }

  const platformMediaMap = {
    'PL01': mediaByGroup['group_a'],  // Facebook
    'PL03': mediaByGroup['group_a'],  // LinkedIn (shared)
    'PL02': mediaByGroup['group_b'],  // Instagram
    'PL04': mediaByGroup['group_c'],  // Pinterest
  };

  for (const platformCode of piece.target_platforms) {
    const copy = copyRecords.find(c => c.platform_code === platformCode);
    await createGHLPost({
      locationId: LOCATION_ID,
      accountId: getAccountIdForPlatform(platformCode),
      platform: getPlatformType(platformCode),
      mediaIds: [platformMediaMap[platformCode]],
      caption: copy.caption,
      scheduledDate: calculatePostingTime(piece.scheduled_date, platformCode, piece.day_of_week),
      tags: buildTags(piece),
      firstComment: copy.first_comment
    });
  }
}
```

---

## 5. Platform Account Mapping

```json
{
  "platform_accounts": {
    "PL01_facebook": { "ghl_account_id": "{id}", "image_group": "group_a", "posting_times": { "weekday": "09:00", "weekend": "10:00" } },
    "PL02_instagram": { "ghl_account_id": "{id}", "image_group": "group_b", "posting_times": { "weekday": "08:30", "weekend": "10:00" } },
    "PL03_linkedin": { "ghl_account_id": "{id}", "image_group": "group_a", "posting_times": { "weekday": "08:00" } },
    "PL04_pinterest": { "ghl_account_id": "{id}", "image_group": "group_c", "posting_times": { "weekday": "19:00", "weekend": "19:00" } }
  },
  "product_catalog": {
    "location_id": "{GHL_LOCATION_ID}",
    "cache_ttl_days": 7,
    "auto_sync": "weekly_sunday_midnight",
    "image_field": "image",
    "media_field": "medias"
  }
}
```

---

## 6. Status Sync (Daily CRON)

```javascript
async function syncGHLStatuses() {
  const { data: pendingPosts } = await supabase
    .from('posts')
    .select('id, ghl_post_id, ghl_status, content_piece_id')
    .not('ghl_status', 'in', '("published","failed")');

  for (const post of pendingPosts) {
    const ghlPost = await fetchGHLPost(post.ghl_post_id);
    if (ghlPost.status !== post.ghl_status) {
      await supabase.from('posts').update({
        ghl_status: ghlPost.status,
        posted_at: ghlPost.status === 'published' ? ghlPost.publishedAt : null,
        platform_post_url: ghlPost.postUrl || null
      }).eq('id', post.id);
    }
  }
}
```

---

## 7. Rate Limits

| API | Burst | Daily |
|-----|-------|-------|
| GHL Social Planner | 100 / 10 seconds | 200,000 / day |
| GHL Products | 100 / 10 seconds | 200,000 / day |

Product image fetching is ~10 calls/week (cached). Social posting is ~28–52 posts/week. Well within limits.

---

## 8. GHL Tags

```
viatrexx-content, week-{N}, pillar-{code}, type-{CT}, piece-{code},
awareness-{level}, phase-{N}, image-group-{group}
```

---

## 9. Error Handling

| Error | Response |
|-------|----------|
| 401 Unauthorized | Alert admin, pause pushes |
| 429 Rate Limited | Exponential backoff, retry |
| 400 Bad Request | Log, flag post |
| Media upload fail | Retry 2×, flag asset |
| Post creation fail | Retry 2×, move back to approved |
| Product not found | Use fallback (brand icon), log warning |
