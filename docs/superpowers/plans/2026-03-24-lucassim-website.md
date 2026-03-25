# lucassim Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Construir el sitio web estático de lucassim.com con 3 páginas (home, /vareapp, /slotr) usando Astro y Tailwind CSS.

**Architecture:** Astro con template minimal. Tres páginas estáticas que comparten componentes reutilizables (Navbar, Footer, ContactButtons, FeatureCard, ProductCard). Sin backend — contacto vía WhatsApp y email. Deploy en Netlify / Cloudflare Pages / GitHub Pages.

**Tech Stack:** Astro 5, Tailwind CSS 3 (pinned), Inter (Google Fonts), Node 18+

> **Nota sobre TDD:** Este proyecto no tiene lógica de negocio que unit-testear. El equivalente de "test" para un sitio estático es `npm run build` — si compila sin errores, el componente es correcto. Cada tarea termina con un build check y verificación visual en `npm run dev`.

---

## Estructura de archivos

```
lucassim/
├── astro.config.mjs
├── tailwind.config.mjs
├── package.json
├── tsconfig.json
├── .gitignore
├── netlify.toml
├── public/
│   └── favicon.svg
└── src/
    ├── layouts/
    │   └── BaseLayout.astro        # <html>, <head>, fonts, meta tags
    ├── components/
    │   ├── Navbar.astro            # showBack: boolean
    │   ├── Footer.astro            # showHomeLink: boolean
    │   ├── ContactButtons.astro    # whatsapp: string, email: string
    │   ├── FeatureCard.astro       # icon, name, description
    │   └── ProductCard.astro       # name, tagline, accent, features[], href
    └── pages/
        ├── index.astro             # Home: Hero + Productos + Contacto
        ├── vareapp.astro           # Hero + Features + Target + Plans + CTA
        └── slotr.astro             # Hero + Features + Target + Pricing + CTA
```

---

## Task 1: Inicializar proyecto Astro con Tailwind

**Files:**
- Create: `astro.config.mjs`
- Create: `tailwind.config.mjs`
- Create: `package.json` (generado por Astro)
- Create: `tsconfig.json` (generado por Astro)
- Create: `.gitignore`

- [ ] **Step 1.1: Crear proyecto Astro en el directorio existente**

Desde `C:/Proyectos/lucassim`, ejecutar:
```bash
npm create astro@latest . -- --template minimal --install --no-git
```
Cuando pregunte si sobreescribir archivos existentes: seleccionar **No** (solo tiene la carpeta `docs`).
Cuando pregunte sobre TypeScript: seleccionar **Strict**.

- [ ] **Step 1.2: Agregar Tailwind CSS v3 (pinned)**

```bash
npm install -D tailwindcss@^3 @astrojs/tailwind
npx astro add tailwind
```
Confirmar todas las preguntas con Y. Pinear v3 es importante: Tailwind 4 usa un formato de configuración incompatible con `tailwind.config.mjs`.

- [ ] **Step 1.3: Verificar que el build pasa**

```bash
npm run build
```
Esperado: `dist/` generado sin errores.

- [ ] **Step 1.4: Agregar entradas al .gitignore**

Agregar al `.gitignore` existente (o crearlo si no existe):
```
# Astro
dist/
.astro/
node_modules/

# Superpowers
.superpowers/
```

- [ ] **Step 1.5: Commit**

```bash
git init
git add astro.config.mjs tailwind.config.mjs package.json package-lock.json tsconfig.json .gitignore src/ public/
git commit -m "chore: initialize Astro + Tailwind project"
```

---

## Task 2: Tokens de diseño y layout base

**Files:**
- Modify: `tailwind.config.mjs`
- Create: `src/layouts/BaseLayout.astro`

- [ ] **Step 2.1: Configurar tokens de color en Tailwind**

Reemplazar el contenido de `tailwind.config.mjs`:
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}'],
  theme: {
    extend: {
      colors: {
        base:       '#111111',
        surface:    '#161616',
        surface2:   '#1a1a1a',
        border:     '#2a2a2a',
        muted:      '#888888',
        subtle:     '#555555',
        vareapp:    '#f97316',
        'vareapp-dark': '#140800',
        slotr:      '#7c3aed',
        'slotr-dark': '#0d0a14',
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
      },
      borderRadius: {
        card: '12px',
        inner: '8px',
      },
    },
  },
  plugins: [],
}
```

- [ ] **Step 2.2: Crear BaseLayout.astro**

Crear `src/layouts/BaseLayout.astro`:
```astro
---
interface Props {
  title: string;
  description?: string;
}

