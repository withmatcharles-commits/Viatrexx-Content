# Viatrexx Phase 1 Content Templates

**Version:** 1.1 (March 2026)
**Purpose:** Base templates for Jules + NanaBanana. All image prompts are NanaBanana-ready JSON. Product image zones defined for Remotion MCP compositing.

---

## 1. Brand Visual System

### Colors

```json
{
  "primary_blue": "#0056b3", "dark_blue": "#004494", "secondary_blue": "#188bf6",
  "green": "#37ca37", "teal": "#4ECDC4", "dark_text": "#2c3e50",
  "gray": "#cbd5e0", "light_bg": "#f8f9fa", "white": "#ffffff", "gold": "#F59E0B"
}
```

### Typography

```json
{
  "headline": { "font": "Montserrat", "weight": "700", "size": "48-64px" },
  "subhead": { "font": "Montserrat", "weight": "600", "size": "28-36px" },
  "body": { "font": "Lato", "weight": "400", "size": "18-24px" },
  "caption": { "font": "Inter", "weight": "400", "size": "14-16px" }
}
```

### Style Rules

```json
{
  "aesthetic": "Clean, clinical-yet-warm, nature-meets-science",
  "avoid": ["Stethoscopes", "Pills/capsules", "Stock photo feel", "Cartoon/clipart", "Miracle cure imagery"],
  "include": ["Nature elements", "Cellular/molecular patterns", "Prism/spectrum effects", "Flow/pathway imagery"]
}
```

---

## 2. Template: SP-STAT (SP1 — TOFU Statistic Highlight)

```json
{
  "template_id": "SP-STAT",
  "awareness_level": "TOFU",
  "piece_codes": ["SP1"],
  "product_image_zone": { "enabled": false },
  "layout": {
    "background": "Gradient #004494 → #4ECDC4, subtle cellular overlay 10%",
    "top": "Small white caps label (e.g., 'DID YOU KNOW?')",
    "center": "Large bold white stat text",
    "bottom": "1-2 line explanation. Logo bottom-right."
  },
  "nanabanana_prompts": {
    "group_a": {
      "dimensions": "1080x1080",
      "prompt": "Professional wellness infographic. Deep blue to teal gradient (#004494 to #4ECDC4). Subtle cellular pattern at 10% opacity. Top: white uppercase '{{LABEL}}'. Center: large bold white '{{STAT_TEXT}}' Montserrat Bold 64px. Below: lighter text '{{EXPLANATION}}'. Logo bottom-right. --ar 1:1 --style clean-medical"
    },
    "group_b": {
      "dimensions": "1080x1350",
      "prompt": "Portrait wellness infographic. Same gradient and layout as group_a adapted for 4:5. All text center 80% safe zone. --ar 4:5 --style clean-medical"
    },
    "group_c": {
      "dimensions": "1000x1500",
      "prompt": "Tall Pinterest wellness infographic. Same gradient. Content in upper 2/3. Large readable text. --ar 2:3 --style clean-medical"
    }
  },
  "example_fill": {
    "LABEL": "DID YOU KNOW?",
    "STAT_TEXT": "78% of Supplements Never Reach Your Cells",
    "EXPLANATION": "When your biological matrix is congested, even the best nutrients get blocked."
  }
}
```

---

## 3. Template: SP-FRAME (SP2 — MOFU Framework)

```json
{
  "template_id": "SP-FRAME",
  "awareness_level": "MOFU",
  "piece_codes": ["SP2"],
  "product_image_zone": {
    "enabled": true,
    "condition": "only_when_framework_references_product",
    "position": "beside relevant step, small thumbnail",
    "size_percent": 15,
    "compositing_tool": "remotion_mcp",
    "fallback": "omit (no product image if not referenced)"
  },
  "layout": {
    "background": "White #f8f9fa with blue accent",
    "top": "Pillar badge + bold dark headline",
    "center": "Diagram/framework with brand color accents",
    "bottom": "One-line takeaway. Logo bottom-right."
  },
  "nanabanana_prompts": {
    "group_a": {
      "dimensions": "1080x1080",
      "prompt": "Clean educational infographic. White (#f8f9fa) background. Top: blue (#0056b3) badge '{{PILLAR_LABEL}}'. Bold dark headline '{{HEADLINE}}'. Center: {{DIAGRAM_TYPE}} diagram using blue/teal showing {{FRAMEWORK_DESCRIPTION}}. Bottom: takeaway '{{TAKEAWAY}}'. Logo bottom-right. --ar 1:1 --style clean-medical"
    },
    "group_b": { "dimensions": "1080x1350", "prompt": "Portrait version. Same layout, 4:5. Text in safe zone. --ar 4:5" },
    "group_c": { "dimensions": "1000x1500", "prompt": "Tall Pinterest version. Content upper 2/3. --ar 2:3" }
  },
  "example_fill": {
    "PILLAR_LABEL": "DETOX & REGENERATION",
    "HEADLINE": "Drainage vs. Detox: They're Not the Same",
    "DIAGRAM_TYPE": "two-column comparison",
    "FRAMEWORK_DESCRIPTION": "Left: Drainage (opening pathways). Right: Detox (cellular cleaning). Arrow: drainage first.",
    "TAKEAWAY": "Always drain before you detox."
  }
}
```

