# Jules AI — Connected MCP Servers & Remotion Integration

**Version:** 1.0 (March 2026)

---

## 1. Connected MCP Servers

| MCP Server | Purpose | Phase |
|------------|---------|-------|
| **Supabase** | DB read/write — briefs, content, assets, copy, product_cache | All |
| **Remotion** | Image compositing (product overlays), video rendering (reels) | All |
| **Remotion Media** | NanaBanana image gen + ElevenLabs voice via MCP | All |
| **Linear** | Task/issue tracking for weekly production cycles | All |
| **Neon** | Serverless Postgres edge data access | All |
| **Stitch** | Data integration, ETL, analytics sync | All |
| **V0** | UI component generation for dashboard | Build |
| **Render** | Deployment, Remotion render workers | All |
| **Context7** | Live API documentation retrieval | All |

---

## 2. Usage by Pipeline Stage

### Brief Generation

```
Context7 → latest template specs
Supabase → topic, pillar, SEO, product_cache
Jules generates briefs
Supabase → write briefs
Linear → update task status
```

### Image Generation

```
Supabase → product image URLs from product_cache
NanaBanana API → background images (3 groups)
IF product overlay needed:
  Remotion MCP → composite product onto background → export PNG
Supabase → upload images, create content_assets
Linear → "Images Complete"
```

### Carousel Creation

```
NanaBanana → slide backgrounds (10 slides × 3 groups)
Remotion MCP → product overlays on relevant slides
Remotion MCP (optional) → compile slides into video (Phase 3)
Supabase → write all carousel assets
```

### Reel Production (Phase 3)

```
NanaBanana → visual assets
Supabase → product images
Remotion MCP → full reel composition:
  ├── remotion_create_project(1080×1920, 30fps)
  ├── remotion_add_title_scene (hook, 3s)
  ├── remotion_add_image_content (background + product)
  ├── remotion_add_title_scene (CTA end card)
  └── render → MP4
```

---

## 3. Remotion MCP Configuration

```json
{
  "mcpServers": {
    "remotion": { "url": "http://localhost:3000/mcp" },
    "remotion-media": {
      "command": "npx",
      "args": ["remotion-media-mcp"],
      "env": {
        "KIE_API_KEY": "${NANABANANA_API_KEY}",
        "ELEVENLABS_API_KEY": "${ELEVENLABS_API_KEY}"
      }
    }
  }
}
```

### Tools Used

| Tool | Purpose | Phase |
|------|---------|-------|
| `create_video` | Create composition (image or video) | All |
| `remotion_add_image_content` | Add background or product layer | All |
| `remotion_add_title_scene` | Animated text overlays | Phase 3+ |
| `generate_image` | NanaBanana via Remotion | All |
| `generate_voiceover` | ElevenLabs via Remotion | Phase 4 |

---

## 4. Linear Task Tracking

Auto-created per week:

```
Week 11 Cycle:
  ├── Master Brief (Claude)
  ├── Content Type Briefs (Jules)
  ├── Platform Briefs (Jules)
  ├── Image Generation (Jules/NanaBanana)
  ├── Copywriting (Jules)
  ├── Assembly (Jules)
  ├── Review (Claude)
  └── GHL Push (Content Manager)
```

---

## 5. Image Budget Impact

Product compositing uses Remotion (free/self-hosted) and does NOT increase NanaBanana calls. Background = 1 NanaBanana call. Overlay = Remotion layer.

| Step | Tool | Budget Impact |
|------|------|--------------|
| Background | NanaBanana | Unchanged (75/week) |
| Product overlay | Remotion MCP | No cost |
| Export | Remotion MCP | No cost |

---

## 6. Full MCP Config

```json
{
  "jules_mcp_servers": {
    "supabase": { "url": "https://mcp.supabase.com/mcp" },
    "remotion": { "url": "http://localhost:3000/mcp" },
    "remotion-media": { "command": "npx", "args": ["remotion-media-mcp"] },
    "linear": { "url": "https://mcp.linear.app/sse" },
    "neon": { "url": "https://mcp.neon.tech/sse" },
    "stitch": {},
    "v0": { "url": "https://v0.dev/mcp" },
    "render": {},
    "context7": {}
  }
}
```