const { title, description = 'Software SaaS para negocios paraguayos.' } = Astro.props;
---

<!doctype html>
<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" content={description} />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet" />
    <title>{title}</title>
  </head>
  <body class="bg-base text-white font-sans antialiased">
    <slot />
  </body>
</html>
```

- [ ] **Step 2.3: Verificar build**

```bash
npm run build
```
Esperado: sin errores.

- [ ] **Step 2.4: Commit**

```bash
git add tailwind.config.mjs src/layouts/BaseLayout.astro
git commit -m "feat: add design tokens and base layout"
```

---

## Task 3: Componente Navbar

**Files:**
- Create: `src/components/Navbar.astro`

- [ ] **Step 3.1: Crear Navbar.astro**

```astro
---
interface Props {
  showBack?: boolean;
}

const { showBack = false } = Astro.props;
---

<nav class="fixed top-0 left-0 right-0 z-50 border-b border-border bg-base/90 backdrop-blur-sm">
  <div class="max-w-5xl mx-auto px-6 h-14 flex items-center justify-between">
    <a href="/" class="text-sm font-bold tracking-widest uppercase hover:text-muted transition-colors">
      lucassim
    </a>

    {showBack ? (
      <a href="/" class="text-sm text-muted hover:text-white transition-colors">
        ← Volver
      </a>
    ) : (
      <div class="flex gap-8">
        <a href="/#productos" class="text-sm text-muted hover:text-white transition-colors">
          Proyectos
        </a>
        <a href="/#contacto" class="text-sm text-muted hover:text-white transition-colors">
          Contacto
        </a>
      </div>
    )}
  </div>
</nav>

<!-- Spacer para compensar el navbar fijo -->
<div class="h-14"></div>
```

- [ ] **Step 3.2: Verificar build**

```bash
npm run build
```
Esperado: sin errores.

- [ ] **Step 3.3: Commit**

```bash
git add src/components/Navbar.astro
git commit -m "feat: add Navbar component with showBack prop"
```

---

## Task 4: Componente Footer

**Files:**
- Create: `src/components/Footer.astro`

- [ ] **Step 4.1: Crear Footer.astro**

```astro
---
interface Props {
  showHomeLink?: boolean;
}

const { showHomeLink = false } = Astro.props;

const socials = [
  { label: 'GitHub',    href: '#' },
  { label: 'LinkedIn',  href: '#' },
  { label: 'Twitter/X', href: '#' },
];
---

<footer class="border-t border-border mt-24">
  <div class="max-w-5xl mx-auto px-6 py-8 flex flex-col sm:flex-row items-center justify-between gap-4">
    <a href="/" class="text-sm font-bold text-muted tracking-widest uppercase hover:text-white transition-colors">
      lucassim
    </a>

    <div class="flex gap-6">
      {socials.map(s => (
        <a
          href={s.href}
          aria-disabled={s.href === '#' ? 'true' : undefined}
          class={`text-xs transition-colors ${s.href === '#' ? 'text-border cursor-default pointer-events-none' : 'text-muted hover:text-white'}`}
        >
          {s.label}
        </a>
      ))}
    </div>

    <div class="flex items-center gap-4">
      {showHomeLink && (
        <a href="/" class="text-xs text-muted hover:text-white transition-colors">
          ← Inicio
        </a>
      )}
      <span class="text-xs text-subtle">© {new Date().getFullYear()} lucassim</span>
    </div>
  </div>
</footer>
```

- [ ] **Step 4.2: Verificar build**

```bash
npm run build
```
Esperado: sin errores.

- [ ] **Step 4.3: Commit**

```bash
git add src/components/Footer.astro
git commit -m "feat: add Footer component with social links and showHomeLink prop"
```

---

## Task 5: Componentes ContactButtons, FeatureCard y ProductCard

**Files:**
- Create: `src/components/ContactButtons.astro`
- Create: `src/components/FeatureCard.astro`
- Create: `src/components/ProductCard.astro`

- [ ] **Step 5.1: Crear ContactButtons.astro**

```astro
---
interface Props {
  whatsapp: string; // URL completa: https://wa.me/595XXXXXXXXX
  email: string;    // Solo la dirección: usuario@ejemplo.com (el componente agrega mailto:)
}