---

## 4. Template: SP-PROOF (SP3 — BOFU Proof & CTA)

```json
{
  "template_id": "SP-PROOF",
  "awareness_level": "BOFU",
  "piece_codes": ["SP3"],
  "product_image_zone": {
    "enabled": true,
    "position": "center-right",
    "size_percent": 30,
    "background_treatment": "drop-shadow, slight-rotation(-5deg)",
    "fallback": "brand_prism_icon",
    "compositing_tool": "remotion_mcp"
  },
  "layout": {
    "background": "Dark blue #004494 gradient",
    "top": "Bold white proof headline",
    "center_left": "Proof text + product reference in teal",
    "center_right": "PRODUCT IMAGE ZONE (30% width)",
    "bottom": "Green CTA button + logo"
  },
  "nanabanana_prompts": {
    "group_a": {
      "dimensions": "1080x1080",
      "prompt": "Premium wellness post. Dark blue (#004494) gradient. Bold white headline '{{PROOF_HEADLINE}}'. Center-left: white proof text '{{PROOF_POINT}}' with gold accent. Product ref '{{PRODUCT_REF}}' in teal. CENTER-RIGHT: clean 300x400px zone with subtle dark gradient for product overlay. Green CTA button '{{CTA_TEXT}}'. Logo bottom-right. --ar 1:1 --style premium-medical"
    },
    "group_b": { "dimensions": "1080x1350", "prompt": "Portrait premium. Same layout for 4:5. Product zone center-right. Text in safe zone. --ar 4:5" },
    "group_c": { "dimensions": "1000x1500", "prompt": "Tall premium. Product zone in center. Content upper 2/3. --ar 2:3" }
  },
  "example_fill": {
    "PROOF_HEADLINE": "1 Squirt = 5 Drops of Precision",
    "PROOF_POINT": "Our calibrated spray system delivers exact dosing every time.",
    "PRODUCT_REF": "Viatrexx Spray Delivery System",
    "CTA_TEXT": "Learn More → Link in Bio"
  }
}
```

---

## 5. Template: INF-DATA (INF1 — TOFU/MOFU Data Visualization)

```json
{
  "template_id": "INF-DATA",
  "awareness_level": "TOFU-MOFU",
  "piece_codes": ["INF1"],
  "product_image_zone": { "enabled": false },
  "layout": {
    "header": "Blue bar with white headline",
    "data_zone": "2-4 data points with numbers, icons, labels",
    "bottom": "Source line + logo"
  },
  "nanabanana_prompts": {
    "group_a": {
      "dimensions": "1080x1080",
      "prompt": "Data infographic. White background. Top: blue (#0056b3) header bar, white text '{{HEADLINE}}'. Center: {{DATA_LAYOUT}} showing {{DATA_POINTS}}. Brand color accents. Source line bottom-left. Logo bottom-right. --ar 1:1 --style data-infographic"
    },
    "group_b": { "dimensions": "1080x1350", "prompt": "Portrait data infographic. Vertical layout. --ar 4:5" },
    "group_c": { "dimensions": "1000x1500", "prompt": "Tall Pinterest data infographic. Large text. --ar 2:3" }
  },
  "data_layout_options": ["3-column", "vertical stack", "circular stats", "bar chart", "comparison table"],
  "example_fill": {
    "HEADLINE": "The Matrix Stagnation Problem",
    "DATA_LAYOUT": "3 vertical stat blocks",
    "DATA_POINTS": "'78%' matrix congestion in blue, '3x' drainage effectiveness in teal, '4 squirts' daily dosing in green"
  }
}
```

---

## 6. Template: INF-PROCESS (INF2 — MOFU/BOFU Process Map)

