# DESIGN.md – GHL Content Dashboard Design System  
**Primary Build: Light Mode + Desktop Web Browser (≥1280px)**

## Theme Strategy (Enforced Order)
1. Light Mode + Desktop (web browser) ← THIS BUILD (100% focus)
2. Mobile Light (responsive)
3. Desktop Dark
4. Mobile Dark

Default theme = Light. Use next-themes for toggle (Top Bar), but all initial components and screenshots are polished Light Mode.

## Light Mode Color Tokens (Primary)
- Background: #ffffff / zinc-50
- Surface / Cards: #ffffff (with subtle 1px zinc-100 border)
- Border: zinc-200
- Text Primary: zinc-950
- Text Secondary: zinc-600
- Primary Accent: #2563eb (GHL Blue-600)
- AI / Jules Accent: #7c3aed (Violet-600) with soft glow
- Success: #16a34a
- Warning: #ca8a04
- Danger: #dc2626
- Hover: zinc-100
- Active Row: #f8fafc

## Typography & Spacing (Desktop Optimized)
- Font: Inter (system-ui)
- Headings: font-semibold tracking-[-0.02em]
- Body: text-sm leading-relaxed
- Container: max-w-[1440px] mx-auto px-8
- Sidebar: fixed 280px (collapsible to 72px on desktop)
- Top Bar: h-16
- Card radius: 16px (xl)
- Shadow: soft shadow-sm / shadow-md on hover
- Spacing scale: 4 (1rem) → 6 (1.5rem) → 8 (2rem) → generous white space

## Layout Rules (Desktop-First)
- Sidebar always visible on lg+ (1280px+)
- Main content area: pt-6 pb-12
- Tables: wide, comfortable padding, horizontal scroll only when necessary
- Modals: max-w-3xl, centered, soft shadow-2xl, 20px border-radius
- Drag & Drop: clean blue outline + subtle lift animation

## Component Standards (All shadcn/ui – Light Optimized)
- Buttons: clean, soft hover lift, primary = GHL Blue
- Data Tables: clean white, zebra #f8fafc, sticky header
- Badges: soft rounded-full, subtle borders
- Calendar: FullCalendar with light theme, clean grid
- All elements have 100% consistency across every page

CRITICAL: No dark colors in this generation. No timelines/Gantt. Mobile responsive but desktop layout is the hero.
