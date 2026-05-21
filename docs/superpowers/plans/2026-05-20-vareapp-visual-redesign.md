# VareApp Visual Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rediseño visual completo de la página VareApp con hero animado, bento grid de categorías con tamaño variable, iconos SVG Lucide y estilos CSS naranja.

**Architecture:** Página 100% estática en Astro. Se reutiliza el componente CategoryCard existente (adaptando colores naranja). Se crean nuevos iconos SVG para VareApp. Hero con animaciones CSS puras. Todo en archivos existentes.

**Tech Stack:** Astro, Tailwind CSS v4, SVG inline, CSS keyframes

---

## File Structure

| File | Action | Responsibility |
|---|---|---|
| `src/styles/global.css` | Modify | Add VareApp orange animation/card/CTA classes |
| `src/components/vareapp-icons.ts` | Create | 11 feature SVG icons + 5 hero food icons |
| `src/pages/vareapp.astro` | Modify | Hero, bento grid layout, pricing, CTA sections |

Note: CategoryCard.astro is reused from Slotr — no changes needed since it accepts dynamic colors via Tailwind classes passed through props.

---

### Task 1: Add VareApp Orange CSS Classes

**Files:**
- Modify: `src/styles/global.css`

- [ ] **Step 1: Add VareApp orange utility classes to global.css**

Add to the end of `src/styles/global.css` (after the existing Slotr classes):

```css
/* VareApp Orange Variants */
.vareapp-card {
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.vareapp-card:hover {
  transform: translateY(-2px);
  border-color: rgba(249, 115, 22, 0.3);
}

.vareapp-cta {
  background: linear-gradient(135deg, #f97316, #ea580c);
  box-shadow: 0 4px 14px rgba(249, 115, 22, 0.35);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.vareapp-cta:hover {
  transform: translateY(-1px);
  box-shadow: 0 6px 20px rgba(249, 115, 22, 0.45);
}

.vareapp-gradient-text {
  background: linear-gradient(135deg, #ffffff 0%, #fb923c 50%, #f97316 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

- [ ] **Step 2: Verify build still passes**

Run: `npm run build`
Expected: Build succeeds without errors

- [ ] **Step 3: Commit**

```bash
git add src/styles/global.css
git commit -m "style(vareapp): add orange card hover, CTA and gradient text utilities"
```

---

### Task 2: Create VareApp SVG Icon System

**Files:**
- Create: `src/components/vareapp-icons.ts`

- [ ] **Step 1: Create vareapp-icons.ts with 16 SVG icons**

Create `src/components/vareapp-icons.ts`:

```typescript
// Lucide-style SVG icons for VareApp features + hero floating food icons
// stroke-width: 1.5, rounded corners, 24x24 viewBox

export const vareappIcons = {
  // Feature icons
  bookOpen: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/></svg>`,

  clipboardList: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect x="8" y="2" width="8" height="4" rx="1" ry="1"/><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"/><path d="M12 11h4"/><path d="M12 16h4"/><path d="M8 11h.01"/><path d="M8 16h.01"/></svg>`,

  settings: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0 .33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9c.26.604.852.997 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>`,

  creditCard: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect x="1" y="4" width="22" height="16" rx="2" ry="2"/><line x1="1" y1="10" x2="23" y2="10"/></svg>`,

  package: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M16.5 9.4l-9-5.19M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg>`,

  barChart3: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M3 3v18h18"/><path d="M18 17V9"/><path d="M13 17V5"/><path d="M8 17v-3"/></svg>`,

  userCheck: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><polyline points="16 11 18 13 22 9"/></svg>`,

  printer: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 6 2 18 2 18 9"/><path d="M6 18H4a2 2 0 0 1-2-2v-5a2 2 0 0 1 2-2h16a2 2 0 0 1 2 2v5a2 2 0 0 1-2 2h-2"/><rect x="6" y="14" width="12" height="8"/></svg>`,

  bot: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 8V4H8"/><rect x="2" y="8" width="20" height="12" rx="2"/><circle cx="8" cy="14" r="1.5"/><circle cx="16" cy="14" r="1.5"/><path d="M9 18h6"/></svg>`,

  palette: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="13.5" cy="6.5" r="2.5"/><circle cx="17.5" cy="10.5" r="2.5"/><circle cx="8.5" cy="7.5" r="2.5"/><circle cx="6.5" cy="12.5" r="2.5"/><path d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12c0 2.215.72 4.265 1.94 5.93"/></svg>`,

  image: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"/><circle cx="9" cy="9" r="2"/><path d="M21 15l-3.086-3.086a2 2 0 0 0-2.828 0L6 21"/></svg>`,

  // Hero floating food icons
  chefHat: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M6 13.87A4 4 0 0 1 7.41 6a5.11 5.11 0 0 1 1.05-1.54 5 5 0 0 1 7.08 0A5.11 5.11 0 0 1 16.59 6 4 4 0 0 1 18 13.87V21H6z"/><line x1="6" y1="17" x2="18" y2="17"/></svg>`,

  utensilsCrossed: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M3 2v7c0 1.1.9 2 2 2h4a2 2 0 0 0 2-2V2"/><path d="M7 2v20"/><path d="M21 15V2a5 5 0 0 0-5 5v6c0 1.1.9 2 2 2h3zm0 0v7"/></svg>`,

  flame: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M8.5 14.5A2.5 2.5 0 0 0 11 12c0-1.38-.5-2-1-3-1.072-2.143-.224-4.054 2-6 .5 2.5 2 4.9 4 6.5 2 1.6 3 3.5 3 5.5a7 7 0 1 1-14 0c0-1.153.433-2.294 1-3a2.5 2.5 0 0 0 2.5 2.5z"/></svg>`,

  coffee: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M17 8h1a4 4 0 1 1 0 8h-1"/><path d="M3 8h14v9a4 4 0 0 1-4 4H7a4 4 0 0 1-4-4Z"/><line x1="6" y1="2" x2="6" y2="4"/><line x1="10" y1="2" x2="10" y2="4"/><line x1="14" y1="2" x2="14" y2="4"/></svg>`,

  pizza: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2L2 22h20L12 2z"/><circle cx="10" cy="13" r="1"/><circle cx="14" cy="10" r="1"/><circle cx="8" cy="9" r="1"/></svg>`,
} as const;