```json
{
  "template_id": "INF-PROCESS",
  "awareness_level": "MOFU-BOFU",
  "piece_codes": ["INF2"],
  "product_image_zone": {
    "enabled": true,
    "condition": "only_at_conclusion_step",
    "position": "beside final step",
    "size_percent": 20,
    "compositing_tool": "remotion_mcp",
    "fallback": "omit"
  },
  "layout": {
    "header": "Bold headline with blue accent",
    "flow": "3-5 numbered steps connected by arrows",
    "conclusion": "Final step → CTA/product",
    "bottom": "Logo"
  },
  "nanabanana_prompts": {
    "group_a": {
      "dimensions": "1080x1080",
      "prompt": "Process-flow infographic. White background. Dark headline '{{HEADLINE}}' with blue underline. {{STEP_COUNT}} steps with numbered blue circles, teal arrow connections. Final step green conclusion '{{CONCLUSION}}'. Logo bottom-right. --ar 1:1 --style process-diagram"
    },
    "group_b": { "dimensions": "1080x1350", "prompt": "Portrait process flow. Vertical steps. --ar 4:5" },
    "group_c": { "dimensions": "1000x1500", "prompt": "Tall process flow. Generous spacing. --ar 2:3" }
  },
  "example_fill": {
    "HEADLINE": "The Viatrexx Terrain Restoration Pathway",
    "STEP_COUNT": "3",
    "CONCLUSION": "Clear Terrain → Ready for Healing"
  }
}
```

---

## 7. Template: CAR-EDUCATE (CAR1 — TOFU→MOFU Educational Carousel)

### Visual Consistency System

All slides share: progressive gradient (blue→teal→green), consistent accent line at bottom, slide numbering, font sizes. Logo on slides 1 and 10 only.

```json
{
  "template_id": "CAR-EDUCATE",
  "awareness_level": "TOFU-MOFU",
  "piece_codes": ["CAR1"],
  "slide_count": 10,
  "product_image_zone": { "enabled": false },
  "visual_system": {
    "background_flow": "Progressive gradient: deep blue → teal → return to blue+green",
    "accent_bar": "Thin line at bottom, color shifts across slides",
    "slide_number": "Top-right, semi-transparent white",
    "logo": "Slide 1 (top-left) and Slide 10 (bottom-right)"
  },
  "slides": {
    "slide_1_HOOK": {
      "prompt_group_a": "Slide 1/10 educational carousel. Deep blue gradient (#004494→#0056b3). Subtle organic pattern 5%. Large bold white centered '{{HOOK_TEXT}}'. 1/10 top-right. Logo top-left. Teal accent line bottom. --ar 1:1"
    },
    "slide_2_PROBLEM": {
      "prompt_group_a": "Slide 2/10. Slightly lighter blue. Red X icon. White problem text '{{PROBLEM_TEXT}}'. 2/10 top-right. --ar 1:1"
    },
    "slides_3_to_8_VALUE": {
      "prompt_group_a": "Slide {{N}}/10. Gradient shifting blue→teal. Bold white heading '{{POINT_HEADING}}'. Body text '{{POINT_BODY}}'. {{N}}/10 top-right. --ar 1:1"
    },
    "slide_9_SUMMARY": {
      "prompt_group_a": "Slide 9/10. Teal gradient. Checkmark icon. Bold white '{{SUMMARY_TEXT}}'. 9/10 top-right. --ar 1:1"
    },
    "slide_10_CTA": {
      "prompt_group_a": "Slide 10/10 final. Deep blue + green accent. Bold CTA '{{CTA_TEXT}}'. Instruction '{{CTA_INSTRUCTION}}'. Prominent logo. 10/10 top-right. --ar 1:1"
    }
  },
  "note": "Group B (4:5) and Group C (2:3) prompts follow same structure with adapted aspect ratios and safe zones."
}
```

---

## 8. Template: CAR-CONVERT (CAR2 — MOFU→BOFU Conversion Carousel)