const { whatsapp, email } = Astro.props;
---

<div class="flex flex-wrap gap-3 justify-center">
  <a
    href={whatsapp}
    target="_blank"
    rel="noopener noreferrer"
    class="px-6 py-2.5 rounded-lg text-sm font-semibold border border-green-800 text-green-400 hover:bg-green-950 transition-colors"
  >
    WhatsApp
  </a>
  <a
    href={`mailto:${email}`}
    class="px-6 py-2.5 rounded-lg text-sm font-semibold border border-border text-muted hover:border-muted hover:text-white transition-colors"
  >
    Email
  </a>
</div>
```

- [ ] **Step 5.2: Crear FeatureCard.astro**

```astro
---
interface Props {
  icon: string;
  name: string;
  description: string;
}

const { icon, name, description } = Astro.props;
---

<div class="bg-surface border border-border rounded-inner p-5">
  <div class="text-2xl mb-3">{icon}</div>
  <h3 class="text-sm font-bold text-white mb-1.5">{name}</h3>
  <p class="text-xs text-muted leading-relaxed">{description}</p>
</div>
```

- [ ] **Step 5.3: Crear ProductCard.astro**

```astro
---
interface Props {
  name: string;
  eyebrow: string;
  tagline: string;
  accent: 'vareapp' | 'slotr';
  features: string[];
  href: string;
}

const { name, eyebrow, tagline, accent, features, href } = Astro.props;

const accentColor = accent === 'vareapp' ? 'text-vareapp' : 'text-slotr';
const bgColor     = accent === 'vareapp' ? 'bg-vareapp-dark border-orange-950' : 'bg-slotr-dark border-violet-950';
const btnColor    = accent === 'vareapp'
  ? 'bg-vareapp hover:bg-orange-600 text-white'
  : 'bg-slotr hover:bg-violet-700 text-white';
---

<div class={`rounded-card border p-6 flex flex-col gap-4 ${bgColor}`}>
  <div>
    <p class={`text-xs font-bold uppercase tracking-widest mb-2 ${accentColor}`}>{eyebrow}</p>
    <h3 class="text-xl font-black text-white mb-2">{name}</h3>
    <p class="text-xs text-muted leading-relaxed">{tagline}</p>
  </div>

  <ul class="flex flex-col gap-1.5 flex-1">
    {features.map(f => (
      <li class="text-xs text-subtle flex items-center gap-2">
        <span class="text-border">—</span>
        {f}
      </li>
    ))}
  </ul>

  <a
    href={href}
    class={`inline-block text-center rounded-lg px-4 py-2 text-xs font-bold transition-colors ${btnColor}`}
  >
    Ver {name} →
  </a>
