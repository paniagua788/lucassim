# Slotr Visual Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rediseño visual completo de la página Slotr con hero animado, bento grid de categorías con tamaño variable, iconos SVG y estilos CSS actualizados.

**Architecture:** Página 100% estática en Astro. Se reemplaza el componente FeatureCard genérico por un nuevo CategoryCard que renderiza categorías con sub-cards internas. Hero con animaciones CSS puras. Todo en archivos existentes.

**Tech Stack:** Astro, Tailwind CSS v4, SVG inline, CSS keyframes

---

## File Structure

| File | Action | Responsibility |
|---|---|---|
| `src/styles/global.css` | Modify | Add CSS animations (@keyframes float), new utility classes |
| `src/components/icons.ts` | Create | SVG icon constants (17 icons, Lucide-style) |
| `src/components/CategoryCard.astro` | Create | Category card with header + sub-cards grid |
| `src/components/FeatureCard.astro` | Keep (unused) | Legacy component, not imported by slotr.astro anymore |
| `src/pages/slotr.astro` | Modify | Hero, bento grid layout, pricing, CTA sections |

---

### Task 1: Add CSS Animations to global.css

**Files:**
- Modify: `src/styles/global.css`

- [ ] **Step 1: Add @keyframes float and animation utilities**

Add to the end of `src/styles/global.css`:

```css
@import "tailwindcss";

@theme {
  /* Colors */
  --color-base:         #111111;
  --color-surface:      #161616;
  --color-surface2:     #1a1a1a;
  --color-border:       #2a2a2a;
  --color-muted:        #888888;
  --color-subtle:       #555555;
  --color-vareapp:      #f97316;
  --color-vareapp-dark: #140800;
  --color-slotr:        #7c3aed;
  --color-slotr-dark:   #0d0a14;

  /* Typography */
  --font-sans: "Inter", system-ui, sans-serif;

  /* Border radius */
  --radius-card:  12px;
  --radius-inner: 8px;
}

/* Slotr Hero Animations */
@keyframes slotr-float {
  0%, 100% { transform: translate(0, 0) scale(1); }
  25% { transform: translate(15px, -20px) scale(1.05); }
  50% { transform: translate(-10px, 15px) scale(0.95); }
  75% { transform: translate(20px, 10px) scale(1.02); }
}

.slotr-shape {
  animation: slotr-float 20s ease-in-out infinite;
}

.slotr-shape-reverse {
  animation: slotr-float 25s ease-in-out infinite reverse;
}

.slotr-icon-float {
  animation: slotr-float 16s ease-in-out infinite;
}

.slotr-icon-float-reverse {
  animation: slotr-float 20s ease-in-out infinite reverse;
}

/* Slotr Card Hover Effects */
.slotr-card {
  transition: all 0.2s ease;
}

.slotr-card:hover {
  transform: translateY(-2px);
  border-color: rgba(124, 58, 237, 0.3);
}

/* Slotr CTA Button */
.slotr-cta {
  background: linear-gradient(135deg, #7c3aed, #a855f7);
  box-shadow: 0 4px 14px rgba(124, 58, 237, 0.35);
  transition: all 0.2s ease;
}

.slotr-cta:hover {
  transform: translateY(-1px);
  box-shadow: 0 6px 20px rgba(124, 58, 237, 0.45);
}

/* Slotr Gradient Text */
.slotr-gradient-text {
  background: linear-gradient(135deg, #ffffff 0%, #c084fc 50%, #7c3aed 100%);
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
git commit -m "style(slotr): add hero animations and card hover utilities"
```

---

### Task 2: Create SVG Icon System

**Files:**
- Create: `src/components/icons.ts`

- [ ] **Step 1: Create icon constants file**

Create `src/components/icons.ts` with all 17 SVG icons as string constants:

