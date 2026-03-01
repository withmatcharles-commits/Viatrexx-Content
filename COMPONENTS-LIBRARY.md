# COMPONENTS-LIBRARY.md – GHL Content Management Dashboard  
**Light Desktop Version (Web Browser – Primary Build)**

**MANDATORY RULE**: Every screen, sub-page, component, modal, table, form, modal, tab, filter, drag-drop, card, etc. MUST use ONLY components, icons, styles, layouts and patterns defined here. No deviations. This guarantees 100% visual consistency across the entire application.

## 1. Global Layout & Shell
- **AppShell**: Fixed sidebar (280px wide, collapsible to 72px) + fixed top bar (64px) + main content area with `max-w-[1440px] mx-auto px-8 pt-6 pb-12`
- **Sidebar**: White background, subtle zinc-100 border-right, logo at top (text "GHL Content" with icon), scrollable nav links, bottom section for Settings + Logout
- **TopBar**: White, shadow-sm, contains: Global Search (left or center), Location Switcher (dropdown), Notifications Bell, Theme Toggle (placeholder icon), User Avatar (circular with dropdown), GHL Iframe Resize button (bottom-right corner)

## 2. Icons (Lucide React ONLY)
Import from `lucide-react`. Use `size={20}` consistently.
- Navigation: Home, Target (Pillars), List (Topics), FileText (Briefs), Calendar (Schedules), ListTodo (Queues), LibraryBig (Content Library), Image (Assets), BarChart3 (Analytics), Bot (Agents & Tasks), BookOpen (Knowledge Base), Palette (Brand Kit), Settings (Settings)
- Actions: Plus, Edit3, Trash2, Play, UploadCloud, ExternalLink, Eye, CheckCircle, XCircle, Clock
- Status: CheckCircle (Approved), AlertTriangle (Needs Edit), Clock (Scheduled), Zap (Live AI), Pause

## 3. Core UI Components (shadcn/ui + Tailwind – Light Desktop Optimized)
- **Button**: shadcn Button – variants: default (blue-600), outline, ghost, destructive. Sizes: sm / default / lg. Always soft hover lift.
- **Card**: shadcn Card – rounded-2xl, border-zinc-200, shadow-sm, bg-white. Inner padding p-6.
- **DataTable**: TanStack Table wrapped in shadcn. Features: global search, column visibility dropdown, advanced filters row, sortable headers, pagination, sticky header, row hover (zinc-50), Actions column (DropdownMenu with Edit/Delete/…).
- **Modal / Dialog**: shadcn Dialog – max-w-3xl (or 4xl for preview), rounded-3xl, bg-white, header with title + close X, footer with Cancel + Primary button (right aligned).
- **Tabs**: shadcn Tabs – underline style, full-width on sub-pages, pill style only for platform filters.
- **AdvancedFilterBar**: Horizontal flex with Search Input, MultiSelect, DateRangePicker, Clear All button. Chips for active filters.
- **SplitPane**: Resizable left/right (table + preview) – used for Briefs.
- **Kanban / Weekly Scheduler**: @dnd-kit sortable columns. Weekly: 7 equal columns (Mon-Sun) with drop zones. Kanban: vertical columns with cards.
- **Gallery Grid**: Responsive CSS grid (3-5 columns desktop), each item = Card with image/video thumbnail + overlay metadata + actions.
- **FullCalendar**: FullCalendar v6 – light theme, clean grid, no timelines, selectable events, week/month toggle.
- **MarkdownEditor**: TipTap with shadcn toolbar (bold, italic, headings, list, code, link). Split view: Editor | Live Preview.
- **StatusBadge**: Rounded-full, small text, variants: Draft (zinc), In Review (amber), Approved (green), Scheduled (blue), Posted (emerald), Needs Edit (red).
- **AgentCard / SessionCard**: Card with status dot (green pulse for live), avatar, name, current task line, progress ring.
- **KPI Card**: Large bold number, icon top-left, title, subtle trend arrow.
- **ContentCard**: For grid views – image preview (if any), title, status badge, platform icons, quick actions.

## 4. Forms & Inputs
- All forms: react-hook-form + zod.
- Inputs: shadcn Input, Textarea, Select, MultiSelect, DatePicker, Switch, ColorPicker (for Brand Kit).
- Consistent label + helper text + error styling.

## 5. Interaction Patterns
- **Drag & Drop**: Blue glow outline on hover + lift animation.
- **Bulk Actions**: Top table bar with “Select all” + bulk dropdown.
- **Row Actions**: Always last column → DropdownMenu (icon dots).
- **Loading States**: Skeleton shimmer (shadcn) for tables/cards.
- **Empty States**: Centered illustration + message + CTA button.
- **Realtime Updates**: Subtle green flash on Supabase change.

## 6. Consistency Rules (Enforce on every screen)
- Spacing: space-y-6 / space-x-4, px-8 container
- Typography: Inter, headings font-semibold tracking-tight, body text-sm
- Shadows: shadow-sm on cards, shadow-md on hover/modals
- Colors: Strictly Light Mode (white/zinc/blue-600/violet-600)
- Responsive: Desktop-first (sidebar always visible), collapses gracefully on <1280px
- GHL Iframe: Dynamic height via postMessage on every page load/resize

**Agent Instruction**: Before generating any screen, read this file. Then output code that references only these components, icons, and patterns. Never invent new styles.