</div>
```

- [ ] **Step 5.4: Verificar build**

```bash
npm run build
```
Esperado: sin errores.

- [ ] **Step 5.5: Commit**

```bash
git add src/components/
git commit -m "feat: add ContactButtons, FeatureCard, and ProductCard components"
```

---

## Task 6: Página Home (`/`)

**Files:**
- Modify: `src/pages/index.astro`

- [ ] **Step 6.1: Escribir index.astro**

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import Navbar from '../components/Navbar.astro';
import Footer from '../components/Footer.astro';
import ContactButtons from '../components/ContactButtons.astro';
import ProductCard from '../components/ProductCard.astro';

const WHATSAPP = 'https://wa.me/595XXXXXXXXX';
const EMAIL    = 'lucas@ejemplo.com';

const vareappFeatures = [
  'Menú digital con categorías y variantes',
  'Gestión de pedidos en tiempo real',
  'Panel administrativo completo',
  'Caja, inventario y métricas',
];

const slotrFeatures = [
  'Reservas online para tus clientes',
  'Calendarios por recurso o profesional',
  'Múltiples servicios configurables',
  'Panel de administración de agenda',
];
---

<BaseLayout title="lucassim — Software SaaS paraguayo">
  <Navbar />

  <!-- HERO -->
  <section class="max-w-5xl mx-auto px-6 py-24 text-center">
    <p class="text-xs text-subtle uppercase tracking-widest mb-6">lucassim</p>

    <h1 class="text-4xl sm:text-5xl font-black leading-tight mb-6">
      Hola, soy Lucas.<br />
      <span class="text-muted">Ingeniero de Sistemas.</span>
    </h1>

    <p class="text-sm text-muted leading-relaxed max-w-xl mx-auto mb-4">
      Más de <strong class="text-white font-semibold">5 años de experiencia</strong> desarrollando software.
      Proactivo, orientado al crecimiento y apasionado por construir productos que resuelvan problemas reales.
    </p>

    <p class="text-sm text-subtle leading-relaxed max-w-xl mx-auto mb-10">
      Desarrollo soluciones diseñadas para el mercado paraguayo — simples, funcionales y listas para escalar.
    </p>

    <div class="flex flex-wrap gap-3 justify-center">
      <a href="#productos" class="px-6 py-2.5 rounded-lg text-sm font-bold bg-white text-black hover:bg-gray-100 transition-colors">
        Ver proyectos ↓
      </a>
      <a href="#contacto" class="px-6 py-2.5 rounded-lg text-sm font-semibold border border-border text-muted hover:border-muted hover:text-white transition-colors">
        Contacto
      </a>
    </div>
  </section>

  <!-- PRODUCTOS -->
  <section id="productos" class="max-w-5xl mx-auto px-6 py-16">
    <h2 class="text-xs text-subtle uppercase tracking-widest mb-8 text-center">Proyectos</h2>
    <div class="grid sm:grid-cols-2 gap-6">
      <ProductCard
        name="VareApp"
        eyebrow="SaaS · Gastronomía"
        tagline="Menú digital y sistema de pedidos para restaurantes, cafeterías y food trucks."
        accent="vareapp"
        features={vareappFeatures}
        href="/vareapp"
      />
      <ProductCard
        name="Slotr"
        eyebrow="SaaS · Agendamiento"
        tagline="Sistema de turnos online para clínicas, peluquerías, consultoras y canchas deportivas."
        accent="slotr"
        features={slotrFeatures}
        href="/slotr"
      />
    </div>
  </section>

  <!-- CONTACTO -->
  <section id="contacto" class="max-w-5xl mx-auto px-6 py-16 text-center">
    <h2 class="text-2xl font-black mb-3">¿Hablamos?</h2>
    <p class="text-sm text-muted mb-8 max-w-md mx-auto">
      Si te interesa alguno de los productos o tenés una consulta, escribime directamente.
    </p>
    <ContactButtons whatsapp={WHATSAPP} email={EMAIL} />
  </section>

  <Footer />
</BaseLayout>
```

- [ ] **Step 6.2: Verificar build**

```bash
npm run build
```
Esperado: sin errores, `dist/index.html` generado.

- [ ] **Step 6.3: Revisar visualmente**

```bash
npm run dev
```
Abrir `http://localhost:4321` y verificar:
- Navbar fijo con "lucassim" + links
- Hero con título, bio y CTAs
- Dos product cards lado a lado
- Sección de contacto con botones WhatsApp/Email
- Footer con socials deshabilitados

- [ ] **Step 6.4: Commit**

```bash
git add src/pages/index.astro
git commit -m "feat: build home page"
```

---

## Task 7: Página VareApp (`/vareapp`)

**Files:**
- Create: `src/pages/vareapp.astro`

- [ ] **Step 7.1: Crear vareapp.astro**

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import Navbar from '../components/Navbar.astro';
import Footer from '../components/Footer.astro';
import ContactButtons from '../components/ContactButtons.astro';
import FeatureCard from '../components/FeatureCard.astro';

const WHATSAPP = 'https://wa.me/595XXXXXXXXX';
const EMAIL    = 'lucas@ejemplo.com';