export type VareappIconName = keyof typeof vareappIcons;
```

- [ ] **Step 2: Verify TypeScript compiles**

Run: `npx tsc --noEmit src/components/vareapp-icons.ts`
Expected: No errors

- [ ] **Step 3: Commit**

```bash
git add src/components/vareapp-icons.ts
git commit -m "feat(vareapp): add SVG icon system with 11 feature + 5 hero food icons"
```

---

### Task 3: Redesign Hero Section

**Files:**
- Modify: `src/pages/vareapp.astro`

- [ ] **Step 1: Update imports**

Replace the imports at the top of vareapp.astro:

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import Navbar from '../components/Navbar.astro';
import Footer from '../components/Footer.astro';
import ContactButtons from '../components/ContactButtons.astro';
import { vareappIcons } from '../components/vareapp-icons';

const WHATSAPP = 'https://wa.me/595993294266';
const EMAIL    = 'lucas_paniagua@hotmail.com';
---
```

Remove the `FeatureCard` import.

- [ ] **Step 2: Replace hero section**

Replace the existing hero section (lines 39-54) with:

```astro
  <!-- HERO -->
  <section class="relative overflow-hidden bg-[#0a0a0f] py-24 text-center px-6">
    <!-- Animated shapes -->
    <div class="slotr-shape absolute top-[15%] left-[12%] w-[180px] h-[180px] rounded-full" style="background: radial-gradient(circle, rgba(249,115,22,0.25), transparent 70%); filter: blur(40px);"></div>
    <div class="slotr-shape-reverse absolute top-[55%] right-[10%] w-[220px] h-[220px] rounded-full" style="background: radial-gradient(circle, rgba(234,88,12,0.2), transparent 70%); filter: blur(50px);"></div>
    <div class="slotr-shape absolute bottom-[10%] left-[35%] w-[140px] h-[140px] rounded-full" style="background: radial-gradient(circle, rgba(251,146,60,0.15), transparent 70%); filter: blur(35px);"></div>
    <div class="slotr-shape-reverse absolute top-[25%] right-[28%] w-[100px] h-[100px] rounded-full" style="background: radial-gradient(circle, rgba(249,115,22,0.18), transparent 70%); filter: blur(30px);"></div>

    <!-- Grid overlay -->
    <div class="absolute inset-0" style="background-image: linear-gradient(rgba(249,115,22,0.04) 1px, transparent 1px), linear-gradient(90deg, rgba(249,115,22,0.04) 1px, transparent 1px); background-size: 60px 60px; mask-image: radial-gradient(ellipse at center, black 30%, transparent 70%); -webkit-mask-image: radial-gradient(ellipse at center, black 30%, transparent 70%);"></div>

    <!-- Floating food icons -->
    <div class="slotr-icon-float absolute top-[15%] right-[15%]" style="opacity: 0.15;" aria-hidden="true">
      <span set:html={vareappIcons.chefHat} style="width:32px;height:32px;display:block;color:#fb923c;"></span>
    </div>
    <div class="slotr-icon-float-reverse absolute bottom-[20%] left-[12%]" style="opacity: 0.12;" aria-hidden="true">
      <span set:html={vareappIcons.utensilsCrossed} style="width:28px;height:28px;display:block;color:#f97316;"></span>
    </div>
    <div class="slotr-icon-float absolute top-[30%] left-[6%]" style="opacity: 0.10;" aria-hidden="true">
      <span set:html={vareappIcons.flame} style="width:24px;height:24px;display:block;color:#ea580c;"></span>
    </div>
    <div class="slotr-icon-float-reverse absolute bottom-[12%] right-[20%]" style="opacity: 0.12;" aria-hidden="true">
      <span set:html={vareappIcons.coffee} style="width:26px;height:26px;display:block;color:#fb923c;"></span>
    </div>
    <div class="slotr-icon-float absolute top-[50%] left-[22%]" style="opacity: 0.10;" aria-hidden="true">
      <span set:html={vareappIcons.pizza} style="width:22px;height:22px;display:block;color:#f97316;"></span>
    </div>

    <!-- Content -->
    <div class="relative z-10">
      <p class="text-xs font-bold uppercase tracking-widest text-vareapp mb-4 inline-block px-4 py-1.5 border border-orange-500/30 rounded-full">SaaS · Gastronomía</p>

      <img src="/vareapp-claro-transparente.png" alt="VareApp" class="h-20 mx-auto mb-4" />

      <h1 class="text-4xl font-black mb-3 vareapp-gradient-text leading-tight">Menú digital y pedidos para tu negocio</h1>

      <p class="text-sm text-muted max-w-md mx-auto mb-8 leading-relaxed">
        Sistema de menú digital y gestión de pedidos para restaurantes, cafeterías y food trucks en Paraguay.
      </p>

      <a
        href={WHATSAPP}
        target="_blank"
        rel="noopener noreferrer"
        class="inline-block px-8 py-3 rounded-lg text-sm font-bold text-white vareapp-cta"
      >
        Consultá por una demo
      </a>
    </div>
  </section>
```