```typescript
// Lucide-style SVG icons for Slotr features
// stroke-width: 1.5, rounded corners, 24x24 viewBox

export const icons = {
  calendar: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>`,

  list: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"/><line x1="8" y1="12" x2="21" y2="12"/><line x1="8" y1="18" x2="21" y2="18"/><line x1="3" y1="6" x2="3.01" y2="6"/><line x1="3" y1="12" x2="3.01" y2="12"/><line x1="3" y1="18" x2="3.01" y2="18"/></svg>`,

  link: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"/><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"/></svg>`,

  folder: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg>`,

  grid: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>`,

  users: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>`,

  settings: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0 .33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9c.26.604.852.997 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>`,

  lock: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="11" width="18" height="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>`,

  shield: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>`,

  bell: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></svg>`,

  mail: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>`,

  clock: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>`,

  messageCircle: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"/></svg>`,

  sparkles: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>`,

  star: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>`,

  activity: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg>`,

  palette: `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><circle cx="13.5" cy="6.5" r="2.5"/><circle cx="17.5" cy="10.5" r="2.5"/><circle cx="8.5" cy="7.5" r="2.5"/><circle cx="6.5" cy="12.5" r="2.5"/><path d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12c0 2.215.72 4.265 1.94 5.93"/></svg>`,
} as const;

export type IconName = keyof typeof icons;
```

- [ ] **Step 2: Verify TypeScript compiles**

Run: `npx tsc --noEmit src/components/icons.ts`
Expected: No errors

- [ ] **Step 3: Commit**

```bash
git add src/components/icons.ts
git commit -m "feat(slotr): add SVG icon system with 17 Lucide-style icons"
```

---

### Task 3: Create CategoryCard Component

**Files:**
- Create: `src/components/CategoryCard.astro`

- [ ] **Step 1: Create CategoryCard.astro**

Create `src/components/CategoryCard.astro`:

```astro
---
import { icons, type IconName } from './icons';

interface Feature {
  icon: IconName;
  name: string;
  description: string;
  isNew?: boolean;
}

interface Props {
  heading: string;
  description: string;
  features: Feature[];
  icon: IconName;
  isNew?: boolean;
  span: number; // grid-column span value
}

const { heading, description, features, icon, isNew, span } = Astro.props;
---

<div class={`slotr-card bg-white/[0.03] border border-white/[0.06] rounded-2xl p-6 ${isNew ? '!bg-gradient-to-br !from-violet-500/10 !to-purple-500/5 !border-violet-500/25' : ''}`} style={`grid-column: span ${span};`}>
  <!-- Category Header -->
  <div class="mb-4">
    <h3 class="text-lg font-bold text-white flex items-center gap-2">
      <span class="text-slotr" set:html={icons[icon]} style="width:20px;height:20px;display:inline-block;"></span>
      {heading}
      {isNew && (
        <span class="bg-violet-500/20 text-violet-300 text-[10px] font-bold uppercase tracking-wider px-1.5 py-0.5 rounded">Nuevo</span>
      )}
    </h3>
    <p class="text-xs text-subtle mt-1">{description}</p>
  </div>

  <!-- Feature Sub-cards -->
  <div class={`grid gap-2.5 ${features.length >= 5 ? 'grid-cols-3' : features.length >= 3 ? 'grid-cols-2' : 'grid-cols-1'}`}>
    {features.map(f => (
      <div class={`p-3 rounded-xl ${isNew ? 'bg-white/[0.03] border border-violet-500/12' : 'bg-white/[0.02] border border-white/[0.04]'}`}>
        <span class="text-slotr mb-1.5 block" set:html={icons[f.icon]} style="width:16px;height:16px;display:block;"></span>
        <p class="text-[0.7rem] font-bold text-white mb-0.5">{f.name}</p>
        <p class="text-[0.6rem] text-subtle leading-relaxed">{f.description}</p>
      </div>
    ))}
  </div>