const features = [
  { icon: '🍽️', name: 'Menú digital',         description: 'Catálogo con categorías, variantes, extras y fotos de producto.' },
  { icon: '📋', name: 'Gestión de pedidos',    description: 'Pedidos en tiempo real con notificación directa por WhatsApp.' },
  { icon: '⚙️', name: 'Panel administrativo',  description: 'Control total: productos, horarios, staff y configuración del negocio.' },
  { icon: '🧾', name: 'Caja',                  description: 'Registro de ventas, impresión de tickets y facturas electrónicas habilitadas por la DNIT.' },
  { icon: '📦', name: 'Inventario',             description: 'Control de stock con alertas automáticas de bajo inventario.' },
  { icon: '📊', name: 'Métricas',               description: 'Dashboard con ventas, productos más pedidos y horas pico.' },
];

const target = ['Restaurantes', 'Cafeterías', 'Food trucks', 'Rotiserías'];

const plans = {
  esencial: {
    included: ['Menú digital', 'Gestión de pedidos', 'Panel admin', 'Caja — registro de ventas', 'Impresión de ticket*'],
    excluded: ['Factura electrónica (DNIT)', 'Inventario', 'Métricas avanzadas'],
    note: '*El ticket no tiene valor fiscal.',
  },
  pro: {
    included: ['Todo el plan Esencial', 'Factura electrónica (DNIT)', 'Inventario', 'Métricas avanzadas'],
    excluded: [],
    note: 'La factura electrónica tiene plena validez fiscal habilitada por la DNIT.',
    highlight: true,
  },
};
---

<BaseLayout
  title="VareApp — Menú digital y pedidos | lucassim"
  description="VareApp: sistema de menú digital y gestión de pedidos para restaurantes, cafeterías y food trucks en Paraguay."
>
  <Navbar showBack />

  <!-- HERO -->
  <section class="bg-gradient-to-b from-vareapp-dark to-base py-24 text-center px-6">
    <p class="text-xs font-bold uppercase tracking-widest text-vareapp mb-4">SaaS · Gastronomía</p>
    <h1 class="text-5xl font-black mb-4">VareApp</h1>
    <p class="text-sm text-muted max-w-md mx-auto mb-8 leading-relaxed">
      Menú digital y sistema de gestión de pedidos para restaurantes, cafeterías y food trucks.
    </p>
    <a
      href={WHATSAPP}
      target="_blank"
      rel="noopener noreferrer"
      class="inline-block px-8 py-3 rounded-lg text-sm font-bold bg-vareapp hover:bg-orange-600 text-white transition-colors"
    >
      Consultá por una demo
    </a>
  </section>

  <div class="max-w-5xl mx-auto px-6">

    <!-- FUNCIONALIDADES -->
    <section class="py-16">
      <h2 class="text-xl font-black mb-2">¿Qué incluye VareApp?</h2>
      <p class="text-sm text-muted mb-8">Todo lo que necesitás para digitalizar tu negocio gastronómico.</p>
      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
        {features.map(f => <FeatureCard {...f} />)}
      </div>
    </section>

    <!-- PARA QUIÉN ES -->
    <section class="py-12 border-t border-border">
      <h2 class="text-xl font-black mb-2">Ideal para negocios gastronómicos</h2>
      <p class="text-sm text-muted mb-6">Si vendés comida, VareApp se adapta a tu operación.</p>
      <div class="flex flex-wrap gap-2">
        {target.map(t => (
          <span class="px-4 py-1.5 rounded-full text-xs font-semibold border border-orange-900 text-vareapp bg-vareapp-dark">
            {t}
          </span>
        ))}
        <span class="px-4 py-1.5 rounded-full text-xs font-semibold border border-border text-muted">
          Cualquier negocio con menú y pedidos
        </span>
      </div>
    </section>

    <!-- PLANES -->
    <section class="py-12 border-t border-border">
      <h2 class="text-xl font-black mb-2">Elegí el plan que se ajusta a tu negocio</h2>
      <p class="text-sm text-muted mb-8">Precios a consultar — sin sorpresas.</p>
      <div class="grid sm:grid-cols-2 gap-6">

        <!-- Esencial -->
        <div class="bg-surface border border-border rounded-card p-6 flex flex-col">
          <p class="text-xs font-bold uppercase tracking-widest text-muted mb-2">Plan</p>
          <h3 class="text-2xl font-black mb-1">Esencial</h3>
          <p class="text-xs text-subtle italic mb-6">Consultá por el precio</p>
          <ul class="flex flex-col gap-2 flex-1 mb-6">
            {plans.esencial.included.map(f => (
              <li class="text-xs text-muted flex items-center gap-2">
                <span class="text-vareapp">✓</span> {f}
              </li>
            ))}
            {plans.esencial.excluded.map(f => (
              <li class="text-xs text-subtle flex items-center gap-2 line-through opacity-40">
                <span>✕</span> {f}
              </li>
            ))}
          </ul>
          <p class="text-xs text-subtle italic mb-4">{plans.esencial.note}</p>
          <a href={WHATSAPP} target="_blank" rel="noopener noreferrer"
            class="block text-center py-2 rounded-lg text-xs font-bold border border-border text-muted hover:border-muted hover:text-white transition-colors">
            Consultar
          </a>
        </div>

        <!-- Pro -->
        <div class="bg-vareapp-dark border border-orange-900 rounded-card p-6 flex flex-col">
          <p class="text-xs font-bold uppercase tracking-widest text-vareapp mb-2">⭐ Más completo</p>
          <h3 class="text-2xl font-black mb-1">Pro</h3>
          <p class="text-xs text-subtle italic mb-6">Consultá por el precio</p>
          <ul class="flex flex-col gap-2 flex-1 mb-6">
            {plans.pro.included.map((f, i) => (
              <li class={`text-xs flex items-center gap-2 ${i === 1 ? 'text-vareapp font-semibold' : 'text-muted'}`}>
                <span class="text-vareapp">{i === 1 ? '★' : '✓'}</span> {f}
              </li>
            ))}
          </ul>
          <p class="text-xs text-subtle italic mb-4">{plans.pro.note}</p>
          <a href={WHATSAPP} target="_blank" rel="noopener noreferrer"
            class="block text-center py-2 rounded-lg text-xs font-bold border border-vareapp text-vareapp hover:bg-vareapp hover:text-white transition-colors">
            Consultar
          </a>
        </div>

      </div>
    </section>

    <!-- CTA FINAL -->
    <section class="py-16 text-center border-t border-border">
      <h2 class="text-2xl font-black mb-3">¿Listo para digitalizar tu negocio?</h2>
      <p class="text-sm text-muted mb-8">Escribime y coordinamos una demo personalizada.</p>
      <ContactButtons whatsapp={WHATSAPP} email={EMAIL} />
    </section>

  </div>

  <Footer showHomeLink />