- [ ] **Step 3: Verify build passes**

Run: `npm run build`
Expected: Build succeeds

- [ ] **Step 4: Commit**

```bash
git add src/pages/vareapp.astro
git commit -m "style(vareapp): redesign hero with animated shapes and floating food icons"
```

---

### Task 4: Replace Feature Sections with Bento Grid

**Files:**
- Modify: `src/pages/vareapp.astro`

- [ ] **Step 1: Update feature data structure**

Replace the `features` array with categorized data:

```typescript
const featureCategories = [
  {
    heading: 'Pedidos',
    description: 'Todo para que tus clientes pidan fácil.',
    icon: 'bookOpen' as const,
    span: 5,
    features: [
      { icon: 'bookOpen' as const, name: 'Menú digital', description: 'Catálogo con categorías, variantes, extras, fotos y combinaciones. Stock diario configurable. Logo personalizado en el encabezado.' },
      { icon: 'clipboardList' as const, name: 'Gestión de pedidos', description: 'Pedidos en tiempo real para Delivery, Pickup y Mesa (con número de mesa). Notificación directa al negocio por WhatsApp.' },
      { icon: 'userCheck' as const, name: 'Modo mozo', description: 'Panel simplificado para mozos: toman pedidos por mesa directamente desde su celular, sin pasar por WhatsApp.' },
      { icon: 'printer' as const, name: 'Tickets de cocina', description: 'Comandas formato 80mm con detalle completo: items, variantes, extras y aclaraciones. Marcado automático de impresos.' },
    ],
  },
  {
    heading: 'Operaciones',
    description: 'Control total de tu restaurante.',
    icon: 'settings' as const,
    span: 7,
    features: [
      { icon: 'settings' as const, name: 'Panel administrativo', description: 'Control total: productos, horarios, cierres especiales, staff y configuración del negocio.' },
      { icon: 'creditCard' as const, name: 'Caja', description: 'Registro de ventas, venta directa, impresión de tickets y facturas electrónicas habilitadas por la DNIT.' },
      { icon: 'package' as const, name: 'Inventario', description: 'Control de stock con alertas de bajo inventario, registro de movimientos y trazabilidad por lote y vencimiento.' },
      { icon: 'bot' as const, name: 'Impresión automática', description: 'Agente que imprime pedidos nuevos automáticamente a impresora térmica ESC/POS. Sin intervención manual.' },
    ],
  },
  {
    heading: 'Negocio',
    description: 'Datos y estilo para tu marca.',
    icon: 'barChart3' as const,
    span: 6,
    features: [
      { icon: 'barChart3' as const, name: 'Métricas', description: 'Dashboard con ventas, productos más pedidos y horas pico.' },
      { icon: 'palette' as const, name: 'Personalización', description: '11 paletas de color y 6 opciones de fuente seleccionables. Tu menú digital con tu identidad visual.' },
    ],
  },
  {
    heading: 'Marketing',
    description: 'Atraé más clientes.',
    icon: 'image' as const,
    span: 6,
    features: [
      { icon: 'image' as const, name: 'Generador de flyers', description: 'Seleccioná productos, armá tu flyer y exportalo en PDF listo para imprimir o compartir.' },
    ],
  },
];
```