</div>
```

- [ ] **Step 2: Verify build passes**

Run: `npm run build`
Expected: Build succeeds

- [ ] **Step 3: Commit**

```bash
git add src/components/CategoryCard.astro
git commit -m "feat(slotr): add CategoryCard component with variable-size bento layout"
```

---

### Task 4: Redesign Hero Section

**Files:**
- Modify: `src/pages/slotr.astro`

- [ ] **Step 1: Replace hero section in slotr.astro**

Replace the existing hero section (lines 77-92) with:

```astro
  <!-- HERO -->
  <section class="relative overflow-hidden bg-[#0a0a0f] py-24 text-center px-6">
    <!-- Animated shapes -->
    <div class="slotr-shape absolute top-[15%] left-[12%] w-[180px] h-[180px] rounded-full" style="background: radial-gradient(circle, rgba(124,58,237,0.25), transparent 70%); filter: blur(40px);"></div>
    <div class="slotr-shape-reverse absolute top-[55%] right-[10%] w-[220px] h-[220px] rounded-full" style="background: radial-gradient(circle, rgba(168,85,247,0.2), transparent 70%); filter: blur(50px);"></div>
    <div class="slotr-shape absolute bottom-[10%] left-[35%] w-[140px] h-[140px] rounded-full" style="background: radial-gradient(circle, rgba(192,132,252,0.15), transparent 70%); filter: blur(35px);"></div>
    <div class="slotr-shape-reverse absolute top-[25%] right-[28%] w-[100px] h-[100px] rounded-full" style="background: radial-gradient(circle, rgba(124,58,237,0.18), transparent 70%); filter: blur(30px);"></div>

    <!-- Grid overlay -->
    <div class="absolute inset-0" style="background-image: linear-gradient(rgba(124,58,237,0.04) 1px, transparent 1px), linear-gradient(90deg, rgba(124,58,237,0.04) 1px, transparent 1px); background-size: 60px 60px; mask-image: radial-gradient(ellipse at center, black 30%, transparent 70%); -webkit-mask-image: radial-gradient(ellipse at center, black 30%, transparent 70%);"></div>

    <!-- Floating icons -->
    <div class="slotr-icon-float absolute top-[18%] right-[18%]" style="opacity: 0.15;">
      <span set:html={icons.calendar} style="width:32px;height:32px;display:block;color:#a855f7;"></span>
    </div>
    <div class="slotr-icon-float-reverse absolute bottom-[22%] left-[14%]" style="opacity: 0.12;">
      <span set:html={icons.users} style="width:28px;height:28px;display:block;color:#7c3aed;"></span>
    </div>
    <div class="slotr-icon-float absolute top-[35%] left-[8%]" style="opacity: 0.10;">
      <span set:html={icons.bell} style="width:24px;height:24px;display:block;color:#c084fc;"></span>
    </div>

    <!-- Content -->
    <div class="relative z-10">
      <p class="text-xs font-bold uppercase tracking-widest text-slotr mb-4 inline-block px-4 py-1.5 border border-violet-500/30 rounded-full">SaaS · Agendamiento</p>

      <img src="/slotr-morado-claro.png" alt="Slotr" class="h-16 mx-auto mb-4" />

      <h1 class="text-4xl font-black mb-3 slotr-gradient-text leading-tight">Turnos online, sin complicaciones</h1>

      <p class="text-sm text-muted max-w-md mx-auto mb-8 leading-relaxed">
        Sistema de turnos online para clínicas, peluquerías, consultoras y canchas deportivas en Paraguay.
      </p>

      <a
        href={WHATSAPP}
        target="_blank"
        rel="noopener noreferrer"
        class="inline-block px-8 py-3 rounded-lg text-sm font-bold text-white slotr-cta"
      >
        Consultá por una demo
      </a>
    </div>
  </section>
```

Also update the imports at the top of slotr.astro:

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import Navbar from '../components/Navbar.astro';
import Footer from '../components/Footer.astro';
import ContactButtons from '../components/ContactButtons.astro';
import CategoryCard from '../components/CategoryCard.astro';
import { icons } from '../components/icons';

const WHATSAPP = 'https://wa.me/595993294266';
const EMAIL    = 'lucas_paniagua@hotmail.com';
---
```

- [ ] **Step 2: Verify build passes**

Run: `npm run build`
Expected: Build succeeds

