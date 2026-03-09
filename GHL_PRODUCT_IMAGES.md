# GHL Product Image Integration

**Version:** 1.0 (March 2026)

---

## 1. Overview

When a content brief references Viatrexx products, the system fetches real product photos from GHL and composites them into generated content via Remotion MCP.

```
Master Brief → products_referenced: ["Systemic Dx", "Lymph 1"]
  │
  Content Manager → GHL Products API → product_cache (Supabase)
  │
  Jules receives product image URLs in brief context
  │
  NanaBanana generates background → Remotion MCP overlays product photo → final PNG
```

---

## 2. GHL Products API

### List Products

```
GET https://services.leadconnectorhq.com/products/
  ?locationId={GHL_LOCATION_ID}&search=Systemic+Dx&limit=1
Headers: Authorization: Bearer {GHL_PIT_TOKEN}, Version: 2021-07-28
```

### Get Product by ID

```
GET https://services.leadconnectorhq.com/products/{productId}
  ?locationId={GHL_LOCATION_ID}
```

### Response Fields

```json
{
  "_id": "prod_abc123",
  "name": "Viatrexx-Systemic Dx",
  "image": "https://storage.googleapis.com/msgsndr/.../systemic-dx.webp",
  "medias": [
    { "url": "https://...", "type": "image", "title": "Front View" },
    { "url": "https://...", "type": "image", "title": "Angle View" }
  ]
}
```

---

## 3. Product Cache

`product_cache` table in Supabase (see DATABASE_SCHEMA.md). 7-day TTL, weekly full sync via CRON, lazy refresh on cache miss.

### Lookup Function

```javascript
async function getProductImages(productNames) {
  const results = [];
  for (const name of productNames) {
    const normalized = name.toLowerCase().replace(/[^a-z0-9]/g, '');
    let { data: cached } = await supabase
      .from('product_cache')
      .select('*')
      .ilike('product_name_normalized', `%${normalized}%`)
      .gt('expires_at', new Date().toISOString())
      .limit(1).single();

    if (!cached) {
      const response = await fetch(`${GHL_BASE}/products/?locationId=${LOC_ID}&search=${encodeURIComponent(name)}&limit=1`,
        { headers: { 'Authorization': `Bearer ${TOKEN}`, 'Version': '2021-07-28' } });
      const data = await response.json();
      if (data.products?.length > 0) {
        const p = data.products[0];
        const { data: inserted } = await supabase.from('product_cache').upsert({
          ghl_product_id: p._id,
          product_name: p.name,
          product_name_normalized: p.name.toLowerCase().replace(/[^a-z0-9]/g, ''),
          primary_image_url: p.image || p.medias?.[0]?.url,
          media_urls: p.medias || [],
          cached_at: new Date().toISOString(),
          expires_at: new Date(Date.now() + 7*24*60*60*1000).toISOString()
        }, { onConflict: 'ghl_product_id' }).select().single();
        cached = inserted;
      }
    }
    if (cached) results.push({ product_name: cached.product_name, primary_image_url: cached.primary_image_url, all_media: cached.media_urls });
  }
  return results;
}
```

---

## 4. Template Product Image Zones

Templates that support product images include a `product_image_zone`:

| Template | When Product Appears | Position |
|----------|---------------------|----------|
| SP-PROOF (SP3) | Always | center-right, 30% |
| SP-FRAME (SP2) | Sometimes | small thumbnail beside step |
| INF-PROCESS (INF2) | Sometimes | conclusion step |
| CAR-CONVERT slides 3–7 | When slide references product | right-aligned, 20% |
| CAR-CONVERT slide 10 (CTA) | Always | centered above CTA, 35% |

```json
{
  "product_image_zone": {
    "enabled": true,
    "position": "center-right",
    "size_percent": 30,
    "background_treatment": "drop-shadow, slight-rotation(-5deg)",
    "fallback": "brand_prism_icon",
    "compositing_tool": "remotion_mcp"
  }
}
```

---

## 5. Compositing Strategies

**Strategy A: Remotion MCP Overlay (primary)**

Jules generates the NanaBanana background leaving a clean zone, then uses Remotion MCP to layer the product photo with drop shadow and positioning, and exports the final composite PNG.

**Strategy B: NanaBanana Reference Image**

For simpler compositions, pass the product URL as a reference image to NanaBanana with inpainting instructions.

---

## 6. Error Handling

| Scenario | Handling |
|----------|---------|
| Product not found in GHL | Skip product image, use fallback icon |
| Product has no image | Use placeholder text |
| GHL rate limited | Retry with backoff, use cache |
| Image URL broken (404) | Re-fetch from GHL, update cache |
| Cache expired | Lazy refresh or weekly sync |