- [ ] **Step 2: Replace feature section with bento grid**

Replace the features section (lines 58-65) with:

```astro
    <!-- FUNCIONALIDADES -->
    <section class="py-16">
      <h2 class="text-xl font-black mb-2">¿Qué incluye VareApp?</h2>
      <p class="text-sm text-muted mb-8">Todo lo que necesitás para digitalizar tu negocio gastronómico.</p>

      <!-- Bento Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-4">
        {featureCategories.map(cat => (
          <div class={`vareapp-card rounded-2xl p-6 ${cat.heading === 'Marketing'
            ? 'bg-gradient-to-br from-orange-500/10 to-amber-500/5 border border-orange-500/25'
            : 'bg-white/[0.03] border border-white/[0.06]'
          } ${cat.span === 5 ? 'lg:col-span-5' : cat.span === 6 ? 'lg:col-span-6' : cat.span === 7 ? 'lg:col-span-7' : 'lg:col-span-1'}`}>
            <div class="mb-4">
              <h3 class="text-lg font-bold text-white flex items-center gap-2">
                <span class="text-vareapp" set:html={vareappIcons[cat.icon]} style="width:20px;height:20px;display:inline-block;"></span>
                {cat.heading}
              </h3>
              <p class="text-xs text-subtle mt-1">{cat.description}</p>
            </div>

            <div class={`grid gap-2.5 ${cat.features.length >= 4 ? 'grid-cols-1 md:grid-cols-2 lg:grid-cols-2' : cat.features.length >= 3 ? 'grid-cols-1 md:grid-cols-2' : 'grid-cols-1'}`}>
              {cat.features.map(f => (
                <div class="p-3 rounded-xl bg-white/[0.02] border border-white/[0.04]">
                  <span class="text-vareapp mb-1.5 block" set:html={vareappIcons[f.icon]} style="width:16px;height:16px;display:block;"></span>
                  <p class="text-[0.7rem] font-bold text-white mb-0.5">{f.name}</p>
                  <p class="text-[0.6rem] text-subtle leading-relaxed">{f.description}</p>
                </div>
              ))}
            </div>
          </div>
        ))}
      </div>
    </section>
```

- [ ] **Step 3: Verify build passes**

Run: `npm run build`
Expected: Build succeeds

- [ ] **Step 4: Commit**

```bash
git add src/pages/vareapp.astro
git commit -m "refactor(vareapp): replace feature sections with bento grid layout"
```

---

### Task 5: Redesign Pricing and CTA Sections

**Files:**
- Modify: `src/pages/vareapp.astro`

- [ ] **Step 1: Update pricing section styles**

Replace the pricing section styles to match the new design:

```astro
    <!-- PLANES -->
    <section class="py-12 border-t border-white/[0.06]">
```

Update the Esencial card classes:
```astro
        <div class="bg-white/[0.03] border border-white/[0.06] rounded-2xl p-6 flex flex-col">
```

Update the Pro card classes:
```astro
        <div class="bg-vareapp-dark/50 border border-orange-500/25 rounded-2xl p-6 flex flex-col">
```

Update the Pro "Consultar" button:
```astro
            class="block text-center py-2 rounded-lg text-xs font-bold border border-vareapp text-vareapp hover:bg-vareapp hover:text-white transition-colors">
```

- [ ] **Step 2: Update CTA section**

Replace the CTA section border:

```astro
    <!-- CTA FINAL -->
    <section class="py-16 text-center border-t border-white/[0.06]">
```

- [ ] **Step 3: Verify build passes**

Run: `npm run build`
Expected: Build succeeds

- [ ] **Step 4: Commit**

```bash
git add src/pages/vareapp.astro
git commit -m "style(vareapp): redesign pricing and CTA sections to match new style"
```

---

### Task 6: Final Verification and Preview

**Files:**
- All modified files

- [ ] **Step 1: Full build verification**

Run: `npm run build`
Expected: Build succeeds without errors or warnings

- [ ] **Step 2: Preview the page**

Run: `npm run preview`
Expected: Page loads at http://localhost:4321 with:
- Hero with animated orange shapes, grid overlay, 5 floating food icons, gradient text
- Bento grid with 4 category cards (spans 5, 7, 6, 6)
- SVG icons instead of emojis
- Pricing section with consistent styling
- CTA section at bottom

- [ ] **Step 3: Final commit with all changes**

```bash
git status
git add -A
git commit -m "style(vareapp): complete visual redesign — hero, bento grid, SVG icons"
```

- [ ] **Step 4: Push to remote**

```bash
git push origin main
```