```json
{
  "template_id": "CAR-CONVERT",
  "awareness_level": "MOFU-BOFU",
  "piece_codes": ["CAR2"],
  "slide_count": 10,
  "visual_system": {
    "background_flow": "Dark premium gradient (#004494→#556270) with gold accents",
    "accent": "Gold (#F59E0B) lines and highlights"
  },
  "slides": {
    "slide_1_HOOK": {
      "product_image_zone": { "enabled": false },
      "prompt_group_a": "Slide 1/10 premium carousel. Dark gradient (#004494→#556270). Gold accent top. Bold white '{{HOOK_TEXT}}'. Teal subtext '{{HOOK_SUBTEXT}}'. 1/10 top-right. Logo top-left. --ar 1:1 --style premium-carousel"
    },
    "slide_2_FRAMEWORK_INTRO": {
      "product_image_zone": { "enabled": false },
      "prompt_group_a": "Slide 2/10. Warmer gradient. Structural icon. '{{FRAMEWORK_TITLE}}'. Body explanation. Gold accent. 2/10 top-right. --ar 1:1"
    },
    "slides_3_to_7_DEEP_VALUE": {
      "product_image_zone": {
        "enabled": true,
        "condition": "only_when_slide_references_product",
        "position": "right-aligned-center",
        "size_percent": 20,
        "compositing_tool": "remotion_mcp"
      },
      "prompt_group_a": "Slide {{N}}/10. Dark gradient. Gold circle step number '{{STEP_NUM}}'. Bold heading '{{STEP_HEADING}}'. Detail text '{{STEP_DETAIL}}'. Product in teal '{{PRODUCT_REF}}'. RIGHT SIDE: clean zone for optional product overlay. {{N}}/10 top-right. --ar 1:1 --style premium-carousel"
    },
    "slide_8_PROOF": {
      "product_image_zone": { "enabled": false },
      "prompt_group_a": "Slide 8/10 proof. Dark blue. Teal quote marks. '{{PROOF_TEXT}}'. Attribution '{{PROOF_SOURCE}}'. 8/10 top-right. --ar 1:1"
    },
    "slide_9_SUMMARY": {
      "product_image_zone": { "enabled": false },
      "prompt_group_a": "Slide 9/10. Dark teal gradient. Summary '{{SUMMARY_TEXT}}'. Gold accent. 9/10 top-right. --ar 1:1"
    },
    "slide_10_CTA": {
      "product_image_zone": {
        "enabled": true,
        "position": "centered-above-cta",
        "size_percent": 35,
        "background_treatment": "glow-effect",
        "compositing_tool": "remotion_mcp"
      },
      "prompt_group_a": "Slide 10/10 CTA. Deep blue. CENTER: clean zone for product image with glow. Green CTA button '{{CTA_TEXT}}' below. Lead text '{{CTA_LEAD}}'. Prominent logo. 10/10 top-right. --ar 1:1 --style premium-carousel"
    }
  },
  "example_fill": {
    "HOOK_TEXT": "Why Your Patients Keep Plateauing",
    "HOOK_SUBTEXT": "The 3-Step Protocol Most Practitioners Miss",
    "FRAMEWORK_TITLE": "The Terrain Restoration Protocol",
    "STEP_NUM": "1",
    "STEP_HEADING": "Step 1: Open the Drainage Pathways",
    "STEP_DETAIL": "Viatrexx-Lymph 1 targets deep lymphatic congestion while Mesenchyme clears the extracellular matrix.",
    "PRODUCT_REF": "Viatrexx-Lymph 1 + Mesenchyme",
    "PROOF_TEXT": "After drainage-first protocols, my complex cases resolved 3× faster.",
    "PROOF_SOURCE": "— Dr. K., ND, Vancouver",
    "SUMMARY_TEXT": "Drain → Detox → Regenerate: The Order Matters",
    "CTA_TEXT": "Get the Full Protocol →",
    "CTA_LEAD": "Ready to resolve your toughest cases?"
  }
}
```

---

## 9. Template Usage Rules

### Selection Logic

```
SP1 → SP-STAT  |  SP2 → SP-FRAME  |  SP3 → SP-PROOF
INF1 → INF-DATA  |  INF2 → INF-PROCESS
CAR1 → CAR-EDUCATE  |  CAR2 → CAR-CONVERT
```

### Variable Replacement

Jules fills `{{VARIABLE}}` placeholders from Master Brief data. Key mappings: `{{HOOK_TEXT}}` ← `key_messages.tofu`, `{{PILLAR_LABEL}}` ← pillar name, `{{CTA_TEXT}}` ← brief CTA, `{{PRODUCT_REF}}` ← `products_referenced`.

### NanaBanana Prompt Assembly

1. Select template prompt for piece_code + image group
2. Replace `{{VARIABLES}}`
3. Append: `--no stethoscope, pills, stock photo, cartoon, clipart, miracle`
4. Append style tag
5. Send to NanaBanana 2 API

### Product Image Compositing

For templates with `product_image_zone.enabled = true`:
1. NanaBanana generates background with clean zone for product
2. Jules calls Remotion MCP to layer product photo (from GHL product_cache)
3. Remotion exports final composite PNG
4. If no product image available, use `fallback` (brand icon or omit)

### Carousel Consistency

All 10 slides in a set must use the same template. Background gradient shifts ~5% per slide. Accent line color progresses. Slide numbering on every slide. Logo on slides 1 and 10 only. All text in center 80% safe zone.