</BaseLayout>
```

- [ ] **Step 7.2: Verificar build**

```bash
npm run build
```
Esperado: `dist/vareapp/index.html` generado sin errores.

- [ ] **Step 7.3: Revisar visualmente**

```bash
npm run dev
```
Abrir `http://localhost:4321/vareapp` y verificar:
- Navbar con "← Volver"
- Hero con fondo naranja oscuro
- Grid de 6 features (2×3)
- Chips de tipos de negocio
- Dos planes (Esencial sin factura electrónica, Pro con)
- CTA con WhatsApp y Email
- Footer con "← Inicio"

- [ ] **Step 7.4: Commit**

```bash
git add src/pages/vareapp.astro
git commit -m "feat: build VareApp product page"
```

---

## Task 8: Página Slotr (`/slotr`)

**Files:**
- Create: `src/pages/slotr.astro`

- [ ] **Step 8.1: Crear slotr.astro**

```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
import Navbar from '../components/Navbar.astro';
import Footer from '../components/Footer.astro';
import ContactButtons from '../components/ContactButtons.astro';
import FeatureCard from '../components/FeatureCard.astro';

const WHATSAPP = 'https://wa.me/595XXXXXXXXX';
const EMAIL    = 'lucas@ejemplo.com';

const features = [
  { icon: '📅', name: 'Reservas online',        description: 'Página pública donde tus clientes reservan su turno sin llamar.' },
  { icon: '📆', name: 'Gestión de agenda',       description: 'Vista de calendario por recurso con bloqueos y cancelaciones.' },
  { icon: '🛎️', name: 'Múltiples servicios',    description: 'Configuración de servicios con duración y disponibilidad horaria.' },
  { icon: '👥', name: 'Staff y recursos',         description: 'Soporte para personas (peluqueros, profesionales) y recursos físicos (canchas, consultorios).' },
  { icon: '🔔', name: 'Notificaciones',           description: 'Aviso automático al cliente al momento de confirmar la reserva.' },
  { icon: '⚙️', name: 'Panel administrativo',    description: 'Configuración completa: horarios, servicios, bloqueos y ajustes del negocio.' },
];

const target = ['Clínicas', 'Peluquerías', 'Consultoras', 'Canchas deportivas', 'Consultorios'];

const pricingRanges = [
  { range: '1 recurso',    example: 'Consultorio individual, peluquero solo' },
  { range: '2–3 recursos', example: '3 canchas de pádel, 2 profesionales', featured: true },
  { range: '4+ recursos',  example: 'Clínica con múltiples especialistas' },
];
---

<BaseLayout
  title="Slotr — Sistema de turnos online | lucassim"
  description="Slotr: sistema de agendamiento de turnos online para clínicas, peluquerías, consultoras y canchas deportivas en Paraguay."
>
  <Navbar showBack />

  <!-- HERO -->
  <section class="bg-gradient-to-b from-slotr-dark to-base py-24 text-center px-6">
    <p class="text-xs font-bold uppercase tracking-widest text-slotr mb-4">SaaS · Agendamiento</p>
    <h1 class="text-5xl font-black mb-4">Slotr</h1>
    <p class="text-sm text-muted max-w-md mx-auto mb-8 leading-relaxed">
      Sistema de turnos online para clínicas, peluquerías, consultoras y canchas deportivas.
    </p>
    <a
      href={WHATSAPP}
      target="_blank"
      rel="noopener noreferrer"
      class="inline-block px-8 py-3 rounded-lg text-sm font-bold bg-slotr hover:bg-violet-700 text-white transition-colors"
    >
      Consultá por una demo
    </a>
  </section>

  <div class="max-w-5xl mx-auto px-6">

    <!-- FUNCIONALIDADES -->
    <section class="py-16">
      <h2 class="text-xl font-black mb-2">¿Qué incluye Slotr?</h2>
      <p class="text-sm text-muted mb-8">Todo lo que necesitás para que tus clientes reserven solos.</p>
      <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
        {features.map(f => <FeatureCard {...f} />)}
      </div>
    </section>

    <!-- PARA QUIÉN ES -->
    <section class="py-12 border-t border-border">
      <h2 class="text-xl font-black mb-2">Para cualquier negocio que trabaje con turnos</h2>
      <p class="text-sm text-muted mb-6">Si tu negocio agenda citas, Slotr es para vos.</p>
      <div class="flex flex-wrap gap-2">
        {target.map(t => (
          <span class="px-4 py-1.5 rounded-full text-xs font-semibold border border-violet-900 text-slotr bg-slotr-dark">
            {t}
          </span>
        ))}
        <span class="px-4 py-1.5 rounded-full text-xs font-semibold border border-border text-muted">
          Cualquier negocio que agenda citas
        </span>
      </div>
    </section>

    <!-- PRECIOS -->
    <section class="py-12 border-t border-border">
      <h2 class="text-xl font-black mb-2">Precio según tu equipo</h2>
      <p class="text-sm text-muted mb-2">Pagás por los calendarios que usás. Sin costos fijos por funciones que no necesitás.</p>
      <p class="text-xs text-subtle mb-8">Precio base incluye 1 recurso/calendario. Cada recurso adicional tiene un costo adicional.</p>

      <div class="flex flex-col gap-3 max-w-lg">
        {pricingRanges.map(r => (
          <div class={`flex items-center justify-between rounded-inner px-5 py-4 border ${
            r.featured
              ? 'bg-slotr-dark border-violet-800'
              : 'bg-surface border-border'
          }`}>
            <div>
              <p class={`text-sm font-bold ${r.featured ? 'text-white' : 'text-muted'}`}>{r.range}</p>
              <p class="text-xs text-subtle mt-0.5">{r.example}</p>
            </div>
            <a
              href={WHATSAPP}
              target="_blank"
              rel="noopener noreferrer"
              class={`text-xs font-semibold italic whitespace-nowrap ml-6 hover:not-italic transition-all ${
                r.featured ? 'text-slotr hover:text-violet-400' : 'text-subtle hover:text-muted'
              }`}
            >
              Consultá →
            </a>
          </div>
        ))}
      </div>
    </section>

    <!-- CTA FINAL -->
    <section class="py-16 text-center border-t border-border">
      <h2 class="text-2xl font-black mb-3">¿Querés que tus clientes reserven solos?</h2>
      <p class="text-sm text-muted mb-8">Escribime y te muestro cómo funciona.</p>
      <ContactButtons whatsapp={WHATSAPP} email={EMAIL} />
    </section>

  </div>

  <Footer showHomeLink />
</BaseLayout>
```

