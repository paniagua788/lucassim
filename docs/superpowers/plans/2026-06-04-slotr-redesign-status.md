# Slotr Page Redesign — Status & Continuation Guide

> **Last updated:** 2026-06-04
> **Current state:** Page updated with categorized features (17 features, 5 categories). Visual redesign NOT started yet.
> **Branch:** main (pushed to origin)

---

## What's Done ✅

### 1. Content Update (COMPLETED & PUSHED)
- **Spec:** `docs/superpowers/specs/2026-06-04-slotr-page-update-design.md`
- **Plan:** `docs/superpowers/plans/2026-06-04-slotr-page-update.md`
- **File modified:** `src/pages/slotr.astro`
- **Commits:**
  - `6629153` docs: add Slotr page update design spec
  - `4f1f092` refactor(slotr): replace flat features with categorized data structure
  - `568fc59` feat(slotr): render features as categorized sections with Nuevo badge

### 2. Current Feature Structure (in `slotr.astro`)
17 features organized in 5 categories:
| Category | Features |
|---|---|
| Reservas (4) | Reservas online, Múltiples servicios, Multi-servicios, Categorías y precios |
| Gestión (5) | Gestión de agenda, Staff y recursos, Panel administrativo, Bloqueos con motivo, Permisos granulares |
| Comunicación (4) | Notificaciones, Confirmación por email, Recordatorios automáticos, Confirmación por WhatsApp |
| Marketing (2) | Eventos y Promociones (badge "Nuevo"), Reseñas de clientes |
| Analytics (2) | Dashboard de métricas, Personalización |

---

## What's Pending 🔄

### Visual Redesign — Bento Grid Style (NOT STARTED)

**Decisions already made:**
- **Style:** Bento Grid (cards of varying sizes, hierarchical layout)
- **Hero:** Option C — Animated background with floating geometric shapes + CSS-only animations + grid overlay
- **Icons:** Replace ALL emojis with inline SVG icons (Lucide-style, stroke 1.5px, rounded corners)
- **Color scheme:** Keep existing violet/purple brand (#7c3aed, #a855f7, #c084fc) — dark background (#0a0a0f)
- **Constraints:** 100% static page (Astro), no JS runtime, no backend logic, Cloudflare Pages compatible
- **Anti-patterns to avoid:** Emojis as icons, generic AI look, flat uniform grid

**Mockups created (visual companion at localhost:50937, server may be stopped):**
1. `hero-mockup.html` — Hero with animated floating shapes + grid overlay + floating SVG icons
2. `bento-grid-mockup.html` — Feature cards in bento layout, featured card for Eventos
3. `full-page-mockup.html` — Complete page: nav + hero + bento grid + pricing + CTA

**What needs to be designed and implemented:**

| Step | Description | Files |
|---|---|---|
| 1 | **Hero redesign** — Replace current hero with animated background (CSS keyframes), gradient text, floating shapes | `src/pages/slotr.astro` hero section |
| 2 | **Icon system** — Create inline SVG icon components or constants to replace all emojis | New file or inline in astro |
| 3 | **Bento grid for features** — Replace categorized sections with bento grid layout (featured cards span 2 cols, others 1 col) | `src/pages/slotr.astro` features section |
| 4 | **Section redesign** — Redesign "Para quién es", pricing, and CTA sections to match new style | `src/pages/slotr.astro` remaining sections |
| 5 | **CSS updates** — Add animation keyframes, bento grid styles, card hover effects to `src/styles/global.css` or inline | `src/styles/global.css` |
| 6 | **Build verification** — `npm run build` must pass | — |

---

## Design Specs for Continuation

### Hero (Option C — Approved)
```
- Background: #0a0a0f (near-black)
- Animated shapes: 3-4 blurred circles with radial gradients (violet tones)
- Grid overlay: subtle 60px grid with radial mask
- Text: gradient from white → violet → purple
- Badge: pill with border, uppercase "SaaS · Agendamiento"
- CTA: gradient button (violet → purple) with hover lift + shadow
- Animations: CSS-only @keyframes float (20s ease-in-out infinite)
```

### Icon Mapping (emoji → SVG Lucide-style)
| Emoji | Feature | SVG Icon Name |
|---|---|---|
| 📅 | Reservas online | `calendar` |
| 🛎️ | Múltiples servicios | `list` |
| 🧩 | Multi-servicios | `link` |
| 📂 | Categorías y precios | `folder` |
| 📆 | Gestión de agenda | `grid` |
| 👥 | Staff y recursos | `users` |
| ⚙️ | Panel administrativo | `settings` |
| 🚫 | Bloqueos con motivo | `lock` |
| 🔐 | Permisos granulares | `shield` |
| 🔔 | Notificaciones | `bell` |
| 📧 | Confirmación por email | `mail` |
| ⏰ | Recordatorios automáticos | `clock` |
| 💬 | Confirmación por WhatsApp | `message-circle` |
| 🎉 | Eventos y Promociones | `layers` |
| ⭐ | Reseñas de clientes | `star` |
| 📊 | Dashboard de métricas | `activity` |
| 🎨 | Personalización | `palette` |

### Bento Grid Layout
```
Row 1: [Eventos y Promociones — span 2] [Reservas online]
Row 2: [Gestión de agenda] [Multi-servicios] [Notificaciones]
Row 3: [Dashboard] [Staff y recursos] [Personalización]
Row 4: [Reseñas] [Confirmación email] [Recordatorios]
Row 5: [Bloqueos con motivo] [Permisos granulares] [Categorías y precios]
```

### Tailwind Classes to Use
- Background: `bg-[#0a0a0f]` or keep existing `bg-gradient-to-b from-slotr-dark to-base`
- Cards: `bg-white/[0.03] border border-white/[0.06] rounded-2xl`
- Hover: `hover:border-violet-500/30 hover:-translate-y-0.5 transition-all`
- Featured card: `bg-gradient-to-br from-violet-500/10 to-purple-500/5 border-violet-500/25`
- Badge "Nuevo": `bg-violet-500/20 text-violet-300 text-[10px] font-bold uppercase tracking-wider px-2 py-0.5 rounded`
- Grid: `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4`
- Span 2: `md:col-span-2`

---

## Next Steps to Continue

1. **Pull latest:** `git pull origin main`
2. **Review current state:** Open `src/pages/slotr.astro` to see the categorized features
3. **Start implementation:** Follow the steps in the table above (Hero → Icons → Bento Grid → Sections → CSS → Build)
4. **Reference mockups:** The 3 HTML mockups are in `\tmp\brainstorm\content\` (may need to regenerate if server stopped)
5. **Build verification:** Run `npm run build` after each major change

---

## Key Files
| File | Purpose |
|---|---|
| `src/pages/slotr.astro` | Main page — needs visual redesign |
| `src/components/FeatureCard.astro` | Feature card component — may need update for SVG icons |
| `src/styles/global.css` | Global styles — add animations, bento grid styles |
| `src/layouts/BaseLayout.astro` | Layout wrapper — likely unchanged |

## Commands
```bash
npm run dev       # Preview at http://localhost:4321
npm run build     # Verify build (required before commit)
npm run preview   # Preview production build
```