- [ ] **Step 3: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "style(slotr): redesign hero with animated shapes and gradient text"
```

---

### Task 5: Replace Feature Sections with Bento Grid

**Files:**
- Modify: `src/pages/slotr.astro`

- [ ] **Step 1: Update featureCategories data structure**

Replace the `featureCategories` array in slotr.astro with icon references:

```typescript
const featureCategories = [
  {
    heading: 'Reservas',
    description: 'Todo para que tus clientes reserven fácil.',
    icon: 'calendar' as const,
    span: 5,
    features: [
      { icon: 'calendar' as const, name: 'Reservas online', description: 'Página pública donde tus clientes reservan su turno sin llamar.' },
      { icon: 'list' as const, name: 'Múltiples servicios', description: 'Servicios con duración y rango de precios. Con 10 o más servicios, los clientes navegan por categoría primero.' },
      { icon: 'link' as const, name: 'Multi-servicios', description: 'Tus clientes pueden reservar varios servicios en una sola cita. El sistema calcula duración total y precio combinado automáticamente.' },
      { icon: 'folder' as const, name: 'Categorías y precios', description: 'Organizá tus servicios por categoría y mostrá rangos de precio para que el cliente tenga una idea clara antes de reservar.' },
    ],
  },
  {
    heading: 'Gestión',
    description: 'Control total de tu equipo y tu agenda.',
    icon: 'grid' as const,
    span: 7,
    features: [
      { icon: 'grid' as const, name: 'Gestión de agenda', description: 'Vista de calendario por recurso con bloqueos y cancelaciones.' },
      { icon: 'users' as const, name: 'Staff y recursos', description: 'Soporte para personas y recursos físicos, con roles admin/staff y permisos granulares por módulo.' },
      { icon: 'settings' as const, name: 'Panel administrativo', description: 'Configuración completa: horarios, servicios, bloqueos y ajustes del negocio.' },
      { icon: 'lock' as const, name: 'Bloqueos con motivo', description: 'Bloqueá turnos individuales o días completos indicando el motivo. Visible en la agenda para todo el equipo.' },
      { icon: 'shield' as const, name: 'Permisos granulares', description: 'Controlá quién ve y gestiona cada agenda. Permisos independientes por staff para agenda, bloqueos y configuración.' },
    ],
  },
  {
    heading: 'Comunicación',
    description: 'Mantené informados a tus clientes y a tu equipo.',
    icon: 'bell' as const,
    span: 5,
    features: [
      { icon: 'bell' as const, name: 'Notificaciones', description: 'Avisos instantáneos por Telegram al staff cuando un cliente reserva. Integración con bot de Telegram para mantener al equipo informado en tiempo real.' },
      { icon: 'mail' as const, name: 'Confirmación por email', description: 'Tus clientes reciben un email con los detalles de su turno al confirmar la reserva.' },
      { icon: 'clock' as const, name: 'Recordatorios automáticos', description: 'Emails de recordatorio enviados automáticamente antes del turno para reducir ausencias.' },
      { icon: 'messageCircle' as const, name: 'Confirmación por WhatsApp', description: 'Botón directo en la pantalla de confirmación para que el cliente envíe los datos de su turno por WhatsApp.' },
    ],
  },
  {
    heading: 'Marketing',
    description: 'Atraé más clientes y fidelizá a los que ya tenés.',
    icon: 'sparkles' as const,
    span: 4,
    isNew: true,
    features: [
      { icon: 'sparkles' as const, name: 'Eventos y Promociones', description: 'Creá promociones con descuentos porcentuales o fijos, notificaciones visuales con íconos y banners de color. Solo un evento activo a la vez. Tus clientes ven las ofertas directamente en la página de reservas.' },
      { icon: 'star' as const, name: 'Reseñas de clientes', description: 'Los clientes califican su experiencia con estrellas y texto. El puntaje promedio y las reseñas recientes se muestran en tu página pública.' },
    ],
  },
  {
    heading: 'Analytics',
    description: 'Datos claros para tomar mejores decisiones.',
    icon: 'activity' as const,
    span: 3,
    features: [
      { icon: 'activity' as const, name: 'Dashboard de métricas', description: 'KPIs de turnos e ingresos estimados, 5 gráficos por período (7/30/90 días), ranking de servicios, franjas horarias pico y clientes frecuentes.' },
      { icon: 'palette' as const, name: 'Personalización', description: '16 paletas de color, logo propio y etiquetas configurables. Tu sistema de turnos con tu identidad visual.' },
    ],
  },
];
```

- [ ] **Step 2: Replace feature sections with bento grid**

Replace the features section (lines 96-115) with:

```astro
    <!-- FUNCIONALIDADES -->
    <section class="py-16">
      <h2 class="text-xl font-black mb-2">¿Qué incluye Slotr?</h2>
      <p class="text-sm text-muted mb-8">Todo lo que necesitás para que tus clientes reserven solos.</p>

      <!-- Bento Grid -->
      <div class="grid grid-cols-12 gap-4">
        {featureCategories.map(cat => (
          <CategoryCard
            heading={cat.heading}
            description={cat.description}
            features={cat.features}
            icon={cat.icon}
            isNew={cat.isNew}
            span={cat.span}
          />
        ))}
      </div>
    </section>