- [ ] **Step 8.2: Verificar build**

```bash
npm run build
```
Esperado: `dist/slotr/index.html` generado sin errores.

- [ ] **Step 8.3: Revisar visualmente**

```bash
npm run dev
```
Abrir `http://localhost:4321/slotr` y verificar:
- Navbar con "← Volver"
- Hero con fondo violeta oscuro
- Grid de 6 features (2×3)
- Chips de tipos de negocio
- 3 rangos de precio con ejemplos reales y links "Consultá →"
- CTA con WhatsApp y Email
- Footer con "← Inicio"

- [ ] **Step 8.4: Commit**

```bash
git add src/pages/slotr.astro
git commit -m "feat: build Slotr product page"
```

---

## Task 9: Configuración de deploy y pulido final

**Files:**
- Create: `netlify.toml`
- Modify: `astro.config.mjs`
- Modify: `public/favicon.svg`

- [ ] **Step 9.1: Crear netlify.toml**

```toml
[build]
  command = "npm run build"
  publish = "dist"

[build.environment]
  NODE_VERSION = "18"
```

- [ ] **Step 9.2: Verificar que el sitio enlaza correctamente entre páginas**

```bash
npm run dev
```
Verificar manualmente:
- Home: "Ver VareApp →" lleva a `/vareapp` ✓
- Home: "Ver Slotr →" lleva a `/slotr` ✓
- `/vareapp`: "← Volver" lleva a `/` ✓
- `/slotr`: "← Volver" lleva a `/` ✓
- Home: "Ver proyectos ↓" hace scroll a la sección productos ✓
- Home: "Contacto" hace scroll a la sección de contacto ✓