```

- [ ] **Step 3: Verify build passes**

Run: `npm run build`
Expected: Build succeeds

- [ ] **Step 4: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "refactor(slotr): replace feature sections with bento grid layout"
```

---

### Task 6: Redesign Pricing and CTA Sections

**Files:**
- Modify: `src/pages/slotr.astro`

- [ ] **Step 1: Update pricing section styles**

Replace the pricing section (lines 133-163) with:

```astro
    <!-- PRECIOS -->
    <section class="py-12 border-t border-white/[0.06]">
      <h2 class="text-xl font-black mb-2">Precio según tu equipo</h2>
      <p class="text-sm text-muted mb-2">Pagás por los calendarios que usás. Sin costos fijos por funciones que no necesitás.</p>
      <p class="text-xs text-subtle mb-8">Precio base incluye 1 recurso/calendario. Cada recurso adicional tiene un costo adicional.</p>

      <div class="flex flex-col gap-3 max-w-lg">
        {pricingRanges.map(r => (
          <div class={`flex items-center justify-between rounded-2xl px-5 py-4 border ${
            r.featured
              ? 'bg-slotr-dark/50 border-violet-500/25'
              : 'bg-white/[0.03] border-white/[0.06]'
          }`}>
            <div>
              <p class={`text-sm font-bold ${r.featured ? 'text-white' : 'text-muted'}`}>{r.range}</p>
              <p class="text-xs text-subtle mt-0.5">{r.example}</p>
            </div>
            <a
              href={WHATSAPP}
              target="_blank"
              rel="noopener noreferrer"
              class={`text-xs font-semibold whitespace-nowrap ml-6 hover:underline transition-all ${
                r.featured ? 'text-slotr' : 'text-subtle hover:text-muted'
              }`}
            >
              Consultá →
            </a>
          </div>
        ))}
      </div>
    </section>
```

- [ ] **Step 2: Update CTA section styles**

Replace the CTA section (lines 165-170) with:

```astro
    <!-- CTA FINAL -->
    <section class="py-16 text-center border-t border-white/[0.06]">
      <h2 class="text-2xl font-black mb-3">¿Querés que tus clientes reserven solos?</h2>
      <p class="text-sm text-muted mb-8">Escribime y te muestro cómo funciona.</p>
      <ContactButtons whatsapp={WHATSAPP} email={EMAIL} />
    </section>
```

- [ ] **Step 3: Remove old FeatureCard import**

Remove the line `import FeatureCard from '../components/FeatureCard.astro';` from the imports at the top of slotr.astro.

- [ ] **Step 4: Verify build passes**

Run: `npm run build`
Expected: Build succeeds

- [ ] **Step 5: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "style(slotr): redesign pricing and CTA sections to match new style"
```

---

### Task 7: Final Verification and Preview

**Files:**
- All modified files

- [ ] **Step 1: Full build verification**

Run: `npm run build`
Expected: Build succeeds without errors or warnings

- [ ] **Step 2: Preview the page**

Run: `npm run preview`
Expected: Page loads at http://localhost:4321 with:
- Hero with animated shapes, grid overlay, gradient text
- Bento grid with variable-size category cards
- SVG icons instead of emojis
- Pricing section with consistent styling
- CTA section at bottom

- [ ] **Step 3: Final commit with all changes**

```bash
git status
git add -A
git commit -m "style(slotr): complete visual redesign — hero, bento grid, SVG icons"
```

- [ ] **Step 4: Push to remote**

```bash
git push origin main
```