- [ ] **Step 9.3: Build de producción final**

```bash
npm run build
```
Esperado: sin errores ni warnings. Confirmar que existen:
- `dist/index.html`
- `dist/vareapp/index.html`
- `dist/slotr/index.html`

- [ ] **Step 9.4: Commit final**

```bash
git add netlify.toml astro.config.mjs
git commit -m "chore: add Netlify deploy config and finalize site"
```

---

## Contenido para completar antes del deploy

Buscar y reemplazar en todo el proyecto antes de lanzar:

| Placeholder | Reemplazar con |
|---|---|
| `595XXXXXXXXX` | Número de WhatsApp real (formato: `595973XXXXXX`) |
| `lucas@ejemplo.com` | Email real de contacto |
| `href: '#'` en Footer socials | URLs reales de GitHub, LinkedIn, Twitter/X |

---

## Verificación final del sitio completo

Antes de hacer el deploy, verificar cada página en `npm run dev`:

**Home (`/`)**
- [ ] Navbar fijo, links funcionales
- [ ] Hero: nombre, bio, subtítulo, CTAs
- [ ] Dos product cards con botones "Ver X →"
- [ ] Sección contacto con WhatsApp y Email
- [ ] Footer con socials (deshabilitados si son `#`)

**VareApp (`/vareapp`)**
- [ ] Navbar con "← Volver" → `/`
- [ ] Hero naranja, botón "Consultá por una demo"
- [ ] 6 features en grid 2×3
- [ ] Chips de tipos de negocio
- [ ] Plan Esencial: sin factura electrónica / Plan Pro: con factura electrónica (DNIT)
- [ ] CTA final con WhatsApp y Email
- [ ] Footer con "← Inicio"

**Slotr (`/slotr`)**
- [ ] Navbar con "← Volver" → `/`
- [ ] Hero violeta, botón "Consultá por una demo"
- [ ] 6 features en grid 2×3
- [ ] Chips de tipos de negocio (incluyendo Consultoras)
- [ ] 3 rangos de precio (1 / 2–3 / 4+) con ejemplos y "Consultá →"
- [ ] CTA final con WhatsApp y Email
- [ ] Footer con "← Inicio"
